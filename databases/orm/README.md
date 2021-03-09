# Object Relational Mapping (ORM)

ORM is a technique for converting data between incompatible type systems using object-oriented programming languages. This creates, a "_virtual object database_" that can be used from within the programming language.

This involves translating the logical representation of the objects into an atomized form that is capable of being stored ina database while preserving the properties of the objects and their relationships so that they can be reloaded as objects when needed. If this storage and retrieval functionality is implemented, the objects are said to be _persistent_.

## Comparison with traditional data access techniques

### Advantages

* Often reduces the amount of code that needs to be written

	* Represent models and their data.

	* Represent associations between these models.

	* Represent inheritance hierarchies through related models.

	* Validate models before they get persisted to the database.

	* Perform database operations in an object-related fashion.

### Disadvatages

* High level of abstraction, obscuring what is actually happening in the implementation code.

* Heavy reliance on ORM software may be a major factor in producing poorly designed databases.

## Challenges

A variety of difficulties arise when considering how to match an object system to a relational database. These difficulties are referred to as the __object-relational impedance mismatch__.