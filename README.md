# Software Architect Handbook

This attempts to be a collection of the minimal least required concepts, terminology, and skills that an architect should have.

I won't be covering most of the topics in detail, some of them will be references to external sources, there's plenty of information out there if you want to do research on your own, books, blogs, videos, open source projects, etc, I rather prefer just presenting to you the fundamentals and plant the seed of curiosity in you to go and do a deeper research as needed.

The idea of this collection is not to help you become a expert of, let's say a particular architectural style, but rather get an overall knowledge of different types of architectures, pros and cons, and technical concepts that have system impact and should be considered in the broader perspective an architect should have.

## TOC

* Design Principles
* Programming Paradigms
  * Imperative and Procedural
  * Declarative
  * Functional
  * Object-oriented
* Architectural Patterns & Principles
  * Clean Architecture
  * REST
* Technology Specifics
  * Languages & Frameworks
  * Databases
  * Operating Systems
* Fundamentals Glossary

## Software Design Principles

* [SOLID](./pp/solid)
  * [Single Responsibility Principle](./pp/solid/srp.md)
  * [Open-Closed Principle](./pp/solid/ocp.md)
  * [Liskov-Substitution Principle](./pp/solid/lsp.md)
  * [Interface Segregation Principle](./pp/solid/isp.md)
  * [Dependency Inversion Principle](./pp/solid/dip.md)
* DRY
* KISS

## Programming Paradigms

* [Imperative and Procedural](./paradigms/imperative)
* [Declarative](./paradigms/declarative)
* Functional
  * Design principles
    * [Referentially Transparent (No Side Effects)](./paradigms/functional/referentially-transparent.md)

### OOP: Object Oriented Programming

* [OOP Introduction](./paradigms/oop)
  * Objects and Classes
  * Class-based vs Prototype-based languages
* [4 Pillars of OOP](./paradigms/oop/4pillars.md)
  * Abstraction
  * Inheritance
  * Encapsulation
  * Polymorphism
* [Abstract Class](./paradigms/oop/abstract-class.md)
* [Mixin Class](./paradigms/oop/mixin.md)
* [Traits](./paradigms/oop/traits.md)
* [Interface & Type](./paradigms/oop/interface.md)
* [Subtyping: Interface Inheritance](./paradigms/oop/subtyping.md)
* [Composition, Aggregation and Delegation](./paradigms/oop/cad.md)]
  * [Composition vs Inheritance](./paradigms/oop/inheritance-composition.md)
* [Parameterized Types](./paradigms/oop/inheritance-parameterized.md)
* [Dynamic Dispatch / Message Passing](./paradigms/oop/dynamic-dispatch.md)
* [OMT Notation & UML](./paradigms/notations.md)
* [Object-Oriented Design Principles](./paradigms/oop/design-principles.md)
  * Program to an interface, not an implementation
  * Favor object composition over class inheritance
* [GoF Design Patterns](https://github.com/herrera-ignacio/design_patterns/)

## Architectural Patterns & Principles

* [General Architectural Principles](./pp/architectural)
* [DAO: Data Access Object](./pp/dao)
* [Abstraction Inversion](./pp/abstraction-inversion)

### Clean Architecture

* [Components](./clean/components)
* [Component Cohesion](./clean/component-cohesion)
  * [Reuse/Release Equivalence Principle]()
  * [Common Closure Principle]()
  * [Common Reuse Principle]()
* [Component Coupling]()
* Objects
  * [Boundaries](./clean/objects/boundaries)
  * [Entities](./clean/objects/entities)
  * [Interactor](./clean/objects/interactor)
* [Use Cases](./clean/use-cases)
* [MVC Problems](./clean/mvc)
* [Plugin Architecture: MCP](./clean/mcp)
* WIP https://www.youtube.com/watch?v=o_TH-Y78tt4 46.41

#### Extra material

* [Clean Architecture Essentials](https://dev.to/ivanpaulovich/clean-architecture-essentials-5a0m)

### REST: Representational State Transfer

* [REST intro](./architectures/rest)

## Technology specifics

Specifics that should be considered while developing a software solution relying on a particular technology.

### Javascript & Node.js

* [Considerations for a better architecture](./js/considerations.md)
* [AfterAcademy, backend architecture considerations](https://afteracademy.com/blog/design-node-js-backend-architecture-like-a-pro)
* [The Working Architecture, Viktor Turskyi](js/working-architecture)

### Databases

* [ACID](./databases/acid.md)
* [Transactions](./databases/transactions.md)
* [2PC Protocol / XA Transactions](./databases/2pc.md)
* [Views](./databases/view.md)
* [Joins](./databases/joins.md)
* Stored Procedures
* Indexing
* [Object-oriented databases](./databases/object-oriented)
* [ORM: Object-relational Mapping](./databases/orm)
* [Active Record Pattern](./databases/active-record)
* Data Mapper

### Operating Systems

* [Multithreading](./os/multithreading)
* [Parallelism & Concurrency](./os/parallelism)
* [Process & Thread](./os/process-thread)

## Fundamentals Glossary

Must know terminology.

* [Modularization](./glossary/modularization)
* [Web API](./glossary/web-api)
* [Leaky Abstraction](./glossary/leaky-abstraction)