# Software Architect Handbook

- [Software Architect Handbook](#software-architect-handbook)
  - [Design Principles](#design-principles)
  - [Programming Paradigms](#programming-paradigms)
    - [Structured](#structured)
    - [OOP: Object Oriented Programming](#oop-object-oriented-programming)
    - [Functional](#functional)
  - [Design Patterns](#design-patterns)
    - [Base Patterns](#base-patterns)
    - [General / Architectural](#general--architectural)
    - [Gang of Four Patterns](#gang-of-four-patterns)
    - [Domain Logic](#domain-logic)
    - [Data Source & Persistence](#data-source--persistence)
    - [Object Relational](#object-relational)
      - [Behavioral](#behavioral)
      - [Structural](#structural)
      - [Metadata Mapping](#metadata-mapping)
    - [Web Presentation](#web-presentation)
    - [Distribution](#distribution)
    - [Offline Concurrency](#offline-concurrency)
    - [Session State](#session-state)
    - [Anti-Patterns](#anti-patterns)
  - [Types of Software](#types-of-software)
  - [System Design](#system-design)
    - [System Design - Case Studies](#system-design---case-studies)
  - [Architectural Styles](#architectural-styles)
    - [General Concerns](#general-concerns)
    - [Three-Layer System (Martin Fowler)](#three-layer-system-martin-fowler)
    - [Service Oriented Architecture (SOA)](#service-oriented-architecture-soa)
    - [Ports & Adapters / Hexagonal](#ports--adapters--hexagonal)
    - [Clean Architecture](#clean-architecture)
    - [REST: Representational State Transfer](#rest-representational-state-transfer)
    - [Flux](#flux)
    - [Domain-Driven Design](#domain-driven-design)
    - [Microservices](#microservices)
  - [Databases](#databases)
    - [Relational Databases](#relational-databases)
    - [Wide-column store](#wide-column-store)
  - [Technology specifics](#technology-specifics)
  - [Operating Systems](#operating-systems)
  - [Data Science & Big Data](#data-science--big-data)
  - [Software Engineering Culture](#software-engineering-culture)
  - [Useful Tools](#useful-tools)
  - [Glossary](#glossary)

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

## Design Patterns

> [What is a design pattern?](https://github.com/herrera-ignacio/design_patterns/blob/master/introduction/design-pattern.md)

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

### Anti-Patterns

* [Abstraction Inversion](anti-patterns/abstraction-inversion)

## Types of Software

> Altouhgh some techniques and patterns are relevant for all kinds of software, many are relevant for only one particular branch.

* Enterprise Applications
  * [EAPPs Challenges](enterprise/challenges)
  * [Kinds of EAPPs](enterprise/kinds)


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
* [Message Queue/Message Broker](system-design/message-queue)
  * [Kafka](system-design/message-queue/kafka)
* [Logging, metrics, automation](system-design/logging-metrics-automation)
* [Scaling from zero to millions of users](system-design/from-zero-to-millions)
* [Back-of-the-envelope Estimation](system-design/estimation)
* [A Framework for System Design Interviews](system-design/interview-framework)
* Hashing
  * [The rehashing problem](system-design/hashing/rehashing-problem)
  * [Consistent hashing](system-design/hashing/consistent-hashing)

### System Design - Case Studies

* [Instagram News Feed - Gaurav Sen](https://www.youtube.com/watch?v=fMZMm_0ZhK4)
* [Design a key-value store](system-design/case-studies/keyvalue-store)
* [Design a unique ID generator in distributed systems](system-design/case-studies/uniqueid-generator)
* [Design a URL shortener](system-design/case-studies/url-shortener)
* [Design a web crawler](system-design/case-studies/web-crawler)
* [Design a notification system](system-design/case-studies/notification-systevm)
* [Design a news feed system](system-design/case-studies/news-feed)
* [Design a chat system](system-design/case-studies/chat-system)
* [Design a Search Autocomplete System](system-design/case-studies/search-autocomplete)
* [Design Youtube](system-design/case-studies/youtube)
* [Design Google Drive](system-design/case-studies/google-drive)

## Architectural Styles

> Recommended book: https://en.wikipedia.org/wiki/Pattern-Oriented_Software_Architecture

### General Concerns

* [Architecture](architectures/general/definition)
* [Concurrency](architectures/general/concurrency)
* [Development Overconfidence](architectures/general/overconfidence)
* [Developer Struggle](architectures/general/developer-struggle)
* [Distribution Strategies](architectures/general/distribution-strategies)
* [Layering](architectures/general/layering)
* [Mapping to Relational Databases](architectures/general/mapping-to-rdbs)
* [Organizing Domain Logic](architectures/general/domain-logic)
* [Session State](architectures/general/session-state)
* [Web Presentation](architectures/general/web-presentation)

### Three-Layer System (Martin Fowler)

* [Three Fundamental Layers](architectures/fowler/three-layers)
* [Narratives summary](architectures/fowler/narratives)
* [Other layering schemes](architectures/fowler/other-layering-schemes)

### [Service Oriented Architecture (SOA)](architectures/soa)

### [Ports & Adapters / Hexagonal](architectures/hexagonal)

### [Clean Architecture](architectures/clean)

* [MVC and Hexagonal Architectures as Precursors](architectures/clean/precursors)
* [MVC Problems](architectures/clean/mvc)
* [Tradeoffs](architectures/clean/tradeoffs)
* [What is Architecture](architectures/clean/architecture)
* [Keeping options open](architectures/clean/keeping-options)
* [Plugin Architecture: MCP](architectures/clean/mcp)
* [Request and Response Models](architectures/clean/req-res)
* [Screaming Architecture](architectures/clean/screaming-architecture)
* [Testable Architecture](architectures/clean/testable-architecture)
* [Humble Object Pattern](architectures/clean/humble-object-pattern)
* [Services and boundaries](architectures/clean/services-boundaries)
* [Test Boundaries](architectures/clean/test-boundaries)
* [The Fragile Tests Problem](architectures/clean/fragile-tests)
* Code organization
  * [Package by layer](architectures/clean/code-org/by-layers)
  * [Package by feature](architectures/clean/code-org/by-feature)
  * [Package by component](architectures/clean/code-org/by-component)
* [Target Hardware Bottleneck](architectures/clean/target-hardware-bottleneck)
* [The Missing Advice](architectures/clean/missing-advice)
* Glossary
  * [Details](architectures/clean/details)
  * [Stable Abstractions Rule](architectures/clean/stable-abstractions)
  * [Components](architectures/clean/components)
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
  * [Boundaries](architectures/clean/boundaries)
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

### REST: Representational State Transfer

* [Introduction](architectures/rest/intro.md)
* [History](architectures/rest/history.md)
* [Architectural Properties](architectures/rest/properties.md)
* [Architectural Constraints](architectures/rest/constraints.md)
* [Semantics of HTTP APIs](architectures/rest/http-methods.md)

### [Flux](architectures/flux)

* [MVC Comparison](architectures/flux/mvc-comparison)

### Domain-Driven Design

> [Overview](architectures/ddd/overview)

* [Aggregate](architectures/ddd/aggregate)
* [Bounded Context](architectures/ddd/bounded-context)

### Microservices

> [Overview](architectures/microservices/overview)

* [Benefits and alternatives](architectures/microservices/benefits)
* [Coupling and Cohesion](architectures/microservices/coupling-and-cohesion)
* [Own their data](architectures/microservices/own-data)
* [DDD - Mapping aggregates and bounded contexts](architectures/microservices/ddd-mapping)
* [Monolith](architectures/microservices/monolith)
* [Planning a Migration](architectures/microservices/migration)
* [Splitting the Monolith](architectures/microservices/splitting-monolith)
  * [Strangler Fig Application](architectures/microservices/splitting-monolith/strangler-fig)
  * [UI Composition](architectures/microservices/splitting-monolith/ui-composition)
  * [Branch by Abstraction](architectures/microservices/splitting-monolith/branch-by-abstraction)
  * [Parallel Run](architectures/microservices/splitting-monolith/parallel-run)
  * [Decorating Collaborator](architectures/microservices/splitting-monolith/decorating-collaborator)
  * [Change Data Capture](architectures/microservices/splitting-monolith/change-data-capture)
* [Decomposing the Database](architectures/microservices/decomposing-database)
  * [Shared Database](architectures/microservices/decomposing-database/shared-database)
  * [Database View](architectures/microservices/decomposing-database/database-view)
  * [Database Wrapping Service](architectures/microservices/decomposing-database/database-wrapping-service)
  * [Database-as-a-Service Interface](architectures/microservices/decomposing-database/das-interface)
  * [Aggregate Exposing Monolith](architectures/microservices/decomposing-database/aggregate-exposing-monolith)
  * [Change Data Ownership](architectures/microservices/decomposing-database/change-data-ownership)
  * [Synchronize Data in Application](architectures/microservices/decomposing-database/synchronize-data-in-application)
  * [Tracer Write](architectures/microservices/decomposing-database/tracer-write)
* [Splitting Apart the Database](architectures/microservices/splitting-apart-database)
  * Split the Database First
    * [Repository per Bounded Context](architectures/microservices/splitting-apart-database/repository-per-bounded-context)
    * [Database per Bounded Context](architectures/microservices/splitting-apart-database/databas-per-bounded-context)
  * Split the Code First
    * [Monolith as Data Access Layer](architectures/microservices/splitting-apart-database/monolith-as-dal)
* [Trade-Offs](architectures/microservices/tradeoffs)
* [When to avoid](architectures/microservices/when-to-avoid)

> [Tools](architectures/microservices/tooling)

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
* HBase
  * [Overview](databases/wide-column/hbase/overview)
  * [Vs Relational Databases](databases/wide-column/hbase/vs-relational)
  * [Architectural Components](databases/wide-column/hbase/architecture)
  * [Write Mechanism](databases/wide-column/hbase/writes)
  * [Interacting with Shell](databases/wide-column/hbase/shell)
  * [ACID in HBase](https://hadoop-hbase.blogspot.com/2012/03/acid-in-hbase.html)
  * [HBase Shell Interaction](databases/wide-column/hbase/shell)
  * [HBase Interaction](https://www.youtube.com/watch?v=9YkurBN5Pt0)
  * [HBase for Java Developers](https://www.youtube.com/playlist?list=PLf0swTFhTI8r6wUT9dcSQ-sLeaIMbbLm_)


## Technology specifics

Specifics that should be considered while developing a software solution relying on a particular technology.

* [Golang Handbook](https://github.com/herrera-ignacio/go-handbook)
* [Java Handbook](https://github.com/herrera-ignacio/java-handbook)
* [JS Handbook](https://github.com/herrera-ignacio/js-handbook)
* React
  * [Thinking in React](https://reactjs.org/docs/thinking-in-react.html)
* Redux
  * [When and when not to reach for Redux](redux/when)
  * [Redux must know](redux/introduction)
  * [Three Fundamental Principles](redux/three-principles)
  * [Best Practices](redux/best-practices)
  * [Reducers: Immutable Update Patterns](redux/immutable-updates)
  * [Redux Ecosystem Links](https://github.com/markerikson/redux-ecosystem-links)
  * [Flux Comparison](redux/flux-comparison)
  * [MVC Comparison](https://blog.gisspan.com/2017/02/Redux-Vs-MVC,-Why-and-How.html)

## Operating Systems

* [Multithreading](os/multithreading)
* [Parallelism & Concurrency](os/parallelism)
* [Process & Thread](os/process-thread)
* Models of Computation
  * [Finite State Machine](models-of-computation/fsm)

## Data Science & Big Data

* [Batch Processing](ds/batch-processing)
* [ETL](ds/etl)

## Software Engineering Culture

* [Software Engineering at Google](swe/google-software-engineering)
* [Success stories](swe/success-stories)
* [Laws & Theorems](swe/laws)
* [Quotes](swe/quotes.md)

## Useful Tools

* [Telepresence](https://telepresence.io): tool that is aiming to make a hybrid local/remote developer workflow easier for Kubernetes users.
* [Pact](https://pact.io): customer-driven contracts.

## Glossary

  * [Abstract Syntax Tree](glossary/ast)
  * [Anti-Pattern](glossary/anti-pattern)
  * [CRUD](glossary/crud)
  * [First-class citizen](glossary/first-class-citizen)
  * [Leaky Abstraction](glossary/leaky-abstraction)
  * [Micro Services Architecture](glossary/microservices)
  * [Modularization](glossary/modularization)
  * [Patterns](glossary/pattern)
  * [Resilience vs Robustness](glossary/resilience-vs-robustness)
  * [Side Effect](glossary/side-effect)
  * [SPOF: Single Point of Failure](glossary/spof)
  * [Web API](glossary/web-api)
