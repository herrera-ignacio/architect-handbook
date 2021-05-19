# Object-Relational Impedance Mismatch

Set of conceptual and technical difficulties that are often encountered when a _RDBMS_ is being served by an application program written in an OOP language or style, particularlty because objects or class definitions must be mapped to database tables defined by a relational schema.

> Objects reference one another and therefore form a graph in the mathematical sense. Relational schemas are, in contrast, tabular and based on relational algebra, which defines linked heterogeneous tuples (groupings of data fields into a "row" with different types for each field). - [Wikipedia](https://en.wikipedia.org/wiki/Object%E2%80%93relational_impedance_mismatch)

* Granularity
* Subtypes (inheritance)
* Identity
* Associations
* Data navigation

## Granularity

> Object model is more granular than the relational model.

You can have an object model which has more classes than the number of corresponding tables in the database.

## Subtypes (Inheritance)

RDBMs do not define any standard similar on the whole to OOP subtyping.

## Identity

RDBMS defines exactly one notion of "_sameness_", the primary key. However, OOP have different concepts such as object identity and object equality.

## Associations

OOP represents associations as unidirectional references, whereas RDBMS use the notion of foreign keys. In OOP if you need bidirectional relationship, you must define the association twice.

Likewise, you cannot determine the multiplicity of a relationship by looking at the object domain model.

## Data Navigation

In an OOP language, you can navigate from one association to anoter by walking the object network. This is not an efficient way of retrieving data from a relational database. You typically want to minimize the number of SQL queries and thus load several entities via JOINs and select the targeted entities before you start walking the object network.
