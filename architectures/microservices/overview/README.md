# Microservice Architecture

## Overview 
Microservice architecture is a *variant of the service-oriented architecture (SOA)*, it arranges an application as a **collection of loosely-coupled services**.

> A **microservice** is not a layer within a monolithic application (i.e, web controller or backend-for-frontend). Rather **it is a self-contained piece of business functionality with clear interfaces**, and may, through its own internal components, implement a layered architecture.

Microservice architecture try to improve some of the disadvantages and restrictions of monolith applications caused by lack of modularity.

> Modularity supports reuse of parts of the application logic and also facilitates maintenance by allowing repair or replacement of parts of the application without requiring wholesale replacement.

Modularity is achieved to various extents by *different modularization approaches*. **Service-oriented architectures use specific communication standards/protocols to communicate between modules**.

![](2021-06-08-12-03-00.png)

Current applications usually want to provide real-time notifications, for that we need an *Event Streaming Middleware* (i.e. Apache Kafka).

![](2021-06-08-12-03-59.png)
