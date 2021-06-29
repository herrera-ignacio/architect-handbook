# Performance Measures

* Response time
* Responsiveness
* Latency
* Throughput
* Load
* Load sensitivity
* Capacity
* Scalability

> In this terminology, **performance** is either throughput or response time, whichever matters more to you. It can sometimes be difficult to talk about performance when a technique improves throughput but decreases response time. From a user's perspective responsiveness may be more important than response time, so improving responsiveness at a cost of response time or throughput will increase performance.

The problem is that **design decisions don't affect all of these performance factors equally**.

## Response time

Amount of **time it takes for the system to process a request from the outside**. This may be a UI action or a server API call.

## Responsiveness

**How quickly a system acknowledges a request** as opposed to processing it. This is important in many systems because users may become frustrated if a system has low responsiveness, even if its response time is good.

> If your system waits during the whole request, then your responsiveness and response time are the same. For example, providing a progress bar during a file copy improves the responsiveness of your user interface, even though it doesn't improve response time.

## Latency

**Minimum time required to get any form of response**, even if the work to be done is nonexistent.

> This is the reason why you should minimize remote calls. If I ask a program to do nothing, but to tell me when it's done doing nothing, then I should get an almost instantaneous response if the program runs on my local computer. However, if the program runs on a remote computer, I may get a few seconds just because of the time take for the request and resposne to make their way across the wire.

## Troughput

**How much stuff you can do in a given amount of time**. If you're timing the copying of a file, throughput might be measured in bytes per second. For enterprise applications a typical measure is transactions per second (*tps*).

## Load

**How much stress a system is under**, which might be measured in how many users are currently connected to it. The load is usually in *context for some other measurement*, such as a response time. Thus, you may say that the response time for some request is 0.5 seconds with 10 users and 2 seconds with 20 users.

## Load sensitivity

Is an expression of **how the response time varies with the load**.

## Capacity

Indication of **maximum effective throughput or load**. This might be an absolute maximum or a point at which performance dips below an acceptable threshold.

## Scalability

Measure of **how adding resources affects performance**. A scalable system is one that allows you to add hardware and get a commensurate performance improvement, such as doubling how many servers you have to double your throughput.

**Vertical scalability** or **scaling up**, means adding more power to a single server, such as more memory. **Horizontally scalability** or **scaling out** means adding more servers.
