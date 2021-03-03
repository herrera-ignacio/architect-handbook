# DAO: Data Access Object

Pattern that provides an abstract interface to some type of database or other persistence mechanism.

By mapping application calls to the persistence layer, the DAO provides some specific data operations without exposing details of the database. This isolation supports the __Single Responsibility Principle__.

It separates what data access the application needs, in terms of domain-specific objects and data types (the public interface of the DAO), from how these needs can be satisfied with a specific DBMS, database schema, etc (the implementation of the DAO).

## Advantages

* Simple and rigorous separation between two important parts of an application that should not know anything of each othe, and which can be expected to evolve frequently and independently (details of the storage are hidden from the rest of the application).

* Unit testing the code is facilitated by substituting the DAO with a test double in the test, thereby making the tests independent of the persistence layer.

## Potential Disadvantages

* Leaky abstraction

* _Code duplication_: If an application requires multiple DAOs, one might find oneself repeating essentailly the same CRUD for each DAO. The boilerplate may be avoided however, by implementing a generic DAO that handles these common operations.

* _Abstraction inversion_: can hide the high cost of each database access, and can also force developers to trigger multiple database queries to retrieve information that could otherwise be returned in a single operation using SQL set operations.

## Hypotetical use scenario

Imagine a situtation where you receive contracts to develop an application for two different clients. The sepcifications for the application are nearly identifical for the two clients. Both clients manage data using SQL databases, but one company uses a proprietary database and the other uses an open source alternative, which implies that your application's persistence layer will need to be implemented in two different ways. Further, as new clients arise, additional implementations may be needed. In this case, using the DAO pattern would ensure the right amount of abstraction and encapsulation required to access any of the varying backend databases.