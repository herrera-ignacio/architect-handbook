# Software Architect Handbook

__UPDATE!__: I will be updating this repository with a new structure that better supports [Obsidian](https://obsidian.md/).
This README won't be updated anymore and it will reference content from the `/legacy` folder.
I'll iteratively move new versions of such content (and new stuff!) to [./READMEv2.md](./READMEv2.md) which will eventually become the main README and can be opened with Obsidian for better navigation.

> [What is software architecture?](./legacy/architectures/general/definition/README.md)

<!-- TOC -->
- [Software Architect Handbook](#software-architect-handbook)
  - [System design](#system-design)
    - [System Design - Case Studies](#system-design---case-studies)
  - [Design principles](#design-principles)
  - [Design patterns](#design-patterns)
    - [Base patterns](#base-patterns)
    - [System-level or architectural patterns](#system-level-or-architectural-patterns)
    - [Gang of Four Patterns](#gang-of-four-patterns)
    - [Domain logic patterns](#domain-logic-patterns)
    - [Data source \& persistence patterns](#data-source--persistence-patterns)
    - [Object relational patterns](#object-relational-patterns)
      - [Behavioral patterns](#behavioral-patterns)
      - [Structural patterns](#structural-patterns)
      - [Metadata mapping patterns](#metadata-mapping-patterns)
    - [Web presentation patterns](#web-presentation-patterns)
    - [Distribution patterns](#distribution-patterns)
    - [Offline concurrency patterns](#offline-concurrency-patterns)
    - [Session state patterns](#session-state-patterns)
    - [Anti-Patterns](#anti-patterns)
  - [Architectural Styles \& Patterns](#architectural-styles--patterns)
    - [Three-Layer System (Martin Fowler)](#three-layer-system-martin-fowler)
    - [Service Oriented Architecture (SOA)](#service-oriented-architecture-soa)
    - [Ports \& Adapters / Hexagonal](#ports--adapters--hexagonal)
    - [Clean Architecture](#clean-architecture)
    - [REST: Representational State Transfer](#rest-representational-state-transfer)
    - [Flux \& Redux](#flux--redux)
    - [Domain-Driven Design](#domain-driven-design)
    - [Microservices](#microservices)
  - [Data storage](#data-storage)
    - [General concepts](#general-concepts)
      - [Data Consistency](#data-consistency)
      - [Data partitioning](#data-partitioning)
    - [Types](#types)
      - [Relational Databases](#relational-databases)
      - [Wide-column store](#wide-column-store)
      - [GraphQL](#graphql)
  - [Software types](#software-types)
  - [Operating systems](#operating-systems)
    - [Linux](#linux)
  - [Refactoring \& code smells](#refactoring--code-smells)
  - [Programming paradigms](#programming-paradigms)
    - [Structured programming](#structured-programming)
    - [OOP: Object-oriented programming](#oop-object-oriented-programming)
    - [Functional programming](#functional-programming)
  - [Software Engineering Culture](#software-engineering-culture)
    - [Laws \& Theorems](#laws--theorems)
    - [Working Methodologies](#working-methodologies)
  - [Testing](#testing)
    - [E2E Testing](#e2e-testing)
  - [General concepts](#general-concepts-1)
    - [About system-design and architecture](#about-system-design-and-architecture)
    - [About software engineering](#about-software-engineering)
    - [Common jargon](#common-jargon)
  - [Tooling - Language Agnostic](#tooling---language-agnostic)
  - [Technology specifics](#technology-specifics)
    - [Frontend](#frontend)
<!-- TOC -->

## System design

> For a complete System Design study, you should also be familiar with Databases related topics such as CAP Theorem. This section assumes prior knowledge about such topics, but you can also read about those in this very same repo.

- [Introduction](./legacy/system-design/README.md)
- [How to approach a design](./legacy/system-design/how-to)
- [Performance Measures](./legacy/system-design/performance-measures)
  - Response time
  - Responsiveness
  - Latency
  - Throughput
  - Load
  - Load sensitivity
  - Capacity
  - Scalability
- [Load Balancing](./legacy/system-design/load-balancing)
- [Sustainability](./legacy/system-design/sustainability)
- [Scalability](./legacy/system-design/scalability)
  - [Vertical Scaling (scale up/down)](./legacy/system-design/scalability/vertical-scaling)
  - [Horizontal Scaling (scale out/in)](./legacy/system-design/scalability/horizontal-scaling)
- [Caching](./legacy/system-design/caching)
- [RAID](./legacy/system-design/raid)
- [Consistency](./legacy/system-design/consistency)
- [Availability](./legacy/system-design/availability)
  - Fail-over
  - Replication
- [Choosing a Database](./legacy/system-design/choosing-database)
- [CDN: Content Delivery Network](./legacy/system-design/cdn)
- [Stateless web tier](./legacy/system-design/stateless-web-tier)
- [Multi-data center](./legacy/system-design/multi-data-center)
- [Message Queue/Message Broker](./legacy/system-design/message-queue)
  - [Kafka](./legacy/system-design/message-queue/kafka)
- [Logging, metrics, automation](./legacy/system-design/logging-metrics-automation)
- [Scaling from zero to millions of users](./legacy/system-design/from-zero-to-millions)
- [Back-of-the-envelope Estimation](./legacy/system-design/estimation)
- [A Framework for System Design Interviews](./legacy/system-design/interview-framework)
- Hashing
  - [The rehashing problem](./legacy/system-design/hashing/rehashing-problem)
  - [Consistent hashing](./legacy/system-design/hashing/consistent-hashing)

### System Design - Case Studies

| Problems                                   | Solutions                                                   |
|--------------------------------------------|-------------------------------------------------------------|
| Instagram News Feed - Gaurav Sen           | [Solution](https://www.youtube.com/watch?v=fMZMm_0ZhK4)     |
| Key-value store                            | [Solution](./legacy/system-design/case-studies/keyvalue-store)       |
| Unique ID generator in distributed systems | [Solution](./legacy/system-design/case-studies/uniqueid-generator)   |
| URL shortener                              | [Solution](./legacy/system-design/case-studies/url-shortener)        |
| Web crawler                                | [Solution](./legacy/system-design/case-studies/web-crawler)          |
| Notification system                        | [Solution](./legacy/system-design/case-studies/notification-systevm) |
| News feed system                           | [Solution](./legacy/system-design/case-studies/news-feed)            |
| Chat system                                | [Solution](./legacy/system-design/case-studies/chat-system)          |
| Search autocomplete system                 | [Solution](./legacy/system-design/case-studies/search-autocomplete)  |
| Youtube                                    | [Solution](./legacy/system-design/case-studies/youtube)              |
| Google Drive                               | [Solution](./legacy/system-design/case-studies/google-drive)         |

## Design principles

- [Common Architectural Principles](./legacy/principles/general)
- [OO Design Principles](https://wiki.c2.com/?PrinciplesOfObjectOrientedDesign)
  - [Encapsulate what varies](./legacy/principles/oo/encapsulate.md)
  - [Program to an interface, not an implementation](./legacy/principles/oo/favor-interfaces.md)
  - [Favor object composition over class inheritance](./legacy/principles/oo/favor-composition.md)
  - [Strive for loosely coupled designs between objects that interact](./legacy/principles/oo/loosely-coupled-interaction.md)
  - [Least Knowledge](./legacy/principles/oo/least-knowledge.md)
- DRY
- [GRASP](./legacy/principles/grasp.md)
- [Hollywood Principle](./legacy/principles/hollywood.md)
- [SOLID](./legacy/principles/solid)
  - [Single Responsibility Principle](./legacy/principles/solid/srp)
  - [Open Closed Principle](./legacy/principles/solid/ocp)
  - [Liskov Substitution Principle](./legacy/principles/solid/lsp)
  - [Interface Segregation Principle](./legacy/principles/solid/isp)
  - [Dependency Inversion Principle](./legacy/principles/solid/dip)
- [KISS](./legacy/principles/kiss.md)
- [WET](https://dev.to/wuz/stop-trying-to-be-so-dry-instead-write-everything-twice-wet-5g33)
- [YAGNI](./legacy/principles/yagni.md)

## Design patterns

> [What is a design pattern?](./legacy/glossary/pattern)

### Base patterns

- [Gateway](./legacy/design-patterns/base/gateway)
- [Mapper](./legacy/design-patterns/base/mapper)
- [Layer Supertype](./legacy/design-patterns/base/layer-supertype)
- [Separated Interface](./legacy/design-patterns/base/separated-interface)
- [Registry](./legacy/design-patterns/base/registry)
- [Value Object](./legacy/design-patterns/base/value-object)
  - [Money](./legacy/design-patterns/base/value-object/money)
- [Special Case](./legacy/design-patterns/base/special-case)
- [Plugin](./legacy/design-patterns/base/plugin)
- [Service Stub](./legacy/design-patterns/base/service-stub)
- [Record Set](./legacy/design-patterns/base/record-set)

### System-level or architectural patterns

- [Event Sourcing](./legacy/design-patterns/architectural/event-sourcing.md)
- [CQRS: Command and Query Responsibility Segregation](./legacy/design-patterns/architectural/cqrs.md)
- [Saga: distributed transactions](./legacy/design-patterns/architectural/saga.md)

### Gang of Four Patterns

Please check the [this repository](https://github.com/herrera-ignacio/design_patterns/) for a detailed explanation and examples of each of the following patterns.

| [Creational](https://github.com/herrera-ignacio/design_patterns/tree/master/creational) | [Structural](https://github.com/herrera-ignacio/design_patterns/tree/master/structural) | [Behavioral](https://github.com/herrera-ignacio/design_patterns/tree/master/structural/behavioral-patterns) |
|------------------ |------------ |------------ |
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

### Domain logic patterns

- [Transaction Script](./legacy/design-patterns/domain-logic/transaction-script)
- [Domain Model](./legacy/design-patterns/domain-logic/domain-model)
- [Table Module](./legacy/design-patterns/domain-logic/table-module)
- [Service Layer](./legacy/design-patterns/domain-logic/service-layer)

### Data source & persistence patterns

- [DAO: Data Access Object](./legacy/design-patterns/data/dao)
- [Active Record](./legacy/design-patterns/data/active-record)
- [Data Mapper](./legacy/design-patterns/data/data-mapper)
- [Table Data Gateway](./legacy/design-patterns/data/table-data-gateway)
- [Row Data Gateway](./legacy/design-patterns/data/row-data-gateway)
- [Repository](./legacy/design-patterns/data/repository)

### Object relational patterns

#### Behavioral patterns

- [Unit of Work](./legacy/design-patterns/object-relational/behavioral/unit-of-work)
- [Identity Map](./legacy/design-patterns/object-relational/behavioral/identity-map)
- [Lazy Load](./legacy/design-patterns/object-relational/behavioral/lazy-load)

#### Structural patterns

- [Identity Field](./legacy/design-patterns/object-relational/structural/identity-field)
- [Foreign Key Mapping](./legacy/design-patterns/object-relational/structural/foreign-key-mapping)
- [Association Table Mapping](./legacy/design-patterns/object-relational/structural/association-table-mapping)
- [Dependent Mapping](./legacy/design-patterns/object-relational/structural/dependent-mapping)
- [Embedded Value / Aggregate Mapping](./legacy/design-patterns/object-relational/structural/embedded-value)
- [Serializd LOB](./legacy/design-patterns/object-relational/structural/serialized-lob)
- [Single Table Inheritance](./legacy/design-patterns/object-relational/structural/single-table-inheritance)
- [Class Table Inheritance / Root-Leaf Mapping](./legacy/design-patterns/object-relational/structural/class-table-inheritance)
- [Concrete Table Inheritance](./legacy/design-patterns/object-relational/structural/concrete-table-inheritance)
- [Inheritance Mappers](./legacy/design-patterns/object-relational/structural/inheritance-mappers)

#### Metadata mapping patterns

- [Metadata Mapping](./legacy/design-patterns/object-relational/metadata-mapping/metadata-mapping)
- [Query Object](./legacy/design-patterns/object-relational/metadata-mapping/query-object)
- [Repository](./legacy/design-patterns/object-relational/metadata-mapping/repository)

### Web presentation patterns

> [What are web presentation patterns?](./legacy/architectures/general/web-presentation)

- [Application Model / Presentation Model](./legacy/design-patterns/web-presentation/presentation-model)
- [Humble View / Passive View](./legacy/design-patterns/web-presentation/passive-view)
- [MVC: Model View Controller](./legacy/design-patterns/web-presentation/mvc)
- [MVP: Model View Presenter](./legacy/design-patterns/web-presentation/mvp)
- [MVVM: Model View View-Model](./legacy/design-patterns/web-presentation/mvvm)
- [Front Controller](./legacy/design-patterns/web-presentation/front-controller)
- [Page Controller](./legacy/design-patterns/web-presentation/page-controller)
- [Supervising Controller](./legacy/design-patterns/web-presentation/supervising-controller)
- [Template View](./legacy/design-patterns/web-presentation/template-view)
- [Transform View](./legacy/design-patterns/web-presentation/transform-view)
- [Two Step View](./legacy/design-patterns/web-presentation/two-step-view)

### Distribution patterns

- [Remote Facade](./legacy/design-patterns/distribution/remote-facade)
- [Data Transfer Object](./legacy/design-patterns/distribution/dto)

### Offline concurrency patterns

- [Optimistic Offline Lock](./legacy/design-patterns/offline-concurrency/optimistic-offline-lock)
- [Pessimistic Offline Lock](./legacy/design-patterns/offline-concurrency/pessimistic-offline-lock)
- [Coarse-Grained Lock](./legacy/design-patterns/offline-concurrency/coarse-grained-lock)

### Session state patterns

- [Client Session State](./legacy/design-patterns/session-state/client)
- [Server Session State](./legacy/design-patterns/session-state/server)
- [Database Session State](./legacy/design-patterns/session-state/database)

### Anti-Patterns

> [What is an Anti-Pattern?](./legacy/glossary/anti-pattern)

- [Abstraction Inversion](./legacy/anti-patterns/abstraction-inversion)

## Architectural Styles & Patterns

> Recommended book: <https://en.wikipedia.org/wiki/Pattern-Oriented_Software_Architecture>

### Three-Layer System (Martin Fowler)

- [Three Fundamental Layers](./legacy/architectures/fowler/three-layers)
- [Narratives summary](./legacy/architectures/fowler/narratives)
- [Other layering schemes](./legacy/architectures/fowler/other-layering-schemes)

### [Service Oriented Architecture (SOA)](./legacy/architectures/soa)

### [Ports & Adapters / Hexagonal](./legacy/architectures/hexagonal)

### [Clean Architecture](./legacy/architectures/clean)

- [MVC and Hexagonal Architectures as Precursors](./legacy/architectures/clean/precursors)
- [MVC Problems](./legacy/architectures/clean/mvc)
- [Tradeoffs](./legacy/architectures/clean/tradeoffs)
- [What is Architecture](./legacy/architectures/clean/architecture)
- [Keeping options open](./legacy/architectures/clean/keeping-options)
- [Plugin Architecture - Model Controller Presenter (MCP)](./legacy/architectures/clean/mcp)
- [Request and Response Models](./legacy/architectures/clean/req-res)
- [Screaming Architecture](./legacy/architectures/clean/screaming-architecture)
- [Testable Architecture](./legacy/architectures/clean/testable-architecture)
- [Humble Object Pattern](./legacy/architectures/clean/humble-object-pattern)
- [Services and boundaries](./legacy/architectures/clean/services-boundaries)
- [Test Boundaries](./legacy/architectures/clean/test-boundaries)
- [The Fragile Tests Problem](./legacy/architectures/clean/fragile-tests)
- Code organization
  - [Package by layer](./legacy/architectures/clean/code-org/by-layers)
  - [Package by feature](./legacy/architectures/clean/code-org/by-feature)
  - [Package by component](./legacy/architectures/clean/code-org/by-component)
- [Target Hardware Bottleneck](./legacy/architectures/clean/target-hardware-bottleneck)
- [The Missing Advice](./legacy/architectures/clean/missing-advice)
- Glossary
  - [Details](./legacy/architectures/clean/details)
  - [Stable Abstractions Rule](./legacy/architectures/clean/stable-abstractions)
  - [Components](./legacy/architectures/clean/components)
    - [Concrete Components](./legacy/architectures/clean/concrete-components)
    - [Component Principles](./legacy/architectures/clean/component-principles)
      - [Component Cohesion](./legacy/architectures/clean/component-principles/component-cohesion)
        - [Reuse/Release Equivalence Principle](./legacy/architectures/clean/component-principles/component-cohesion/rep)
        - [Common Closure Principle](./legacy/architectures/clean/component-principles/component-cohesion/ccp)
        - [Common Reuse Principle](./legacy/architectures/clean/component-principles/component-cohesion/crp)
      - [Component Coupling](./legacy/architectures/clean/component-principles/component-coupling)
        - [Acyclic Dependencies Principle](./legacy/architectures/clean/component-principles/component-coupling/adp)
        - [Stable Dependencies Principle](./legacy/architectures/clean/component-principles/component-coupling/sdp)
        - [Stable Abstractions Principle](./legacy/architectures/clean/component-principles/component-coupling/sap)
  - [Stability](./legacy/architectures/clean/stability)
  - [Boundaries](./legacy/architectures/clean/boundaries)
  - Objects
    - [Entities](./legacy/architectures/clean/objects/entities)
    - [Use Cases](./legacy/architectures/clean/objects/use-cases)
    - [Interactor](./legacy/architectures/clean/objects/interactor)
    - [Interface Adapters](./legacy/architectures/clean/objects/iadapters)
    - [Presenter and View](./legacy/architectures/clean/objects/presenter-view)
    - [Database Gateways](./legacy/architectures/clean/objects/database-gateways)
    - [Main Component](./legacy/architectures/clean/objects/main)
  - [Policy](./legacy/architectures/clean/policy)
  - [Business Rules](./legacy/architectures/clean/business-rules)
  - [Dependency Rule](./legacy/architectures/clean/dependency-rule)

### REST: Representational State Transfer

> [Recommended reference: restfulapi.net](https://restfulapi.net/)

- [Introduction](./legacy/architectures/rest/intro.md)
- [History](./legacy/architectures/rest/history.md)
- [Architectural Properties](./legacy/architectures/rest/properties.md)
  - [Stateless vs Stateful](./legacy/architectures/rest/stateless.md)
- [Architectural Constraints](./legacy/architectures/rest/constraints.md)
- [Five key principles](https://www.infoq.com/articles/rest-introduction/)
- [Semantics of HTTP APIs](./legacy/architectures/rest/http-methods.md)

### [Flux & Redux](./legacy/architectures/flux)

- [What the flux?! Let's Redux](https://blog.andyet.com/2015/08/06/what-the-flux-lets-redux/)
- [Facebook's MVC Comparison](./legacy/architectures/flux/mvc-comparison)

### Domain-Driven Design

> [Overview](./legacy/architectures/ddd/overview)

- [Aggregate](./legacy/architectures/ddd/aggregate)
- [Bounded Context](./legacy/architectures/ddd/bounded-context)

### Microservices

> [Overview](./legacy/architectures/microservices/overview)

- [Benefits and alternatives](./legacy/architectures/microservices/benefits)
- [Coupling and Cohesion](./legacy/architectures/microservices/coupling-and-cohesion)
- [Own their data](./legacy/architectures/microservices/own-data)
- [DDD - Mapping aggregates and bounded contexts](./legacy/architectures/microservices/ddd-mapping)
- [Monolith](./legacy/architectures/microservices/monolith)
- [Planning a Migration](./legacy/architectures/microservices/migration)
- [Splitting the Monolith](./legacy/architectures/microservices/splitting-monolith)
  - [Strangler Fig Application](./legacy/architectures/microservices/splitting-monolith/strangler-fig)
  - [UI Composition](./legacy/architectures/microservices/splitting-monolith/ui-composition)
  - [Branch by Abstraction](./legacy/architectures/microservices/splitting-monolith/branch-by-abstraction)
  - [Parallel Run](./legacy/architectures/microservices/splitting-monolith/parallel-run)
  - [Decorating Collaborator](./legacy/architectures/microservices/splitting-monolith/decorating-collaborator)
  - [Change Data Capture](./legacy/architectures/microservices/splitting-monolith/change-data-capture)
- [Decomposing the Database](./legacy/architectures/microservices/decomposing-database)
  - [Shared Database](./legacy/architectures/microservices/decomposing-database/shared-database)
  - [Database View](./legacy/architectures/microservices/decomposing-database/database-view)
  - [Database Wrapping Service](./legacy/architectures/microservices/decomposing-database/database-wrapping-service)
  - [Database-as-a-Service Interface](./legacy/architectures/microservices/decomposing-database/das-interface)
  - [Aggregate Exposing Monolith](./legacy/architectures/microservices/decomposing-database/aggregate-exposing-monolith)
  - [Change Data Ownership](./legacy/architectures/microservices/decomposing-database/change-data-ownership)
  - [Synchronize Data in Application](./legacy/architectures/microservices/decomposing-database/synchronize-data-in-application)
  - [Tracer Write](./legacy/architectures/microservices/decomposing-database/tracer-write)
- [Splitting Apart the Database](./legacy/architectures/microservices/splitting-apart-database)
  - Split the Database First
    - [Repository per Bounded Context](./legacy/architectures/microservices/splitting-apart-database/repository-per-bounded-context)
    - [Database per Bounded Context](./legacy/architectures/microservices/splitting-apart-database/databas-per-bounded-context)
  - Split the Code First
    - [Monolith as Data Access Layer](./legacy/architectures/microservices/splitting-apart-database/monolith-as-dal)
    - [Multischema Storage](./legacy/architectures/microservices/splitting-apart-database/multischema-storage)
  - Schema Separation
    - [Split Table](./legacy/architectures/microservices/splitting-apart-database/split-table)
    - [Move Foreign-Key Relationship to Code](./legacy/architectures/microservices/splitting-apart-database/move-fk-to-code)
  - [Shared Static Data](./legacy/architectures/microservices/splitting-apart-database/shared-static-data)
  - [Dealing with Transactions](./legacy/architectures/microservices/splitting-apart-database/transactions)
    - [Sagas](./legacy/architectures/microservices/splitting-apart-database/transactions/sagas)
- [Growing Pains](./legacy/architectures/microservices/growing-pains)
- [Trade-Offs](./legacy/architectures/microservices/tradeoffs)
- [When to avoid](./legacy/architectures/microservices/when-to-avoid)

> [Tools](./legacy/architectures/microservices/tooling)

## Data storage

- [CAP/Brewer's Theorem](./legacy/databases/cap)
- [BASE](./legacy/databases/base)
- [Object-oriented databases](./legacy/databases/object-oriented)
- [Database Scaling](./legacy/databases/scaling)
  - Vertical Scaling (Scaling Up)
  - Horizontal Scaling (Sharding)
- [Data Replication](./legacy/databases/replication)
- [Consistency Models](./legacy/databases/consistency-models)
  - Strong Consistency vs Weak Consistency
  - Eventual Consistency
  - Strong Eventual Consistency (SEC)
- Synchronization techniques
  - [Quorum consensus](./legacy/databases/quorum-consensus)
- [Handling failures](./legacy/databases/handling-failures)
  - Failure detection
    - All-to-all multicasting
    - Gossip protocol
  - Handling temporary failures
    - Sloppy quorum
    - Hinted handoff
  - Handling performance failures
    - Anti-entropy protocol
  - Handling data center outage

### General concepts

#### Data Consistency

- [Data consistency primer](./legacy/databases/consistency/README.md)
- [Strong consistency](./legacy/databases/consistency/strong.md)
- [Eventual consistency](./legacy/databases/consistency/eventual.md)
- Inconsistency resolution
  - [Versioning](./legacy/databases/inconsistency-resolution/versioning)

#### Data partitioning

- [Data partitionioning primer](./legacy/databases/partitioning/README.md)
- [Horizontal partitioning (_sharding_)](./legacy/databases/partitioning/horizontal.md)
  - [Consistent hashing](./legacy/databases/partitioning/consistent-hashing.md)
- [Vertical partitioning](./legacy/databases/partitioning/vertical.md)
- [Fuctional partitioning](./legacy/databases/partitioning/functional.md)

### Types

#### Relational Databases

- [ACID](./legacy/databases/relational/acid/README.md): Atomicity, Consistency, Isolation, Durability
- [Isolation Levels](./legacy/databases/relational/isolation-levels/README.md)
- [Transactions](./legacy/databases/relational/transactions.md)
- [Read Phenomena](./legacy/databases/relational/read-phenomena/README.md)
- [2PC Protocol / XA Transactions](./legacy/databases/relational/2pc.md)
- [Views](./legacy/databases/relational/view.md)
- [Joins](./legacy/databases/relational/joins.md)
- Stored Procedures
- Indexing
- [ORM: Object-relational Mapping](./legacy/databases/relational/orm)
- [Object-relational impedance mismatch](./legacy/databases/relational/impedance-mismatch)

#### Wide-column store

- [Overview](./legacy/databases/wide-column)
- HBase
  - [Overview](./legacy/databases/wide-column/hbase/overview)
  - [Vs Relational Databases](./legacy/databases/wide-column/hbase/vs-relational)
  - [Architectural Components](./legacy/databases/wide-column/hbase/architecture)
  - [Write Mechanism](./legacy/databases/wide-column/hbase/writes)
  - [Interacting with Shell](./legacy/databases/wide-column/hbase/shell)
  - [ACID in HBase](https://hadoop-hbase.blogspot.com/2012/03/acid-in-hbase.html)
  - [HBase Shell Interaction](./legacy/databases/wide-column/hbase/shell)
  - [HBase Interaction](https://www.youtube.com/watch?v=9YkurBN5Pt0)
  - [HBase for Java Developers](https://www.youtube.com/playlist?list=PLf0swTFhTI8r6wUT9dcSQ-sLeaIMbbLm_)

#### GraphQL

- [Overview](./legacy/databases/graphql)
- [Why use GraphQL?](./legacy/databases/graphql/why)

## Software types

> Although some techniques and patterns are relevant for all kinds of software, many are relevant for only one particular branch.

- Enterprise Applications
  - [EAPPs Challenges](./legacy/enterprise/challenges)
  - [Kinds of EAPPs](./legacy/enterprise/kinds)

## Operating systems

- [Multithreading](./legacy/os/multithreading)
- [Parallelism & Concurrency](./legacy/os/parallelism)
- [Process & Thread](./legacy/os/process-thread)
- Models of Computation
  - [Finite State Machine](models-of-computation/fsm)

### Linux

- [Core principles](./legacy/os/linux/core-principles/README.md)
- [Components](./legacy/os/linux/components/README.md)
- [File system](./legacy/os/linux/file-system/README.md)

## Refactoring & code smells

- [Code Smell](https://wiki.c2.com/?CodeSmell)
- [Refactoring Guru](https://refactoring.guru/)

## Programming paradigms

- [Imperative and Procedural](./legacy/paradigms/imperative)
- [Declarative](./legacy/paradigms/declarative)

### Structured programming

> [What is structured programming?](./legacy/paradigms/structured)

- [Functional Decomposition](./legacy/paradigms/structured/functional-decomposition)
- [Structured Tests](./legacy/paradigms/structured/tests)

### OOP: Object-oriented programming

- [OOP Introduction](./legacy/paradigms/oop/README.md)
  - Objects and Classes
  - Class-based vs Prototype-based languages
- Foundational concepts
  - [4 Pillars of OOP](./legacy/paradigms/oop/4pillars.md)
    - Abstraction
    - Inheritance
    - Encapsulation
    - Polymorphism
  - [Abstract Class](./legacy/paradigms/oop/abstract-class.md)
  - [Mixin Class](./legacy/paradigms/oop/mixin.md)
  - [Traits](./legacy/paradigms/oop/traits.md)
  - [Interface & Type](./legacy/paradigms/oop/interface.md)
- Techniques
  - [Subtyping: Interface Inheritance](./legacy/paradigms/oop/subtyping.md)
  - [Composition, Aggregation and Delegation](./legacy/paradigms/oop/cad.md)
    - [Composition vs Inheritance](./legacy/paradigms/oop/inheritance-composition.md)
  - [Parameterized Types](./legacy/paradigms/oop/inheritance-parameterized.md)
  - [Dynamic Dispatch / Message Passing](./legacy/paradigms/oop/dynamic-dispatch.md)
  - [OMT Notation & UML](./legacy/paradigms/oop/omt-notations.md)
- Advanced concepts
  - [Object-Oriented Design Principles](#design-principles)
  - [Gamma Design Patterns](https://github.com/herrera-ignacio/design_patterns/)
  - [The Power of Polymorphism: Dependency Inversion](./legacy/paradigms/oop/polymorphism)
  - [Prototypal vs Classical Inheritance](./legacy/paradigms/oop/prototypal-oo)

### Functional programming

> [What is functional programming?](./legacy/paradigms/functional/README.md)

- [Referentially Transparent (No Side Effects)](./legacy/paradigms/functional/referentially-transparent.md)
- [Immutability](./legacy/paradigms/functional/immutability)
- [Idempotence](./legacy/paradigms/functional/idempotence)

## Software Engineering Culture

- [Unix Philosophy](./legacy/swe/unix-philosophy)
- [Software Engineering at Google](./legacy/swe/google-software-engineering)
- [Success stories](./legacy/swe/success-stories)
- [Quotes](./legacy/swe/quotes.md)

### Laws & Theorems

- [_80/20 Rule_](./legacy/swe/laws/80-20.md)
- [_Beyoncé Rule_: If you liked it, put a CI test](./legacy/swe/laws/beyonce.md)
- [_Churn Rule_: Teams should internalize deprecation](./legacy/swe/laws/churn.md)
- [_Constantine's law_: Favor high cohesion](./legacy/swe/laws/constantine.md)
- [_Conway's law_: Systems reflect organization's communication structure](./legacy/swe/laws/conway.md)
- [_Hyrum's Law_: The Law of Implicit Dependencies](./legacy/swe/laws/hyrum.md)
- [_Occam's Razor_: The simplest explanation](./legacy/swe/laws/occam.md)
- [_Pareto principle_: The 80/20 rule](./legacy/swe/laws/pareto.md)

### Working Methodologies

- [XP: Extreme Programming](./legacy/swe/xp)

## Testing

### [E2E Testing](testing/e2e.md)

- [Anti Patterns](testing/e2e/anti-patterns.md)
- [Best Practices](https://docs.cypress.io/guides/references/best-practices)

## General concepts

### About system-design and architecture

- [What is Software Architecture?](./legacy/architectures/general/definition)
- [The Software Architect](./legacy/architectures/general/the-software-architect.md)
- [The First Derivative](./legacy/architectures/general/the-first-derivative.md)
- [Evolutionary Design](https://www.martinfowler.com/articles/designDead.html)
- [Development Overconfidence](./legacy/architectures/general/overconfidence)
- [Is Quality Worth the Cost?](./legacy/architectures/general/quality)
- [Concurrency](./legacy/architectures/general/concurrency)
- [Distribution Strategies](./legacy/architectures/general/distribution-strategies)
- [Layering](./legacy/architectures/general/layering)
- [Resilience vs Robustness](./legacy/architectures/general/resilience-vs-robustness)

### About software engineering

- [Developer Struggle](./legacy/architectures/general/developer-struggle)
- [Mapping to Relational Databases](./legacy/architectures/general/mapping-to-rdbs)
- [Organizing Domain Logic](./legacy/architectures/general/domain-logic)
- [Session State (stateful vs stateless sessions)](./legacy/architectures/general/session-state)
- [Technical Debt](./legacy/architectures/general/technical-debt)
- [Leaky Abstractions](./legacy/architectures/general/leaky-abstraction)

### Common jargon

- [Abstract Syntax Tree](./legacy/glossary/ast)
- [CRUD](./legacy/glossary/crud)
- [First-class citizen](./legacy/glossary/first-class-citizen)
- [Modularization](./legacy/glossary/modularization)
- [Side Effect](./legacy/glossary/side-effect)
- [SPOF: Single Point of Failure](./legacy/glossary/spof)
- [Web API](./legacy/glossary/web-api)

## Tooling - Language Agnostic

- [Telepresence](https://telepresence.io): tool that is aiming to make a hybrid local/remote developer workflow easier for Kubernetes users.
- [Pact](https://pact.io): customer-driven contracts.

## Technology specifics

- [Cybersecurity Handbook](https://github.com/herrera-ignacio/cybersecurity_guidelines)
  - Networking
  - Telecommunications
  - Encryption
  - etc.
- [Golang Handbook](https://github.com/herrera-ignacio/go-handbook)
- [Go In Practice](https://github.com/herrera-ignacio/go-in-practice)
- [Java Handbook](https://github.com/herrera-ignacio/java-handbook)
- [JS Handbook](https://github.com/herrera-ignacio/js-handbook)
- React
  - [Thinking in React](https://reactjs.org/docs/thinking-in-react.html)
- Redux
  - [When and when not to reach for Redux](./legacy/redux/when)
  - [Redux must know](./legacy/redux/introduction)
  - [Three Fundamental Principles](./legacy/redux/three-principles)
  - [Best Practices](./legacy/redux/best-practices)
  - [Reducers: Immutable Update Patterns](./legacy/redux/immutable-updates)
  - [Redux Ecosystem Links](https://github.com/markerikson/redux-ecosystem-links)
  - [Flux Comparison](./legacy/redux/flux-comparison)
  - [MVC Comparison](https://blog.gisspan.com/2017/02/Redux-Vs-MVC,-Why-and-How.html)
- Data Science
  - [Batch Processing](./legacy/ds/batch-processing)
  - [ETL](./legacy/ds/etl)

### Frontend

> [Frontend developer roadmap](https://roadmap.sh/frontend).

- [Atomic design](./legacy/frontend/atomic-design/README.md)
- [Design system](./legacy/frontend/design-system/README.md)
- [Legacy lifecycle of frontend](./legacy/frontend/legacy-lifecycle/README.md)
- [Areas of frontend](./legacy/frontend/areas/README.md)
  - [Backbone goals and OKRs](./legacy/frontend/backbone-OKRs/README.md)
- [Accessibility testing](./legacy/frontend/accessibility-testing/README.md)
- [CSR vs SSR](./legacy/frontend/csr-vs-ssr/README.md)
