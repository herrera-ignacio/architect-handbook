# CQRS: Command and Query Responsibility Segregation

> CQRS is a pattern that separates read and update operations for a data store. It allows a system to better evolve over time and prevents update commands from causing merge conflicts at the domain level.

- [CQRS: Command and Query Responsibility Segregation](#cqrs-command-and-query-responsibility-segregation)
  - [Context and problem](#context-and-problem)
  - [Solution](#solution)
  - [Advantages](#advantages)
  - [Issues and considerations](#issues-and-considerations)
  - [When to use](#when-to-use)
  - [When not to use](#when-not-to-use)
  - [Implementation details](#implementation-details)
    - [Separate data stores](#separate-data-stores)
    - [Event sourcing](#event-sourcing)

## Context and problem

In traditional architectures, the same data model is used to query and update a database. That's simple and works well for basic CRUD operations.

However, as the system evolves, the data model and the queries become more complex. On the read side, the application may perform many different queries, returning DTOs with different shapes. On the write side, the model may implement complex validation and business logic.

![](2022-08-08-13-50-43.png)

- There is often a _mismatch_ between the read and write representations of data, such as additional columns or properties that must be updated correctly even though they aren't required as part of an operation.
- _Data contention_ can occur when operations are performed in parallel on the same set of data.
- _Performance_ can be affected due to load on the data store and data access layer, and the _complexity_ of the queries requried to retrieve information.
- Managing _security_ and permissions can become complex, because each entity is subject to both read and write operations, which might expose data in the wrong context.

## Solution

CQRS separates reads and writes into different models, using __commands__ to update data, and __queries__ to read data.o

- Commands should be task-based, rather than data centric. (e.g. "Book hotel room", not "set ReservationStatus to Reserved").
- Commands may be placed on a queue for asynchronous processing, rather than being processed synchronously.
- Queries never modify the database. A query returns a DTO that does not encapsulate any domain knowledge.

![](2022-08-08-14-05-36.png)

> The models can then be isolated, although that's not an absolute requirement.

## Advantages

- __Independent scaling__: CQRS allows the read and write workloads to scale independently, and may result in fewer lock contentions.
- __Optimized data schemas__: The read side can use a schema that is optimized for queries, while the write side uses a schema that is optimized for updates.
- __Security__: It's easier to ensure that only the right domain entities are performing writes on the data.
- __Separation of concerns__: Segregating the read and write sides can result in models that are more maintainable and flexible. Most of the complex business logic goes into the write model. The read model can be relatively simple.
- __Simpler queries__: By storing a materialized view in the read database, the application can avoid complex joins when querying.

## Issues and considerations

- __Complexity__: CQRS code can't automatically be generated from a database schema using caffolding mechanisms such as ORM tools. It can lead to more complex design and implementation, especially if they include the _Event Sourcing_ pattern.
- __Messaging__: It's common to use messaging to process commands and publish update events. Therefore, the application must handle message failures or duplicate messages.
- __Eventual consistency__: If you separate the read and write databases, the read data may be stale. The read store must be updated to reflect changes to the write store, and it can be difficult to detect when a user has issued a request based on stale read data.

## When to use

- __Collaborative domains where many users access the same data in parallel__. CQRS allows you to define commands with enough granularity to minimize merge conflicts at the domain level, and conflicts that do arise can be merged by the command.
- __Task-based UI__ where users are guided through a complex process as a __series of steps__ or with __complex domain models__. The wirte model has a full command-processing stack with business logic, input validation, and business validation.
- Performance of data reads must be fine-tuned separately from performance of data writes, especially when the __number of reads is much greater than the number of writes__.
- One team of developers can focus on the complex domain model for writes, while another team can focus on the read model and the user interfaces.
- The system is expected to evolve over time and might contain __multiple versions of the model__, or where business rules change regularly.
- Integration with other systems, especially in __combination with event sourcing__, where the temporal failure of one subsystem shouldn't affect the availability of the others.

## When not to use

- The domain or the business rules are simple.
- A simple CRUD-style UI and data access operations are sufficient.

> Consider applying CQRS to limited sections of your system where it will be most valuable.

## Implementation details

### Separate data stores

For greater isolation, you can physically separate the read data from the write data. In that case, the read database can use its own data schema that is optimized for queries.

For example, it can store a _materialized view_ of the data, in order to avoid complex joins or complex ORM mappings. It might even use a different type of data store. For example, the write database might be relational, while the read database is a document database.

If separate read and write databases are used, __they must be kept in sync__. Typically this is accomplished by having the write model publish an event whenever it updates the database. This __must occur in a single transaction__.

> See [Event-driven architecture style](https://docs.microsoft.com/en-us/azure/architecture/guide/architecture-styles/event-driven).

![](2022-08-08-14-51-52.png)

### Event sourcing

CQRS is often used along with the _Event Sourcing_ pattern. The store of events is the write model, and is the official source of information. The read model of a CQRS-based system provides materialized views of the data, typically as highly denormalized views. These views are tailored to the UI, which helps to maximize both display and query performance.

Using the stream of events as the write store, rather than the actual data at a point in time, __avoid updates conflicts__ on a single aggregate and maximizes performance and scalability. The events can be used to __asynchronously generate materialized views__ of the data.

Because the event store is the official source of information, it is possible to delete the materialized views and replay all past events to create a new representation of the current state when the system evolves, or when the read model must change.

When using CQRS combined with Event Sourcing, consider the following:

- Systems are __only eventually consistent__. There will be some delay between the event being generated and the data store being updated.
- __Adds complexity__ because code must be created to initiate and handle events, and assemble or update the appropriate views requires by the read model. However, it can make it easier to model the domain, and makes it easier to rebuild views or create new ones because the intent of the changes in the data is preserved in the event stream.
- Generating materialized views for use in the read model by replaying and handling the events can require significant processing time and resource usage. Resolve this by implementing _snapshots_ at scheduled intervals.
