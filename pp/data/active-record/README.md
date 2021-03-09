# Active Record Pattern (ARP)

> ARP was described by Martin Fowler in his book _Patterns of Enterprise Application Architecture_.

This object carries both data and behavior. Much of this data is persistent and needs to be stored in a database. Active Record uses the most obvious approach, putting data access logic in the domain object. This way all people know how to read and write their data to and from the database.

## Goal

An object that wraps a row in a database table or view, encapsulates the database access and adds domain logic on that data.

## Pros

* __Simple__. Because of how tightly matched the records in your database and the objects in your system are conceptually.

* __Easy to understand__. Intuitive understanding of how you can work with the system even if you've never had the least exposure to an ORM before.

## Cons

* __Coupling__. The main drawback is that domain becomes tightly coupled to a particular persistence mechanism. Should that mechanism require a global change, every class that implements this pattern may change.

* __Tricky atomic operations__. If a group of objects must be saved in an all-or-nothing fashion, either one object must know about all these other objects and control their persistence, or the control over the entire transaction must be handled from outside the domain.


### Active Record vs Data Mapper

The biggest different between them is that the Data Mapper is meant to be a layer between the actual business domain and the database, where Active Record seeks to invisibly bridge the gaps between the two as seamlessly as possible.