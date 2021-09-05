# Design a key-value store

* Overview
* Design scope
  * Single server key-value store
  * Distributed key-value store
  * System components

## Overview

A key-value store, also referred to as a key-value database, is a non-relational database. Each unique identifier is stored as a key with its associated value.

In a key-value pair, the key must be unique, and a value can be accessed through it associated the key. Keys can be plain text or hashed values. For performance reasons, a short key works better. The value can be strings, lists, objects, etc; and it's usually treated as an opaaque object in key-value stores.

A basic key-value store would support the following operations:

* `put(key, value)`: inserts "value" associated with "key".

* `get(key)`: get "value" associated with "key".

## Design scope

Each design achieves a specific balance regarding the tradeoffs of the read, write, and memory usage. Another tradeoff has to be made between consistency and availability.

### Single server key-value store

An intuitive approach is to store key-value pairs in a hash table, which keeps everything in memory. Even though memory access is fast, fitting everything in memory may be impossible due to the space constraint.

Two optimizations can be done to fit more data in a single server:

* Data compression
* Store only frequently used data in memory and the rest on disk

Even with these optimizations, a single server can reach its capacity very quickly. A distributed key-value store is required to support big data.

### Distributed key-value store

A distributed key-value store distributes key-value pairs across many servers. It is important to understand [CAP theorem](../../../databases/cap). Choosing the right CAP guarantees that fit your use case is an important step in building the system.

### System components

There are a few core components and techniques used to build a key-value store:

* [Data partition](../../../databases/partitioning)
* [Data replication](../../../databases/replication)
* [Consistency](../../../databases/consistency)
* [Inconsistency resolution]()
* [Handling failures]()
* [System architecture diagram]()
* [Write path]()
* [Read path]()
