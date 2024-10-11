# Horizontal partitioning primer (_sharding_)

> Check [sharding pattern](https://docs.microsoft.com/en-us/azure/architecture/patterns/sharding) for a more details about implementation considerations.

- [Horizontal partitioning primer (_sharding_)](#horizontal-partitioning-primer-sharding)
  - [Overview](#overview)
  - [Sharding keys](#sharding-keys)

## Overview

Sharding spreads the load over more computers, which reduces contention and improves performance.

![](2022-08-10-20-02-41.png)

> In this example, product inventory data is divided into shards based on the product key. Each shard holds the data for a contiguous range of shard keys (A-G and H-Z), organized alphabetically.

## Sharding keys

The most important factor is the choice of a sharding key. It can be difficult to change it after the system is in operation. The key must __ensure that data is partitioned to spread the workload as evenly as possible__ across the shard.

The shards don't have to be the same size. It's more important to __balance the number of requests__. Some shards might be vary large, but each item has a low number of access operations. Other shards might be very small, but each item is accessed much more frequently. Nevertheless, it's also important to ensure that a single shard does not exceed the scale limits.

Avoid creating "hot" partitions that can affect performance and availability. For example, using the first letter of a customer's name causes an unbalanced distribution, because some letters are more common. Instead, use a hash of a customer identifier to distribute data more evenly across partitions.

Choose a sharding key that __minimizes any future requirement__ to split large shards, coalesce small shards into larger partitions, or change the schema.
