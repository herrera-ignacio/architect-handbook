# Value Object

> A small simple object, like money or a date range, whose equality isn't based on identity.

* Overview
* How It Works
* When to Use It

## Overview

*Value Object* is similar to the primitive types present in many languages that aren't purely object oriented.

## How It Works

* We like to think that *Value Objects* are small objects, such as a money object or a date, while reference objects are large, such as an order or a customer.

* The key difference lies in how they deal with equality. A **reference object uses identity as the basis for equality** (maybe the identity within the programming system, such as the built-in identity of OO programming languages, or maybe some kind of ID number, such as the primary key in a relational database). A **_Value Object_ bases its notion of equality on field values within the class**. Thus, two date objects may be the same if their day, month, and year values are the same.

* They are often passed around by value instead of by reference.

* It's a good idea to make them **immutable**, to avoid aliasing bugs (when two objects share the same value object and one of the owners changes the values in it).

* *Value Objects* shouldn't be persisted as complete records. Instead use *Embedded Value* or *Serialized LOB*.

## When to Use It

Treat something as a *Value Object* when you're basing equality on something other than an identity.

It's worth considering this for any small object that's easy to create.
