# Service Layer

> *"Defines an application's boundary with a layer of services that establishes a set of available operations and coordinates the application's response in each operation."* - Randy Stafford

* Overview
* How It Works
  * Kinds of "Business Logic"
  * Implementation Variations
  * To Remote or Not to Remote
  * Identifying Services and Operations
* When to Use It
* Case Study: The Revenue Recognition Problem

## Overview

![](2021-06-26-15-40-38.png)

Enterprise applications typically need different kinds of interfaces to the data they store and they implement: data loaders, user interfaces, integration gateways, and others. Despite their different purposes, these interfaces often need **common interactions** with the application to **access and manipulate its data and invoke its business logic**. The interactions may be complex, involving transactions across multiple resources and the coordination of several responses to an action. Encoding the lgoic of the interactions separately in each interface causes a lot of duplication.

A *Service Layer* defines an application's **boundary** and its set of available operations from the perspective of **interfacing client layers**. It **encapsulates the application's business logic**, controlling transactions and coordinating responses in the implementation of its operations.

## How It Works

A *Service Layer* can be implemented in a couple of different ways. The differences appear in the allocation of responsibility behind the *Service Layer* interface.

### Kinds of "Business Logic"

Many designers like to device "business logic" into two kinds: "*domain logic*", having to do pruely with the problem domain (such as strategies for calculating revenue recognition on a contract), and "*application logic*" also sometimes refered to as "*workflow logic*", having to do with application responsibilities (such as notifying contract administrators, and integrated applications, of revenue recognition calculations).

Putting *application logic* into pure domain object classes has a couple of undesirable consequences:

1. Domain object class are less reusable across applications if they implement application-specific logic and depend on application-specific packages.

2. Harder to reimplement the application logic in, say, a workflow tool if that should ever become desirable.

For this reasons, *Service Layer* **factors each kind of business logic into a separate layer**, yielding the usual benefits of layering and rendering the pure domain object classes more reusable from application to application.

### Implementation Variations

The two basic implementation variations are the **Domain Facade** approach and the **Operation Script** approach.

#### Domain Facade Approach

A *Service Layer* is implemented as a **set of thin facades** over a *Domain Model*. The classes implementing the facades **don't implement any business logic**. Rather, the *Domain Model* implements all of the business logic.

The thin facades **establish a boundary and set of operations** through which client layers interact with the application, exhibiting the defining charactersitics of *Service Layer*.

#### Operation Script Approach

A *Service Layer* is implemented as a set of thicker classes that directly **implement application logic** but delegate to encapsulated domain object classes for domain logic.

The operations available to clients of a *Service Layer* are implemented as **scripts**, organized several to a class defining a subject area of related logic. Each such class forms an application "*service*". A *Service Layer* is comprised of these application service classes, which should extend a *Layer Supertype*, abstracting their responsibilities and common behavior.

### To Remote or Not to Remote

The interface of a *Service Layer* class is **coarse grained** almost by definition, since it declares a set of application operations available to **interfacing client layers**. Therefore, *Service Layer* classes are **well suited to remote invocation from an interface granularity perspective**.

However, remote invocations comes at the **cost of dealing with object distribution**. It likely entails a lot of extra work to make your *Service Layer* method signatures __deal in *Data Transfer Objects*__, especially if you have a complex *Domain Model* and rich editing UIs.

> "My Advice is to start with a locally invocable *Service Layer* whose method signatures deal in domain objects. Add remotabilit when you need it by putting *Remote Facades* on yoru *Service Layer*, or having your *Service Layer* objects implement remote interfaces." - Martin Fowler

### Identifying Services and Operations

They're determined by the need of *Service Layer* clients, the most significant of which is typically a user interface. Thus, the starting point for identifying *Service Layer* operations is **the use case model** and **the user interface design** for the application.

> Many of the use cases in an enterprise application are fairly boring "CRUD" use cases on domain objects. The application's responsibilities in carrying out these use cases, however, may be anything but boring. Validation aside, each operation increasingly requires notification of other people and other integrated applications. This response must be coordinated and transaccted atomically, by *Service Layer* operations.

## When to Use It

The benefit of *Service Layer* is that it **defines a common set of application operations** available to many kinds of clients and it **coordinates** an application's response in each operation.

In an application with **more than one kind of client of its business logic**, and complex responses in its use cases involving **multiple transactional resources**, it makes a lot of sense to include a *Service Layer* with **container-managed transactions**, even in an undistributed architecture.

You probably **don't need** a *Service Layer* if your application's business logic will only have one kind of client (say, a user interface) and its use case responses don't involve multiple transactional resources.

> "But as soon as you envision a second kind of client, or a second transactional resource in use case responses, it pays to design in a *Service Layer* from the beginning." - Martin Fowler 

## Case Study: The Revenue Recognition Problem

> [The Revenue Recognition Problem](../../../problems/revenue-recognition)

### Java Example


This example ueses **operation script** approach to implement a *Service Layer* with POJOs, demonstrating how *Service Layer* is used to script application logic and delegate for domain logic.

To make the demostration we expand the scenario to include some application logic. Suppose the use cases for the application require that, when the revenue recognitions for a contract are calculated, the application must respond by sending an e-mail notification of that event to a designated contract administrator and by publishing a message using message-oriented middleware to notify other integrated applications.

![](2021-06-27-16-23-11.png)

> RecognitionService POJO class diagram

```java
public class ApplicationService {
  protected EmailGateway getEmailGateway() {
    // return an instance of EmailGateway
  }

  protected IntegrationGateway getIntegrationGateway() {
    // return an instace of IntegrationGateway
  }
}

public interface EmailGateway {
  void sendEmailMessage(String toAddress, String subject, String body);
}

public interface IntegrationGateway {
  void publishRevenueRecognitionCalculation(Contract contract);
}

public class RecognitionService extends ApplicationService {
  // ...

  public void calculateRevenueRecognitions(long contractNumber) {
    // Delegate to domain object
    Contract contract = Contract.readForUpdate(contractNumber);
    contract.calculateRecognitions();

    // Coordinate Application logic
    getEmailGateway().sendEmailMessage(
      contract.getAdministratorEmailAddress(),
      "RE: Contract #" + contractNumber,
      contract + " has had revenue recognitions calculated."
    );

    getIntegrationGateway().publishRevenueRecognitionCalculation(contract);
  }

  public Money recognizedRevenue(long contractNumer, Date asOf) {
    // Delegate to domain object
    return Contract.read(contractNmber).recognizedRevenue(asOf);
  }
}
```

**Persistence details are left out of the example**. The `Contract` class implements static methods to read contracts from the Data Source layer by their numbers. One of these methods has a name revealign an intention to update the contract that's read.

**Transaction control details are left out of the example**. The `calculateRevenueRecognitions()` method is inherently transactional because, during its execution, persistent contract objects are modified via addition of revenue recognitions; messages are enqueued in message-oriented middleware, and e-mail messages are sent. All of these responses must be transacted atomically because we don't want to send e-mail and publish messages to other applications if the contract changes fail to persist.

The important point about the example is that the *Service Layer* **uses both scripting and domain object classes in coordinating the transactional response of the operation**.
