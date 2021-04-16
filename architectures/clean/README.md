# Clean Architecture

> Reference: https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html

* Formal Definition.
* MVC and Hexagonal Architecture as precursors.
* Generalization of Clean Architectures

## Formal Definition

The Clean Architecture style aims for a loosely coupled implementation focused on use cases and it is summarized as:

1. It is an architecture style where the _Use Cases_ are the centran organizing structure.

2. Follows the _Ports and Adapters_ pattern.
  * Implementation guided by tests (TDD Outside-In).
  * Decoupled from technology details.

3. Follows lots of principles (_Dependency Rule_, _Stable Abstractions Principle_, _Stable Dependencies Principle_, _SOLID_, and so on).

## MVC as precursor

The precursor of layered architectures is the __classic MVC pattern from Smalltalk. This disentangles the model from the user interface (controller and view), so that the model does not depend on the UI__.

More complex systems do not have just one user interface, but possibly multiple user interfaces (such as a web app or a mobile app). MVC isolates the business logic on the server from these UIs, so the server doesn't care about which kind of app accesses it.

Typically, the server still depends on backend services such as databases or third party providers. This is perfectly fine, and leads to a simple layered architecture.

The __Hexagonal Architecture goes further and stops making a distinction between frontend and backend__. Any external system might be an input (data source) or an output. Our core system defines the necessary interface (ports), and we create adapters for any external systems.

One classic approach for strong decoupling is a __Service Oriented Architecture (SOA)__, where all serices publich events to and consume events from a shared bus. A similar approach was later popularized by microservices.

> Clean Architecture could be considered an evolution of related approaches like the __Onion Architecture__ by Jeffrey Palermo (2008) and the __Hexagonal Architecture__ ("_Ports and Adapters_") by Alistar Cockburn and others (< 2008).
>
> Different problems have different requirements. Clean Architecture and related approaches favor decoupling, flexibility, and dependency inversion, but sacrifice simplicity. This is not always a good deal.

## Generalization of Clean Architectures

> * __Hexagonal Architecture (Ports and Adapters)__ by Alistair Cockburn and adopted by Steve Freeman, and Nat Pryce in their book _Growing Object Oriented Software_.
> * __Onion Architecture__ by Jeffrey Palermo.
> * __Screaming Architecture__ from Robert C Martin.
> * __DCI__ from James Coplien, and Trygve Reenskaug.
> * __BCE__ by Ivar Jacobson from his book _Object Oriented Software Engineering: A Use-Case Driven Approach_.

Though architectures all vary somewhat in their details, they are very similar. They all have the same objective, which is the separation of concerns. They all achieve this separation by dividing the software into layers. Each has at least one layer for business rules, and another for interfaces.

Each of these architectures produce systems that are:

1. __Independent of Frameworks__. The architecture does not depend on the existence of some library of feature laden software. This allows you to use such frameworks as tools, rather than having to cram your system into their limited constraints.

2. __Testable__. The business rules can be tested without the UI, Database, Web Server, or any other external element.

3. __Independent of UI__. The UI can change easily, without changing the rest of the system. A Web UI could be replaced with a console UI, for example, without changing the business rules.

4. __Independent of Databse__. You can swap out Oracle or SQL Server, for Mongo, BigTable, CouchDB, or something else. Your business rules are not bound to the database.

5. __Independent of any external agency__. In fact your business rules simply don’t know anything at all about the outside world.
