# Composition, Aggregation, and Delegation

## Composition

__Objects can contain other objects in their instance variables__, this is known as _Object Composition_.

Object composition is used to represent "__has-a__" relationships. Object A "_owns_" an object B, where B has no meaning or purpose in the system without A.

For example, an object in the Employee class might contain, either directly or through a pointer, an object in the Address class. Every employee _has an_ address, so every Employee object has access to a place to store an Address object (either directly embedded within itself, or at a separate location addressed via a pointer).

Object composition is also __an alternative to class inheritance__. Here, new functionality is obtained by assembling or composing objects to get more complex functionality. This requires that the objects being composed have well-defined interfaces, no internal details of objects are visible.

## Aggregation

Object aggregation is used to represent "__uses__" relationships. Object A "_uses_" an object B, where B exists independently (conceptually) from A.

### Composition vs Aggregation

Composition an aggregation are usually confused.

Simple rules:

1. A "owns" B = Composition : B has no meaning or purpose in the system without A
2. A "uses" B = Aggregation : B exists independently (conceptually) from A

A Company is an aggregation of People and a composition of Accounts. When a Company ceases to do business its Accounts cease to exist but its People continue to exist.

## Delegation

Make composition as powerful for reuse as inheritance. In delegation, _two_ objects are involved in handling a request: __a receiving object delegates operations to its delegate__. This is analogous to subclasses deferring requests to parent classes, but with inheritance, an inherited operation can always refer to the receiving object through the `this` member in C++ for example. To achieve the same effect with delegation, the receiver passes itself to the delegate to let the delegated operation refer to the receiver.

For example, instead of making class _Window_ a subclass of _Rectangle_ (because windows happen to be rectangular), the Window class might reuse the behavior of Rectangle by keeping a Rectangle instance variable and _delegating Rectangle-specific behavior to it_. Window must now forward requests to its Rectangle instance explicitly, whereas before it would have inherited those operations.

The __main advantage__ of delegation is that it __makes easy to compose behaviors at runtime and to change the way they're composed__. Our window can become circular at run-time simply by replacing its Rectangle instance with a Circle instance, assuming they have the same type.

Delegation has a __disadvantage__ it shares with other techniques that make software more flexible through object composition: __dynamic, highly parameterized software is harder to understand than more static software__. There are also run-time inefficiences, but the human inefficiencies are more important in the long run. __Delegation is only a good design choice when it simplifies more than it complicates__.
