# Decomposing the Database

## Overview

Microservices work best when we practice *information hiding*, which in turn typically leads us toward microservices totally encapsulating their own data storage and retrieval mechanisms.

Splitting a database apart is far from a simple endeavor, however. We need to consider issues of:

* Data synchronization during transactions
* Logical versus physical schema decomposition
* Transactional integrity
* Joins
* Latency
* More...

## Transferring Ownership

Before we start considering the tricky task of pulling data out of the giant monolithic database, we need to consider where the data in question should actually live. As you split services out from the monolith, some of the data should come with you, and some of it should stay where it is.

If we embrace the idea of a microservice *encapsulating the logic* associated with one or more aggregates, we also need to *move the management of their state* and associated data into the microservice's own schema.

On the other hand, if our new microservice needs to interact with an aggregate that is still owned by the monolith, we need to *expose this capability via a well-defined interface*.
