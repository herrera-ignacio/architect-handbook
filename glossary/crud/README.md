# CRUD

__Create, read, update and delete__ are the four basic functions of _persistent storage_.

CRUD operations are __idempotent__, meaning that multiple applications of the same operation have the same effect on a storage as a single application.

## Storage Management

> Storage management is the direct manipulation of the contents of storage locations by users.

Data can be put in a _location_ of a storage. The fundamental feature of a storage location is that it has a readable and updatable content (state). These _read_ and _update_ operations are two basic operations on a storage and re known as the __load-update pair__ (LUP).

Before a storage location can be read or updated, it needs to be available. A storage location can be made either available or unavailable for usage. These _create_ and _delete_ operations are the two other basic operations on a storage.

Together they make up the four basic operations of __storage management__.

## Database applications

Each letter in the acronym can map to a standard _SQL statement_, _HTTP method_ or _DDS_ operation.

| CRUD   | SQL    | HTTP   | DDS     |
|--------|--------|--------|---------|
| Create | Insert | PUT    | write   |
| Read   | Select | GET    | read    |
| Update | Update | PUT    | write   |
| Delete | Delete | DELETE | dispose |

Although a relational database provides a common _persistence layer_ in software applications, numerous other persistence layers exist. CRUD functionality can for example be implemented with object databases, XML databases, flat text files, or custom file formats.

## POST method

The _POST_ method in HTTP is not a CRUD operation as _GET, PUT and DELETE_, which have _storage management semantics_, meaning that they let user agents directly manipulate the states of starget resources. It is a process operation that has _target-resource-specific semantics_, so it does not let user agents directly manipulate the states of target resources. Contrary to CRUD operations, POST method is not necessarily idempotent.

* [Roy Fielding (2009-03-20), "It is okay to use POST"](https://roy.gbiv.com/untangled/2009/it-is-okay-to-use-post).
