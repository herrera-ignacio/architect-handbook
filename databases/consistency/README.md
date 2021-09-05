# Consistency Models

* Overview
* Eventual Consistency
* Strong Eventual Consistency (SEC)

## Overview

> From CAP Theorem: **Consistency** means that every read receives the most recent write or an *error*.

Consistency model is an important factor to consider when designing a key-value store. It defines the **degree of data consistency**, and a wide spectrum of possible consistency models exist.

> Since data is replicated at multiple nodes, it must be synchronized across replicas. A common technique for this is [quorum consensus](../quorum-consensus).

## Eventual Consistency

*Eventual Consistency* is a **consistency model** used in **distributed computing** to achieve **high availability** that informally guarantees (*liveness guarantee*) that, if no new updates are made to a given data item, eventually all accesses to that item will return the last updated value.

> Eventual consistency is also called **optimistic replication**.

A system that has achieved eventual consistency is often said to have **converged**, or achieved **replica convergence**.

*Eventual Consistency* is a weak guarantee, most stronger models, like **linearizability**, are trivially eventually consistent, but a system that is merely eventually consistent does not usually fulfill these stronger constraints.

> Eventual consistency is sometimes criticized as increasing the complexity of distributed software applications.

## Strong Eventual Consistency (SEC)

Whereas eventual consistency is only a *liveness guarantee* (updates will be observed eventually), **SEC** adds the **safety guarantee** that any two nodes that have received the same (unordered) set of updates will be in the same state.

If furthermore, the system is monotonic, the application will never suffer rollbacks. *Conflict-free replicated data types* are a common approach to ensuring SEC.
