# CQRS: Command and Query Responsibility Segregation

> CQRS is a pattern that separates read and update operations for a data store. It allows a system to better evolve over time and prevents update commands from causing merge conflicts at the domain level.

- [CQRS: Command and Query Responsibility Segregation](#cqrs-command-and-query-responsibility-segregation)
  - [Context and problem](#context-and-problem)
  - [Solution](#solution)
    - [Separate data stores](#separate-data-stores)

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

