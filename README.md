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
* Design Patterns & Principles
  * Base patterns
  * Data source & persistence
* Architectural styles
  * Clean Architecture
  * REST
* Technology Specifics
  * Languages & Frameworks
  * Databases
  * Operating Systems
* Fundamentals Glossary

## Design Principles

* [SOLID](./principles/solid)
  * [Single Responsibility Principle](./principles/solid/srp
  * [Open-Closed Principle](./principles/solid/ocp)
  * [Liskov-Substitution Principle](./principles/solid/lsp)
  * [Interface Segregation Principle](./principles/solid/isp)
  * [Dependency Inversion Principle](./principles/solid/dip.md)
* DRY
* KISS
* [General Architectural Principles](./principles/architectural)

## Programming Paradigms

* [Imperative and Procedural](./paradigms/imperative)
* [Declarative](./paradigms/declarative)

### [Structured](./paradigms/structured)

* [Functional Decomposition](./paradigms/structured/functional-decomposition)
* [Tests](./paradigms/structured/tests)

### OOP: Object Oriented Programming

* [OOP Introduction](./paradigms/oop)
  * Objects and Classes
  * Class-based vs Prototype-based languages
* [4 Pillars of OOP](./paradigms/oop/4pillars.md)
  * Abstraction
  * Inheritance
  * Encapsulation
  * Polymorphism
* [The Power of Polymorphism](./paradigms/oop/polymorphism)
* [Abstract Class](./paradigms/oop/abstract-class.md)
* [Mixin Class](./paradigms/oop/mixin.md)
* [Traits](./paradigms/oop/traits.md)
* [Interface & Type](./paradigms/oop/interface.md)
* [Subtyping: Interface Inheritance](./paradigms/oop/subtyping.md)
* [Composition, Aggregation and Delegation](./paradigms/oop/cad.md)]
  * [Composition vs Inheritance](./paradigms/oop/inheritance-composition.md)
* [Parameterized Types](./paradigms/oop/inheritance-parameterized.md)
* [Dynamic Dispatch / Message Passing](./paradigms/oop/dynamic-dispatch.md)
* [OMT Notation & UML](./paradigms/oop/omt-notations.md)
* [Object-Oriented Design Principles](./paradigms/oop/design-principles.md)
  * Program to an interface, not an implementation
  * Favor object composition over class inheritance
* [GoF Design Patterns](https://github.com/herrera-ignacio/design_patterns/)
* [Prototypal OO](./paradigms/oop/prototypal-oo)

### [Functional](./paradigms/functional/README.md) 

* [Referentially Transparent (No Side Effects)](./paradigms/functional/referentially-transparent.md)
* [Immutability](./paradigms/functional/immutability)

## Design Patterns & Principles

* [Abstraction Inversion](./design-patterns/abstraction-inversion)
* [MVC: Model-View-Controller](./design-patterns/mvc)

### Base Patterns

* [Mapper](./design-patterns/base/mapper)

### Data Source & Persistence

* [DAO: Data Access Object](./design-patterns/data/dao)
* [Active Record](./design-patterns/data/active-record)
* [Data Mapper](./design-patterns/data/data-mapper)

#### Object-relational Metadata Mapper

* [Repository](./design-patterns/data/repository)

## Architectural Styles

* [Architecture](./architectures/general/definition)
* [Development Overconfidence](./architecture/general/overconfidence)
* [Developer Struggle](./architecture/general/developer-struggle)

### [Ports & Adapters / Hexagonal](./architectures/hexagonal)

### [Clean Architecture](./architectures/clean)

* [MVC and Hexagonal Architectures as Precursors](./architectures/clean/precursors)
* [MVC Problems](./architectures/clean/mvc)
* [Plugin Architecture: MCP](./architectures/clean/mcp)
* WIP https://www.youtube.com/watch?v=o_TH-Y78tt4 46.41
* [Tradeoffs](./architectures/clean/tradeoffs)

#### Clean Architecture - Glossary

* [Stable Abstractions Rule](./architectures/clean/stable-abstractions)
* [Components](./architectures/clean/components)
* [Component Cohesion](./architectures/clean/component-cohesion)
  * [Reuse/Release Equivalence Principle]()
  * [Common Closure Principle]()
  * [Common Reuse Principle]()
* [Component Coupling]()
* Objects
  * [Boundaries](./architectures/clean/objects/boundaries)
  * [Entities](./architectures/clean/objects/entities)
  * [Interactor](./architectures/clean/objects/interactor)
* [Use Cases](./architectures/clean/use-cases)

#### Clean Architecture - Extra material

* [Clean Architecture Essentials](https://dev.to/ivanpaulovich/clean-architecture-essentials-5a0m)

### REST: Representational State Transfer

* [Introduction](./architectures/rest/intro.md)
* [History](./architectures/rest/history.md)
* [Architectural Properties](./architectures/rest/properties.md)
* [Architectural Constraints](./architectures/rest/constraints.md)
* [Semantics of HTTP APIs](./architecture/rest/http-methods.md)

### [Flux](./architectures/flux)

* [MVC Comparison](./mvc-comparison)

## Technology specifics

Specifics that should be considered while developing a software solution relying on a particular technology.

### Javascript & Node.js

* [Considerations for a better architecture](./js/considerations.md)
* [AfterAcademy, backend architecture considerations](https://afteracademy.com/blog/design-node-js-backend-architecture-like-a-pro)
* [The Working Architecture, Viktor Turskyi](js/working-architecture)

### React

* [Thinking in React](https://reactjs.org/docs/thinking-in-react.html)

### Redux

* [When and when not to reach for Redux](./redux/when)
* [Redux must know](./redux/introduction)
* [Three Fundamental Principles](./redux/three-principles)
* [Best Practices](./redux/best-practices)
* Structuring Reducers
  * [Immutable Update Patterns](./redux/immutable-updates)
* [Redux Ecosystem Links](https://github.com/markerikson/redux-ecosystem-links)
* [Flux Comparison](./redux/flux-comparison)

### Databases

* [ACID](./databases/acid.md)
* [Transactions](./databases/transactions.md)
* [2PC Protocol / XA Transactions](./databases/2pc.md)
* [Views](./databases/view.md)
* [Joins](./databases/joins.md)
* Stored Procedures
* Indexing
* [Object-oriented databases](./databases/object-oriented)
* [ORM: Object-relational Madesign-patternsing](./databases/orm)
* [Object-relational impedance mismatch](./databases/impedance-mismatch)

### Operating Systems

* [Multithreading](./os/multithreading)
* [Parallelism & Concurrency](./os/parallelism)
* [Process & Thread](./os/process-thread)

## Models of Computation

* [Finite State Machine](/./models-of-computation/fsm)

## Fundamentals Glossary

Must know terminology.

* [CRUD](./glossary/crud)
* [Abstract Syntax Tree](./glossary/ast)
* [Anti-Pattern](./glossary/anti-pattern)
* [Modularization](./glossary/modularization)
* [Web API](./glossary/web-api)
* [Leaky Abstraction](./glossary/leaky-abstraction)
* [First-class citizen](./glossary/first-class-citizen)
* [Side Effect](./glossary/side-effect)
* [Idempotence](./glossary/idempotence)
