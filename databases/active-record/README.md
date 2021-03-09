# Active Record Pattern (ARP)

> ARP was described by Martin Fowler in his book _Patterns of Enterprise Application Architecture_.

This object carries both data and behavior. Much of this data is persistent and needs to be stored in a database. Active Record uses the most obvious approach, putting data access logic in the domain object. This way all people know how to read and write their data to and from the database.

## Goal

An object that wraps a row in a database table or view, encapsulates the database access and adds domain logic on that data.

## Active Record as ORM

Active Record Pattern is a description of an ORM system. It gives us several mechanisms, the most important being the ability to:

* Represent models and their data.

* Represent associations between these models.

* Represent inheritance hierarchies through related models.

* Validate models before they get persisted to the database.

* Perform database operations in an object-related fashion.
