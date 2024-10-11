# Data consistency primer

- [Data consistency primer](#data-consistency-primer)
  - [Managing data consistency](#managing-data-consistency)
  - [Considerations](#considerations)

## Managing data consistency

_Strong data consistency_ implies that all instances of an application are presented with the same set of data values all of the time, the latest updated ones.

In relational databases, consistency is often enforced by transactional models that use locks to prevent concurrent application instances from modifying the same data at the same time.

> Strongly consistent systems also locks concurrent requests to query data, but relational databases usually enable relaxing this rule and provide access to a copy of the data that reflects the state it was in before the update started.

Many non-relational databases (e.g., flat files) follow a similar strategy, known as __pessimistic locking__. An application instance locks data while it is being modified, and then releases the lock when the update is complete.

In modern cloud applications, the data is likely to be partitioned across data stores, some of which could be dispersed over a wide geography due to multiple reasons (e.g., high availability, low latency, etc.).

## Considerations

Managing and maintaining data consistency in a distributed environment is a critical aspect of the system, particularly in terms of the concurrency and availability issues that can arise.

> You frequently need to __trade strong consistency for availability__. This means that you may need to design some aspects of your solutions around the notion of eventual consistency and accept that the data that your applications use might not be completely consistent all of the time.

The issue is that strategies such as __serialization__ and __locking__ only work well if all application instances share the same data store, and the application is designed to ensure that the locks are very short-lived. However, if data is partitioned or replicated across different data stores, locking and serializing data access to maintain consistency can become an __expensive overhead__ that impacts the throughput, response time, and scalability of a system.

Therefore, most modern distributed applications __do not lock the data that they modify__, and they take a rather more relaxed approach to consistency, known as _eventual consistency_.
