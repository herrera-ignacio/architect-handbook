# Software Architect Handbook

This attempts to be a collection of the minimal least required concepts, terminology, and skills that an architect should have.

I won't be covering most of the topics in detail, some of them will be references to external sources, there's plenty of information out there if you want to do research on your own, books, blogs, videos, open source projects, etc, I rather prefer just presenting to you the fundamentals and plant the seed of curiosity in you to go and do a deeper research as needed.

The idea of this collection is not to help you become a expert of, let's say a particular architectural style, but rather get an overall knowledge of different types of architectures, pros and cons, and technical concepts that have system impact and should be considered in the broader perspective an architect should have.

## TOC

* Design Principles
* Programming Paradigms
* Design Patterns & Principles
* Anti-Patterns
* Types of Software
* Architectural styles
* System Design
* Databases
* Distributed Systems
* Technology Specifics
* Models of Computation
* Well-known problems
* Glossary
  * Laws & Theorems

## Design Principles

* [SOLID](./principles/solid)
  * [Single Responsibility Principle](./principles/solid/srp)
  * [Open-Closed Principle](./principles/solid/ocp)
  * [Liskov-Substitution Principle](./principles/solid/lsp)
  * [Interface Segregation Principle](./principles/solid/isp)
  * [Dependency Inversion Principle](./principles/solid/dip)
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
* [Gamma Design Patterns](https://github.com/herrera-ignacio/design_patterns/)
* [Prototypal OO](./paradigms/oop/prototypal-oo)

### [Functional](./paradigms/functional/README.md) 

* [Referentially Transparent (No Side Effects)](./paradigms/functional/referentially-transparent.md)
* [Immutability](./paradigms/functional/immutability)
* [Idempotence](paradigms/functional/idempotence)

## Design Patterns & Principles

> [What is a design pattern?](https://github.com/herrera-ignacio/design_patterns/blob/master/introduction/design-pattern.md)
* Base Patterns
* General / Architectural
* Gang Of Four Patterns (GoF) 
* Domain Logic
* Data Source Pesistence
* Object-Relational
  * Behavioral 
  * Structural
  * Metadata Mapping
* Web Presentation
* Distribution
* Offline Concurrency

### Base Patterns

* [Gateway](design-patterns/base/gateway)
* [Mapper](design-patterns/base/mapper)
* [Layer Supertype](design-patterns/base/layer-supertype)
* [Separated Interface](design-patterns/base/separated-interface)
* [Registry](design-patterns/base/registry)
* [Value Object](design-patterns/base/value-object)
  * [Money](design-patterns/base/value-object/money)
* [Special Case](design-patterns/base/special-case)
* [Plugin](design-patterns/base/plugin)
* [Service Stub](design-patterns/base/service-stub)
* [Record Set](design-patterns/base/record-set)

### General / Architectural 

* [Event Sourcing](design-patterns/architectural/event-sourcing)

### Gang of Four Patterns

Please check the [this repository](https://github.com/herrera-ignacio/design_patterns/) for a detailed explanation and examples of each of the following patterns.

| [Creational](https://github.com/herrera-ignacio/design_patterns/tree/master/creational) | [Structural](https://github.com/herrera-ignacio/design_patterns/tree/master/structural) | [Behavioral](https://github.com/herrera-ignacio/design_patterns/tree/master/structural/behavioral-patterns) |
|------------------	|------------	|------------	|
| [Abstract Factory](https://github.com/herrera-ignacio/design_patterns/tree/master/creational/abstract-factory) | [Adapter](https://github.com/herrera-ignacio/design_patterns/tree/master/structural/adapter) | [Chain of Responsibility](https://github.com/herrera-ignacio/design_patterns/tree/master/behavioral/chain-of-responsibility) |
| [Builder](https://github.com/herrera-ignacio/design_patterns/tree/master/creational/builder) | [Bridge](https://github.com/herrera-ignacio/design_patterns/tree/master/structural/bridge) | [Command](https://github.com/herrera-ignacio/design_patterns/tree/master/behavioral/command) |
| [Factory Method](https://github.com/herrera-ignacio/design_patterns/tree/master/creational/factory-method) | [Composite](https://github.com/herrera-ignacio/design_patterns/tree/master/structural/composite) | [Interpreter](https://github.com/herrera-ignacio/design_patterns/tree/master/behavioral/interpreter) |
| [Prototype](https://github.com/herrera-ignacio/design_patterns/tree/master/creational/prototype) | [Decorator](https://github.com/herrera-ignacio/design_patterns/tree/master/structural/decorator) | [Iterator](./behavioral/iterator) |
| [Singleton](https://github.com/herrera-ignacio/design_patterns/tree/master/creational/singleton) | [Facade](https://github.com/herrera-ignacio/design_patterns/tree/master/structural/facade) | [Mediator](https://github.com/herrera-ignacio/design_patterns/tree/master/behavioral/mediator) |
| | [Flyweight](https://github.com/herrera-ignacio/design_patterns/tree/master/structural/flyweight) | [Memento](https://github.com/herrera-ignacio/design_patterns/tree/master/behavioral/memento) |
| | [Proxy](https://github.com/herrera-ignacio/design_patterns/tree/master/structural/proxy) | [Observer](https://github.com/herrera-ignacio/design_patterns/tree/master/behavioral/observer) |
| | | [State](https://github.com/herrera-ignacio/design_patterns/tree/master/behavioral/state) |
| | | [Strategy](https://github.com/herrera-ignacio/design_patterns/tree/master/behavioral/strategy) |
| | | [Template Method](https://github.com/herrera-ignacio/design_patterns/tree/master/behavioral/template-method) |
| | | [Visitor](https://github.com/herrera-ignacio/design_patterns/tree/master/behavioral/visitor) |

### Domain Logic

* [Transaction Script](design-patterns/domain-logic/transaction-script)
* [Domain Model](design-patterns/domain-logic/domain-model)
* [Table Module](design-patterns/domain-logic/table-module)
* [Service Layer](design-patterns/domain-logic/service-layer)

### Data Source & Persistence

* [DAO: Data Access Object](design-patterns/data/dao)
* [Active Record](design-patterns/data/active-record)
* [Data Mapper](design-patterns/data/data-mapper)
* [Table Data Gateway](design-patterns/data/table-data-gateway)
* [Row Data Gateway](design-patterns/data/row-data-gateway)
* [Repository](design-patterns/data/repository)

### Object Relational

#### Behavioral

* [Unit of Work](design-patterns/object-relational/behavioral/unit-of-work)
* [Identity Map](design-patterns/object-relational/behavioral/identity-map)
* [Lazy Load](design-patterns/object-relational/behavioral/lazy-load)

#### Structural

* [Identity Field](design-patterns/object-relational/structural/identity-field)
* [Foreign Key Mapping](design-patterns/object-relational/structural/foreign-key-mapping)
* [Association Table Mapping](design-patterns/object-relational/structural/association-table-mapping)
* [Dependent Mapping](design-patterns/object-relational/structural/dependent-mapping)
* [Embedded Value / Aggregate Mapping](design-patterns/object-relational/structural/embedded-value)
* [Serializd LOB](design-patterns/object-relational/structural/serialized-lob)
* [Single Table Inheritance](design-patterns/object-relational/structural/single-table-inheritance)
* [Class Table Inheritance / Root-Leaf Mapping](design-patterns/object-relational/structural/class-table-inheritance)
* [Concrete Table Inheritance](design-patterns/object-relational/structural/concrete-table-inheritance)
* [Inheritance Mappers](design-patterns/object-relational/structural/inheritance-mappers)

#### Metadata Mapping

* [Metadata Mapping](design-patterns/object-relational/metadata-mapping/metadata-mapping)
* [Query Object](design-patterns/object-relational/metadata-mapping/query-object)
* [Repository](design-patterns/object-relational/metadata-mapping/repository)

### Web Presentation

* [Model View Controller](design-patterns/web-presentation/mvc)
* [Page Controller](design-patterns/web-presentation/page-controller)
* [Front Controller](design-patterns/web-presentation/front-controller)
* [Template View](design-patterns/web-presentation/template-view)
* [Transform View](design-patterns/web-presentation/transform-view)
* [Two Step View](design-patterns/web-presentation/two-step-view)

### Distribution

* [Remote Facade](design-patterns/distribution/remote-facade)
* [Data Transfer Object](design-patterns/distribution/dto)

### Offline Concurrency

* [Optimistic Offline Lock](design-patterns/offline-concurrency/optimistic-offline-lock)
* [Pessimistic Offline Lock](design-patterns/offline-concurrency/pessimistic-offline-lock)
* [Coarse-Grained Lock](design-patterns/offline-concurrency/coarse-grained-lock)

### Session State

* [Client Session State](design-patterns/session-state/client)
* [Server Session State](design-patterns/session-state/server)
* [Database Session State](design-patterns/session-state/database)

## Anti-Patterns

* [Abstraction Inversion](anti-patterns/abstraction-inversion)

## Types of Software

> Altouhgh some techniques and patterns are relevant for all kinds of software, many are relevant for only one particular branch.

### Enterprise Applications

* [EAPPs Challenges](enterprise/challenges)
* [Kinds of EAPPs](enterprise/kinds)

## Architectural Styles

> Recommended book: https://en.wikipedia.org/wiki/Pattern-Oriented_Software_Architecture

### General Concerns

* [Architecture](./architectures/general/definition)
* [Development Overconfidence](./architectures/general/overconfidence)
* [Developer Struggle](./architectures/general/developer-struggle)
* [Layering](architectures/general/layering)
* [Organizing Domain Logic](architectures/general/domain-logic)
* [Mapping to Relational Databases](architectures/general/mapping-to-rdbs)
* [Web Presentation](architectures/general/web-presentation)
* [Concurrency](architectures/general/concurrency)
* [Session State](architectures/general/session-state)
* [Distribution Strategies](architectures/general/distribution-strategies)

### Three-Layer System (Martin Fowler)

* [Three Fundamental Layers](architectures/fowler/three-layers)
* [Narratives summary](architectures/fowler/narratives)
* [Other layering schemes](architectures/fowler/other-layering-schemes)

### [Ports & Adapters / Hexagonal](./architectures/hexagonal)

### [Clean Architecture](./architectures/clean)

* [MVC and Hexagonal Architectures as Precursors](./architectures/clean/precursors)
* [MVC Problems](./architectures/clean/mvc)
* [Tradeoffs](./architectures/clean/tradeoffs)
* [What is Architecture](architectures/clean/architecture)
* [Keeping options open](architectures/clean/keeping-options)
* [Plugin Architecture: MCP](./architectures/clean/mcp)
* [Request and Response Models](architectures/clean/req-res)
* [Screaming Architecture](architectures/clean/screaming-architecture)
* [Testable Architecture](architectures/clean/testable-architecture)
* [Humble Object Pattern](architectures/clean/humble-object-pattern)
* [Services and boundaries](architectures/clean/services-boundaries)
* [Test Boundaries](architectures/clean/test-boundaries)
* [The Missing Advice](architectures/clean/missing-advice)

#### Clean Architecture - Glossary

* [Details](architectures/clean/details)
* [Stable Abstractions Rule](./architectures/clean/stable-abstractions)
* [Components](./architectures/clean/components)
  * [Concrete Components](architectures/clean/concrete-components)
* [Component Principles](architectures/clean/component-principles)
  * [Component Cohesion](architectures/clean/component-principles/component-cohesion)
    * [Reuse/Release Equivalence Principle](architectures/clean/component-principles/component-cohesion/rep)
    * [Common Closure Principle](architectures/clean/component-principles/component-cohesion/ccp)
    * [Common Reuse Principle](architectures/clean/component-principles/component-cohesion/crp)
  * [Component Coupling](architectures/clean/component-principles/component-coupling)
    * [Acyclic Dependencies Principle](architectures/clean/component-principles/component-coupling/adp)
    * [Stable Dependencies Principle](architectures/clean/component-principles/component-coupling/sdp)
    * [Stable Abstractions Principle](architectures/clean/component-principles/component-coupling/sap)
* [Stability](architectures/clean/stability)
* [Boundaries](./architectures/clean/boundaries)
* Objects
  * [Entities](architectures/clean/objects/entities)
  * [Use Cases](architectures/clean/objects/use-cases)
  * [Interactor](architectures/clean/objects/interactor)
  * [Interface Adapters](architectures/clean/objects/iadapters)
  * [Presenter and View](architectures/clean/objects/presenter-view)
  * [Database Gateways](architectures/clean/objects/database-gateways)
  * [Main Component](architectures/clean/objects/main)
* [Policy](architectures/clean/policy)
* [Business Rules](architectures/clean/business-rules)
* [Dependency Rule](architectures/clean/dependency-rule)
* [The Fragile Tests Problem](architectures/clean/fragile-tests)
* [Target Hardware Bottleneck](architectures/clean/target-hardware-bottleneck)
* Code organization
  * [Package by layer](architectures/clean/code-org/by-layers)
  * [Package by feature](architectures/clean/code-org/by-feature)
  * [Package by component](architectures/clean/code-org/by-component)

#### Clean Architecture - Extra material

* [Clean Architecture Essentials](https://dev.to/ivanpaulovich/clean-architecture-essentials-5a0m)

### REST: Representational State Transfer

* [Introduction](./architectures/rest/intro.md)
* [History](./architectures/rest/history.md)
* [Architectural Properties](./architectures/rest/properties.md)
* [Architectural Constraints](./architectures/rest/constraints.md)
* [Semantics of HTTP APIs](./architectures/rest/http-methods.md)

### [Flux](./architectures/flux)

* [MVC Comparison](architectures/flux/mvc-comparison)

### Micro Services

* [Micro services overview](architectures/microservices/overview)
* [Properties](architectures/microservices/properties)
* [Service granularity](architectures/microservices/granularity)
* [Benefits](architectures/microservices/benefits)
* [Criticism](architectures/microservices/issues)
* [Concerns](architectures/microservices/concerns)
* [Event Streaming Platform](architectures/microservices/event-stremaing-platform)

## System Design

> For a complete System Design study, you should also be familiar with Databases related topics such as CAP Theorem.

* [Introduction](system-design)
* [Where to start](system-design/how-to)
* [Performance Measures](system-design/performance-measures)
  * Response time
  * Responsiveness
  * Latency
  * Throughput
  * Load
  * Load sensitivity
  * Capacity
  * Scalability
* [Sustainability](system-design/sustainability)
* [Scalability](system-design/scalability)
  * [Vertical Scaling (scale up/down)](system-design/scalability/vertical-scaling)
  * [Horizontal Scaling (scale out/in)](system-design/scalability/horizontal-scaling)
* [Load Balancing](system-design/load-balancing)
* [Caching](system-design/caching)
* [RAID](system-design/raid)
* [Consistency](system-design/consistency)
* [Availability](system-design/availability)
  * Fail-over
  * Replication
* [Choosing a Database](system-design/choosing-database)
* [CDN: Content Delivery Network](system-design/cdn)
* [Stateless web tier](system-design/stateless-web-tier)
* [Multi-data center](system-design/multi-data-center) 
* [Message Queue](system-design/message-queue)
* [Logging, metrics, automation](system-design/logging-metrics-automation)
* [Scaling from zero to millions of users](system-design/from-zero-to-millions)
* [Back-of-the-envelope Estimation](system-design/estimation)
* [A Framework for System Design Interviews](system-design/interview-framework)
* Hashing
  * [The rehashing problem](system-design/hashing/rehashing-problem)
  * [Consistent hashing](system-design/hashing/consistent-hashing)

### Sources & Further Reading

* [Back of the envelope calculations](http://highscalability.com/blog/2011/1/26/google-pro-tip-use-back-of-the-envelope-calculations-to-choo.html)
* [How to ace a systems design interview](https://www.palantir.com/2011/10/how-to-rock-a-systems-design-interview/)
* [The system design interview](https://www.hiredintech.com/system-design)
* [Intro to Architecture and Systems Design Interviews](https://www.youtube.com/watch?v=ZgdS0EUmn70)
* [System design template](https://leetcode.com/discuss/career/229177/My-System-Design-Template)

### Case Studies

* [Instagram News Feed - Gaurav Sen](https://www.youtube.com/watch?v=fMZMm_0ZhK4)
* [Design a key-value store](system-design/case-studies/keyvalue-store)
* [Design a unique ID generator in distributed systems](system-design/case-studies/uniqueid-generator)
* [Design a URL shortener](system-design/case-studies/url-shortener)
* [Design a web crawler](system-design/case-studies/web-crawler)
* [Design a notification system](system-design/case-studies/notification-system)
* [Design a news feed system](system-design/case-studies/news-feed)
* [Design a chat system](system-design/case-studies/chat-system)

## Databases

* [CAP/Brewer's Theorem](databases/cap)
* [BASE](databases/base)
* [Object-oriented databases](databases/object-oriented)
* [Database Scaling](databases/scaling)
  * Vertical Scaling (Scaling Up)
  * Horizontal Scaling (Sharding)
* [Data Replication](databases/replication)
* [Data Partition](databases/partitioning)
* [Consistency Models](databases/consistency-models)
  * Strong Consistency vs Weak Consistency
  * Eventual Consistency
  * Strong Eventual Consistency (SEC)
* Synchronization techniques
  * [Quorum consensus](databases/quorum-consensus)
* Inconsistency resolution
  * [Versioning](databases/inconsistency-resolution/versioning)
* [Handling failures](databases/handling-failures)
  * Failure detection
    * All-to-all multicasting
    * Gossip protocol
  * Handling temporary failures
    * Sloppy quorum
    * Hinted handoff
  * Handling performance failures
    * Anti-entropy protocol
  * Handling data center outage

### Relational Databases

* [ACID](databases/relational/acid.md)
* [Transactions](databases/relational/transactions.md)
* [2PC Protocol / XA Transactions](databases/relational/2pc.md)
* [Views](databases/relational/view.md)
* [Joins](databases/relational/joins.md)
* Stored Procedures
* Indexing
* [ORM: Object-relational Mapping](databases/relational/orm)
* [Object-relational impedance mismatch](databases/relational/impedance-mismatch)

### Wide-column store

* [Overview](databases/wide-column)

#### HBase

* [Overview](databases/wide-column/hbase/overview)
* [Vs Relational Databases](databases/wide-column/hbase/vs-relational)
* [Architectural Components](databases/wide-column/hbase/architecture)
* [Write Mechanism](databases/wide-column/hbase/writes)
* [Interacting with Shell](databases/wide-column/hbase/shell)
* [ACID in HBase](https://hadoop-hbase.blogspot.com/2012/03/acid-in-hbase.html)
* [HBase Shell Interaction](databases/wide-column/hbase/shell)
* [HBase Interaction](https://www.youtube.com/watch?v=9YkurBN5Pt0)
* [HBase for Java Developers](https://www.youtube.com/playlist?list=PLf0swTFhTI8r6wUT9dcSQ-sLeaIMbbLm_)

## Distributed Systems

* Message Brokers
  * [Kafka](distributed/message-brokers/kafka)

## Technology specifics

Specifics that should be considered while developing a software solution relying on a particular technology.

### Javascript & Node.js

* [Considerations for a better architecture](./js/considerations.md)
* [AfterAcademy, backend architecture considerations](https://afteracademy.com/blog/design-node-js-backend-architecture-like-a-pro)
* [The Working Architecture, Viktor Turskyi](js/working-architecture)

### Golang

Check my [go-handbook repository](https://github.com/herrera-ignacio/go-handbook).

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

### Java

Check my [java-handbook repository](https://github.com/herrera-ignacio/java-handbook) that includes:

* Java Basics, OOP, Functional Programing
* JVM
* Java SE
* Maven
* Spring
* Sprint Boot
* Apache Kafka
* Apache Storm

## Operating Systems

* [Multithreading](./os/multithreading)
* [Parallelism & Concurrency](./os/parallelism)
* [Process & Thread](./os/process-thread)

## Models of Computation

* [Finite State Machine](/./models-of-computation/fsm)

## Data Science & Big Data

* [Batch Processing](ds/batch-processing)
* [ETL](ds/etl)

## Well-known Problems

* [The Revenue Recognition Problem](problems/revenue-recognition)

## Software Engineering Culture

* [Software Engineering at Google](swe/google-software-engineering)

## Glossary

### Common Terms

* [CRUD](glossary/crud)
* [Abstract Syntax Tree](glossary/ast)
* [Patterns](glossary/pattern)
* [Anti-Pattern](glossary/anti-pattern)
* [Micro Services Architecture](glossary/microservices)
* [Modularization](glossary/modularization)
* [Web API](glossary/web-api)
* [Leaky Abstraction](glossary/leaky-abstraction)
* [First-class citizen](glossary/first-class-citizen)
* [Side Effect](glossary/side-effect)
* [*SPOF*: Single Point of Failure](glossary/spof)

### Laws & Theorems

* [Hyrum's Law: The Law of Implicit Dependencies](glossary/laws/hyrum)
* [Churn Rule](glossary/laws/churn-rule)
* [Beyoncé Rule](glossary/laws/beyonce-rule)
