# BASE

* Overview
* Conflict Resolution
* Strong Eventual Consistency (SEC)

## Overview

Eventually-consistent services are often classified as providing *BASE* semantics (*Basically Available, Soft state, Eventual consistency*), in contrast to traditional *ACID* guarantees.

* **Basically Available**: Basic reading and writing operations are available as much as possible (using all nodes of a database cluster), but without any kind of consistency guarantees (the write may not persiste after conflicts are concilied, the read may not get the latest write).

* **Soft State**: Without consistency guarantees, after some amount of time, we only have some probability of knowing state, since it may not yet have converged.

* **Eventually consistent**: If the system is functioning and we wait long enough after any given set of inputs, we will eventually be able to know what the state of the database is, and so any further reads will be consistent with our expectations.

## Conflict Resolution

In order to ensure *replica convergence*, a system must reconcile differences between multiple copies of distributed data. This consists of two parts:

* Exchanging versions or updates of data between servers (often know as **anti-entropy**).

* Choosing an appropriate final state when concurrent updates have occurred, called **reconcilliation**.

### Reconcilliation

The most appropriate approach to *reconcilliation* depends on the application. A widespread approach is *"last writer wins"*. Another is to invoke a user-specified conflict handler. *Timepstamps* and *vector clocks* are often used to detect concurrency between updates. Some people use *"first writer wins"*.

Reconcilliation of concurrent writes must occur sometime before the next read, and can be scheduled at different instants:

* **Read repair**: The correction is done when a read finds an inconsistency. This slows down the read operation.

* **Write repair**: The correction takes place during a write operation, if an inconsistency has been found, slowing down the write operation.

* **Asynchronous repair**: The correction is not part of a read or write operation.
