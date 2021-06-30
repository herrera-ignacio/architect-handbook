# Table Data Gateway

> *"An object that acts as a __Gateway__ to a database table. One instance handles all the rows in the table."*

* Overview
* How It Works
* When to Use It
* Example

## Overview

![](2021-06-29-23-30-36.png)

Mixing SQL in application logic can cause several problems. Many developers aren't comfortable with SQL, and many who are comfortable not write it well. Database administrators need to be able to find SQL easily so they can figure out how to tune and evolve the database.

A *Table Data Gateway* holds all the SQL for accessing a single table or view: selects, inserts, updates, and deletes. Other code calls its methods for all interaction with the database.

## How It Works

A *Table Data Gateway* has a simple interface, usually consisting of several find methods to get data from the database and update, insert, and delete methods. Each method **maps the input parameters into a SQL call and executes the SQL againast a database connection**. The *Table Data Gateway* is usually satateless, as its role is to push data back and forth.

The trickiest thing is how it returns information from a query:

* **Simple data structure**, such as a map. But this forces data to be copied out of the record set that comes from the database into the map, it defeats compile time checking and isn't a very explicit interface.

* __*Data Transfer Object*__.

* __*Record Set*__ that comes from the SQL query. This is conceptually messy, as ideally the in-memory object doesn't have to know anything about the SQL interface. It may also make it difficult to substitute the database for a file or something else.

A *Table Data Gateway* works very well with *Table Module*. If all your updates are done through the *Table Data Gateway*, the returned data can be based on views rather than on the actual tables, which reduces the coupling between your code and the database.

If you're using a *Domain Model*, you can have the *Table Data Gateway* return the appropriate domain object. The problem with this is that you then have bidirectional dependencies between the domain objects and the gateway.

## When to Use It

The first decision is whether to use a *Gateway* approach at all and then which one.

*Table Data Gateway* is probably the simplest database interface pattern to use, as it maps so nicely onto a database table or record type. It also makes a natural point to encapsulate the precise access logic of the data source.

*Table Data Gateway* works particularly well with *Table Module*, where it produces a record set data structure for the *Table Module* to work on. It is also very suitable for *Transaction Scripts*. *Data Mapper* gives a bettewr isolation between *Domain Model* and the database.

Interestingly, it often makes sense to have the *Data Mappers* talk to the database via *Table Data Gateways*. It can be very effective if you want to use metadata for the *Table Data Gateways* but prefer handcoding for the actual mapping to the domain objects.
