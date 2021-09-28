# Design a Notification System

* Step 1: Understand the problem and establish design scope
* Step 2: Propose high-level design and get buy-in
* Step 3: Design deep dive
* Step 4: Wrap up

## Overview

A notification alerts a user with important information like breaking news, product updates, events, offering, etc.

A notification is more than just mobile push notification. Three types of notification formats are: mobile push notification, SMS message, and Email.

![](2021-09-27-16-43-46.png)

## Step 1: Understand the problem and establish design scope

The interview question is purposely designed to be open-ended and ambiguous, and it is your responsability to ask questions to clarify the requirements.

**Candidate**: What types of notification does the system support?
**Interviewer**: Push notification, SMS message, and email.

**Candidate**: Is it a real-time system?
**Interviewer**: Let us say it is a soft real-time system. We want a user to receive notifications as soon as possible. However, if the system is under a high workload, a slight delay is acceptable.

**Candidate**: What are the supported devices?
**Interviewer**: iOS devices, android devices, and laptop/desktop.

**Candidate**: What triggers notifications?
**Interviewer**: Notifications can be triggered by client applications. They can also be scheduled on the server-side.

**Candidate**: will users be able to opt-out?
**Interivewer**: Yes, users who choose to opt-out will no longer receive notifications.

**Candidate**: How many notificatiuons are sent out each day?
**Interviewer**: 10 million mobile push notifications, 1 million SMS messages, and 5 million emails.

## Step 2: Propose high-level design and get buy-in

* Different types of notifications
* Contact info gathering flow
* Notification sending/receiving flow

### Different types of notifications

![](2021-09-27-22-33-50.png)

#### iOS Push Notification

![](2021-09-27-16-54-46.png)

We primary need three components to send an iOS push notification:

* **Provider**: Builds and sends notification requests to *Apple Push Notification Service (APNs)*. To construct a push notification, the provider provides the following data:
  * *Device token*: This is a unique identifier used for sending push notifications.
  * *Payload*: This is a JSON object that contains a notification's payload. 
* **APNS**: Remote service provided by Apple to propagate push notifications to iOS devices.
* **iOS Device**: End client which receives push notifications.

#### Android Push Notification

![](2021-09-27-22-26-43.png)

Android adopts a similar notification flow. Instead of using APNs, *Firebase Cloud Messaging (FCM)* is commonly used to send push notifications to android devices.

#### SMS Message

![](2021-09-27-22-29-39.png)

For SMS messages, third party SMS services like *Twilio*, *Nexmo*, and many others are commonly used.

#### Email

Although companies can set up their own email servers, many of them opt for commercial email services such as *Sendgrid* and *Mailchimp*.

![](2021-09-27-22-32-59.png)

### Contact info gathering flow

To send notifications, we need to gather mobile device tokens, phone numbers, or email addresses. When a ser installs our app or signs up for the first time, API servers collect user contact info and store it in the database.

![](2021-09-27-22-36-47.png)

These are implified database tables to store contact info. Email addresses and phone numbers are stored in the *user* table, whereas device tokens are stored in the *device* table. A user can have multiple devices, indicating that a push notification can be sent to all the user devices.

![](2021-09-27-22-38-28.png)

### Notification sending/receiving flow

#### High-level design

![](2021-09-27-22-39-26.png)

* **Service 1 to N**: A service can be a micro-service, a cron job, or a distributed system that triggers notification sending events. For example, a billing service sends emails to remind customers of their due payment or a shopping website tells customer that their packages will be delivered tomorrow via SMS messages.

* **Notification system**: This is the centerpiece of sending/receiving notifications. Starting with something simple, only one notification server is used. It provides APIs for services 1 to N, and builds notification payloads for third party services.

* **Third-party services**: These are responsible for delivering notifications to users. While integrating with third-party services, we need to pay extra attention to extensibility. Good extensibility means a flexible system that can easily plugging or unplugging of a third party service. Another important consideration is that a third-party service might be unavailable in new markets or in the future. For instance, FCM is unavailable in China. Thus, alternative third-party services such as Jpush, PushY, etc are used there.

* **iOS, Android, SMS, Email**: Users receive notifications on their devices.

Three problems are identified in this design:

* *Single point of failure (SPOF)*: A single notification server means SPOF.
* *Hard to scale*: The notification system handles everything related to push notification in one server. It is challenging to scale databases, caches, and different notification processing components independently.
* *Performance bottleneck*: Processing and sending notifications can be resource intensive. For example, constructing HTML pages and waiting for responses from third party services could take time. Handling everything in one system can result in the system overload, especially during peak hours.

#### High-level design (improved)

* Move the database and cache out of the notification server.
* Add more notification servers and set up automatic horizontal scaling.
* Introduce message queues to decouple the system components.

![](2021-09-27-22-55-13.png)

* **Notification servers**:
  * Provide APIs for services to send notifications. Those APIs are only accessible internally or by verified clients to prevent spams.
  * Carry out basic validations to verify emails, phone numbers, etc.
  * Query the database or cache to fetch data needed to render a notification.
  * Put notification data to message queues for parallel processing.
* **Cache**: User info, device info, notification templates are cached.
* **DB**: It stores data about user, notification, settings, etc.
* **Message queues**: They remove dependencies between components. Message queues serve as buffers when high volumes of notifications are to be sent out. Each notification type is assigned with a distinct message queue so an outage in one third-party service will not affect other notification types.
* **Workers**: Workers are a list of servers that pull notification events from message queues and send them to the corresponding third-party services.
* **Third-party services**: Already explained.

#### Sending/receiving flow

![](2021-09-27-23-14-03.png)

> Example POST `https://api.example.com/v/sms/send`

1. A service calls APIs provided by notification servers to send notifications.
2. Notification servers fetch metadata such as user info, device token, and notification setting from the cache or database.
3. A notification event is sent to the corresponding queue for processing. For instance, an iOS push notification event is sent to the iOS PN queue.
4. Workers pull notification events from message queues.
5. Workers send notifications to third party services.
6. Third-party services send notifications to user devices.

### Step 3: Design deep dive

We will explore the following in deep dive:

* Reliability.
* Additional components and considerations: notification template, notification settings, rate limiting, retry mechanism, security in push notifications, monitor queued notifications and event tracking.
* Updated design.

#### Reliability

* **How to prevent data loss?**: Notifications can usually be delayed or re-ordered, but never lost. To satisfy this requirement, the notification system persists notification data in a database and implements a retry mechanism. The notification log database is included for data persistance.

![](2021-09-27-23-13-51.png)

* **Will recipients receive a notification exactly once?**: The short answer is no. The distributed nature could result in duplicate notifications. To reduce the duplication occurrence, we introduce a dedupe mechanism and handle each failure case carefully.

> A simple dedupe logic: When a notification event first arrives, we check if it is seen before by checking the event ID. If it is seen before, it is discarded. Otherwise, we will send out the notification.

### Additional components and considerations

#### Notification template

A large notification system sends out millions of notifications per day, and many of these notifications folow a similar format. Notification templates are introduced to avioid building every notification from scratch by using a preformatted notification to create unique notification by customizing parameters, styling, tracking limits, etc.

The benefits include:

* Maintaining a consistent format.
* Reducing the margin error.
* Saving time.

#### Notification setting

You may want to provide users fine-grained control over notification settings. This information can be stored for example in the notification setting table with the following fields:

* user_id - bigInt
* channel - varchar # push notification, email or SMS
* opt_in - boolean # opt-in to receive notification

Before any notification is sent to a user, we first check if a user is opted-in to receive this type of notification.

#### Rate limiting

To avoid overwhelming users with too many notifications, we can limit the number of notifications a user can receive. This can help to avoid users turning off notifications completely.

#### Retry mechanism

When a third-party service fails to send a notification, the notification will be added to the mssage queue for retrying. If the proble mpersists, an alert will be sent out to developers.

#### Security in push notifications

For iOS or Android apps, appKey and appSecret are used to secure push notification APIs. Only authenticated or verified clients are allowed to send push notifications using our APIs.

#### Monitor queued notifications

A key metric to monitor is the total number of queued notifications. If the number is large, the notification events are not processed fast enough by workers. To avoid delay in the notification delivery, more workers are needed.

![](2021-09-27-23-26-44.png)

#### Events tracking

Notification metrics, such as open rate, click rate, and engagement are important in understanding customer behaviors. Analytics service implements events tracking. Integration between the notification system and the analytics service is usually required.

![](2021-09-27-23-27-26.png)

### Updated design

![](2021-09-27-23-27-46.png)

Many new components are added:

* Notification servers are equipped with two more critical features: *Authentication* and *Rate limiting*.

* We also add a *Retry mechanism* to handle notification failures. If the system fails to send notifications, they are put back in the messaging queue and the workers will retry for a predefined number of times.

* Furthermore, *notification templates* provide a consistent and efficient notification creation process.

* Finally, *monitoring and tracking systems* are added for system health checks and future improvements.

## Step 4: Wrap up

We described the design of a scalable notification system that supports multiple notification formats: push notification, SMS, and email. We adopted message queues to decouple system components.

Besides the high-level design, we dug deep into more components and optimizations:

* **Reliability**: Robust retry mechanism to minimize the failure rate.

* **Security**: appKey/appSecret pair is used to ensure only verified clients can send notifications.

* **Tracking and monitoring**: These are implemented in any stage of a notification flow to capture important stats.

* **Respect user settings**: Users may opt-ut of receiving notifications. Our system checks user settings first before sending notifications.

* **Rate limiting**: Users will appreciate a frequency capping on the number of notifications they receive.
