# Data Mapper

> Data Mapper was described by Martin Fowler in his book _Patterns of Enterprse Application Architecture_.

> A layer of Mappers that moves data between objects and a database while keeping them independent of each other and the mapper itself.

## Overview

The interface of an object conforming to this pattern would include functions such as CRUD, that operate on objects that represent domain entity types in a data store.

A Data Mapper is a _Data Access Layer_ that performs bidirectional transfer of data between a persistent data store and an in-memory data representation (_Domain Layer_).

## Motivation

__Objects and relational database have different mechanisms for structuring data__. Many parts of an object, such as collections and inheritance, aren't present in relational databases. When you build an object model with a lot of business logic it's valuable to use these mechanisms to bettter organize the data and the behavior that goes with it. __Doing so leads to variant schemas, that is, the object schema and the relational schema don't match up__.

You still need to transfer data between the two schemas, and this transfer becomes a complexity in its own right. If the in-memory objects know about the relational database structure, changes in one tend to ripple the other.

## Definition

The Data Mapper is a __layer__ of software that __separates in-memory objects from the database__. It's responsibility is to __transfer data between te two and also to isolate them from each other__.

With Data Mapper, the in-memory objects needn't know even that there's a database present, they need no SQL interface code, and certainly no knowledge of the database schema. (Also, the database schema is always ignorant of the objects that use it).

Since it's a form of Mapper, Data Mapper itself is even unknown to the domain layer.

## Data Mapper Pros as ORM

* __Greater flexibility__. Application architecture don't necessarily have a final say on the database scheme. Where you've got a historical database, or a new database with an unfriendly gatekeeper, Data Mapper allows you to hide the ways in which your database isn't an ideal way to think about your domain. This allows for more complex models too.

* __Can be have greater performance__. Data Mapper can make more efficient use of the database than a naive Active Record implementation would allow.

### TL;DR

> Datamappers might have "find" or query functionality, but that is not really their main function. The more you find that you are using elaborate query logic in your DataMappers, the more you want to start thinking about decoupling that query logic into a repository while leaving your DataMappers to serve their main function, mapping domain objects to the database and vice versa. [Stackoverflow 27996119](https://stackoverflow.com/questions/27996119/what-exactly-is-the-difference-between-a-data-mapper-and-a-repository)
