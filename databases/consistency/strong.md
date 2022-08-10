# Strong consistency

- [Strong consistency](#strong-consistency)
  - [Overview](#overview)
  - [Disadvantages](#disadvantages)
  - [Impact on distributed environments](#impact-on-distributed-environments)

## Overview

__All changes are atomic__. If a transaction updates multiple data items, the transaction is not allowed to complete until either all of the changes have been made successfully, or if there's a failure, they have all been undone.

In the team between a transaction starting and completing, other concurrent transactions may not be able to access any of the data that has been modified; they will be blocked.

> If data is being replicated, a transaction that implements strong consistency is allowed to complete until every copy of each iteam that has changed has been updated successfully.

It aims to minimize the chance that an application instance might be presented with an inconsistent view of the data.

## Disadvantages

The cost of implementing this model is __the impact it has on the availability, performance, and scalability__ of the resulting solution.

- Network latency could adversely impact the performance of such transactions and result in concurrent access to data being blocked for an extended perior of time.
- If a network failure renders one or more data stores inaccessible during a transaction, the application will be blocked until every data store becomes accessible again.
- It is not tolerant of the types of failure that may occur in distributed environments. For example, it may not be possible to roll back a transaction and release the resources that it holds if a component participating in the transaction has stopped responding due to a network failure. In this case, _manually reconciling_ the data is needed.

## Impact on distributed environments

In a distributed application, you should implement strong consistency only where it is absolutely necessary.

> For example, if an application updates multiple items that are located within the same data store, the benefits may outweigh the disadvantages because data is likely to be locked only for a very short period.

An alternative approach for maintaining strong consistency across replicated data that is frequently implemented by highly scalable NoSQL databases is to use read and write _quorums_ and _versioning_.
