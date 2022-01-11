# Isolation Levels

- [Isolation Levels](#isolation-levels)
  - [Overview](#overview)
  - [Performance vs Isolation](#performance-vs-isolation)
  - [ISO SQL Standard: Isolation Levels](#iso-sql-standard-isolation-levels)
  - [1. Read uncommited](#1-read-uncommited)
  - [2. Read commiteted](#2-read-commiteted)
  - [3. Repeatable read](#3-repeatable-read)
  - [4. Serializable](#4-serializable)
  - [Distributed Systems](#distributed-systems)
  - [References](#references)

## Overview

Database isolation refers to the ability of a database to allow a transaction to execute as if there are no other concurrently running transactions (even though in reality there can be a large number of concurrently running transactions).

> The overarching goal is to prevent reads and writes of temporary, aborted, or otherwise incorrect data written by concurrent transactions.

## Performance vs Isolation

Performance is inversely proportional to how much *read phenomena* we avoid/control.

> Therefore, performance goes down every level of isolation. 

## ISO SQL Standard: Isolation Levels

| Isolation Level  	| Dirty read 	| Non-repeatable Read 	| Phantom Read 	|
|------------------	|------------	|---------------------	|--------------	|
| READ UNCOMMITTED 	| Yes        	| Yes                 	| Yes          	|
| READ COMMITTED   	| No         	| Yes                 	| Yes          	|
| REPEATABLE READ  	| No         	| No                  	| Yes          	|
| SERIALIZABLE     	| No         	| No                  	| No           	|

## 1. Read uncommited

No isolation, any change from the outside is visible to the transaction.

## 2. Read commiteted

Each query in a transaction only sees comitted stuff.

* Lost updates
* Non-repeatable reads
* Phantoms

## 3. Repeatable read

Each query in a transaction only sees comitted updates at the beginning of transaction. So you will only see changes that were comitted before the start of the transaction.

* Phantoms

## 4. Serializable

Transactions are "serialized". The system  *ensures* that when transactions are running concurrently, the final state is equivalent to a state of the system that would exist if they were run serially. There are several ways to achieve this —such as via locking, validation, or multi-versioning.

## Distributed Systems

In distributed systems, there are important *anomalies* that can (and do) emerge even *within* the class of serializable isolation levels. For such systems, it is important to understand the subtle differences between the elements of the class of serializable isolation (strict serializability is known to be the most safe).

Many distributed systems implement variations of the serializable isolation level, such as *one copy-serializability* (1SR), *strict serializability* (strict 1SR) or *update serializabilit*y (US).

## References

* [Introduction to Isolation Levels](https://fauna.com/blog/introduction-to-transaction-isolation-levels)
* [Serializability vs "Strict" Serializability](https://fauna.com/blog/serializability-vs-strict-serializability-the-dirty-secret-of-database-isolation-levels)
