# Repository Pattern

> Mediates between the domain and data mapping layers using a collection-like interface for accesing domain objects.

## Overview

Repositories are a generic concept and don't necessarily have to store anything to a database. Its main function is to provide collection like (query-enabled) access to domain objects. Repositories may (and often will) contain data mappers themselves.

## Motivation

A system with a complex domain model often benefits from a layer, such as the one provided by Data Mapper, that isolates domain objects from details of the database access code. In such systems, it can be worthwhile to build another __layer of abstraction over the mapping layer where query construction code is concentrated__. This becomes more important when there are a large number of domain classes or heavy querying. In these cases particularly, adding this layer __helps minimize duplicate query logic__.

## Definition

A Repository __mediates between the domain and data mapping layers__, acting like an in-memory domain collection.

Client objects construct query specifications declaratively and submit them to Repository for satisfaction. Objects can be added to and removed from the Repository, as they can from a simple collection of objects, and the data mapping code encapsulated by the Repository will carry out the appropriate operations behind the scenes.

Conceptually, a Repository encapsulates the set of objects persisted in a data store and the operations performed over them, providing a more object-oriented view of the persistence layer. Repository also supports the objective of achieving a clean separation and one-way dependency between the domain and data mapping layers.