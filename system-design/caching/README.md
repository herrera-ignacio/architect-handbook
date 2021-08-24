# Caching

* Overview
* Considerations

## Overview

*Caching* is a technique that **stores a copy of a given resource and serves it back when requested**. It is a **temporary** data store layer, **much faster** than the database, and it usually stores the result of expensive responses or frequently accessed data in memory so that **subsequent requests are served more quickly**.

> When a web cache has a requested resource in its store, it intercepts the request and returns its copy instead of redownloading from the originating server.

* This achieves several goals: it eases the load of the server that doesn't need to serve all clients itself, and improves performance by being closer to the client.

* On the other side, it has to be configured properly as not all resources stay identical forever: it is important to cache a resource only until it changes, not longer.

## Considerations

* **Decide when to use** cache: Consider using cache **when data is read frequently but modified infrequently**. Sinced cache data is stored involatile memory, a cache server is **not ideal for persisting data**. Thus, important data should be saved in persistent data stores.

* **Expiration policy**: It is advisable not to make the expiration date too short as this will cause the system to reload data from the database too frequently. Meanwhile, it is advisable not to make the expiration date too long as the data can become stale.

* **Consistency**: This involves keeping the data store and the cache in sync.

> Refer to the paper titled *"Scaling Memcache at Facebook"*.

* **Mitigating failures**: A single cache server represents a potential *SPOF*. Multiple cache servers across different data centers are recommended. Another approach is to overprovision the required memory by certain percentages, providing a buffer.

* **Eviction Policy**: Once the cache is full, any request to add items to the cache might cause existing items to be removed. *Least Recently Used (LRU)* is the most popular. Other eviction policies, such as *Least Frequently Used (LFU)* or *First in First Out (FIFO)*, can be adopted to satisfy different use cases.
