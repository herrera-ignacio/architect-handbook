# Data partitioning

- [Data partitioning](#data-partitioning)
  - [Overview](#overview)
  - [Why partition data?](#why-partition-data)
  - [Designing partitions](#designing-partitions)
    - [Designing for scalability](#designing-for-scalability)
    - [Designing for query performance](#designing-for-query-performance)
    - [Designing for availability](#designing-for-availability)
  - [Application design considerations](#application-design-considerations)
  - [Rebalancing partitions](#rebalancing-partitions)
    - [Offline migration](#offline-migration)
    - [Online migration](#online-migration)

## Overview

In many large-scale solutions, data is divided into _partitions_ that can be managed and accessed separately. Partitioning can improve scalability, reduce contention, and optimize performance. It can also provide a mechanism for dividng data by usage pattern. For example, you can archive older data in cheapar data storage.

> The partitioning strategy must be chosen carefully to maximize the benefits while minizing adverse effects.

## Why partition data?

- __Improve scalability__: You might overcome the physical hardware limits of using a single database system.
- __Improve performance__: Data access operaitons take place over a smaller volume of data. Operations that affect more than one partition can run in parallel.
- __Improve security__: You can separate sensitive data into a different partition and apply different security controls.
- __Improve availability__: Avoids a single point of failure. If one instance fails, only the data in that partition is unavailable.
- __Provide operational flexibility__: You can fine-tune operations & define different strategies for management, monitoring, backup and restore, based on the importance of the data in each partition.

## Designing partitions

There are three typical strategies for partitioning data:

- [Horizontal partitioning (_sharding_)](./horizontal.md): Each partition (_shard_) is a separate data store, but all partitions have the same schema.
- [__Vertical partitioning__](./vertical.md): Each partition holds a subset of the fields for items in the data store. The fields are divided according to their pattern of use.
- [__Functional partitioning__](./functional.md): Data is aggregated according to how it is used by each bounded context in the system. For example, invoice data is stored in one partition and product inventory in another.

These strategies can be combined. For example, you might divide data into shards and then use vertical partitioning to further subdivde the data in each shard.

### Designing for scalability

Consider size and workload for each partition and balance them so that data is distributed to achieve maximum scalability. However, you must also partition the data so that it does not exceed the scaling limits of a single partition store.

Follow these steps when designing partitions for scalability:

1. __Analyze the application to understand the data access patterns__, such as the size of the result set returned by each query, the frequency of access, the inherent latency, and the server-side compute processing requirements. In many cases, a few major entities will demand most of the processing resources.
2. Use this analysis to determine the __current and future scalability targets__, such as data size and workload. Then distribute the data across the partitions to meet the scalability target (e.g., choose the right _sharding key_).
3. Make sure each partition __has enough resources to handle data size and throughput__. If the requirements are likely to exceed these limits, you may need to refine your partitioning strategy or split data out further, possibly combining two or more strategies.
4. __Monitor the system__ to verify that data is distributed as expected and that partitions can handle the load. Actual usage does not always match what an analysis predicts. If so, it might be possible to rebalance some of the partitions.

### Designing for query performance

Query performance can often be boosted by using __smaller data sets and by running parallel queries__. Each partition should contain a small proportion of the entire data set. However, partitioning is not an alternative for designing and configuring a database appropriately. __You must still use indexes and other techniques to optimize query performance__.

Follow these steps when designing partitions for query performance:

1. Examine the application requirements and performance.
   - Use business requirements to determine the critical queries that must always perform quickly.
   - Monitor the system to identify any queries that perform slowly.
   - Find which queries are performed most frequently.
2. Partition the data that is causing slow performance:
   - Limit the size of each partition so that the query response time is within target.
   - Design a sharding key so that the application can easily select the right partition.
   - Consider the location of a partition. Try to optimize based on geography.
3. If an entity has throughput and query performance requirements, use functional partitioning based on that entity. If this is not enough, combine with horizontal partitioning.
4. Consider running queries in parallel across partitions.

### Designing for availability

Partitioning data can improve availability by ensuring that the entire dataset does not constitute a _single point of failure_ and that __individual subsets can be managed independently__.

Consider the following factors that affect availability:

- __How critical the data is to business operations__. Identify which data is critical, such as transactions, and which data is less critical operational data, such as log files.
  - Consider storing critical data in highly available partitions with an appropriate backup plan.
  - Establish separate management and monitoring procedures.
  - Place data with the same level of criticality in the same partition so that it can be backed up together at an appropriate frequency.
- __How individual partitions can be managed__. Support for independent management and maintenance.
  - If a partition fails, it can be recovered independently without affecting applications that access data in other partitions.
  - Partitioning by geographical area allows scheduled maintenance tasks to occur at off-peak hours for each location.
- __Whether to replicate critical data across partitions__. This can improve availability and performance, but can also introduce consistency issues. It takes time to synchronize changes with every replica.

## Application design considerations

Partitioning __adds complexity__ to the design and development of your system. If you address partitioning as an afterthought, it will be more challenging so consider it as a fundamental part of system design even if the system initially contains a single partition.

- __Minimize cross-partition data access operations__: Querying across partitions can be more time-consuming, but optimizing partitions for one set of queries might adversely affect other sets of queries. If you must query across partitions, minimize query time by running parallel queries and aggregating the results within the application.
- __Consider replicating static reference data__: Data such as postal code tables or product lists, consider replicating this data in all of the partitions to reduce separate lookup operations in different partitions.
- __Minimize cross-partition joins__: Minimize requirements for _referential integrity across vertical and functional partitions_. In these schems, the application is responsible for maintaining referential integrity across partitions. Consider replicating or _de-normalizing_ the relevant data if needed. As a last resource, run parallel queries over the partitions and join the data within the application.
- __Embrace eventual consistency__: The data in each partition is updated separately, and the application logic ensures that the updates are all completed successfully. It also handles the inconsistencies that can arise.
- __Consider periodically rebalancing shards__: It can help distribute the data evenly by size and by workload. However, this is a complex task that often requires a custom tool or process.
- __Replicate partitions__: Provides additional redundancy and availability.

## Rebalancing partitions

As a system matures, you might have to adjust the partitioning scheme. For example, partitions might start getting a disproportionate volume of traffic and become hot, leading to excessive contention. Or, you might have underestimated the volume of data in some partitions.

Some data stores, such as Cosmos DB, can automatically rebalance partitions. In other cases, it is an administrative task that consists on two stages:

1. Determine a new partitioning strategy.
      - Which partitions need to be split or merged?
      - What is the new partition key?
2. Migrate data from the old partitioning scheme to the new one.

### Offline migration

Offline migration is typically simpler because it reduces the chances of contention occurring.

1. Mark the partition offline or mak as read-only.
2. Split-merge and move the data to the new partitions.
3. Verify the data.
4. Bring the new partitions online.
5. Remove the old partition.

### Online migration

Online migration is more complex to perform but less disruptive. Depending on the granularity of the migration progress (e.g., item by item, shard by shard), the access code in the client applications might have to handle reading and writing data that's held in two locations, the original partition and the new partition.
