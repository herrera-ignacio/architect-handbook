# Object Oriented Programming

- [Object Oriented Programming](#object-oriented-programming)
  - [Overview](#overview)
  - [History](#history)
  - [Objects and Classes](#objects-and-classes)

## Overview

> OOP imposes discipline on indirect transfer of control.

Programming paradigm based on the concept of _objects_, which can contain data in the form of fields (often known as _attributes_ or _properties_), and code in the form of procedures (often known as _methods_).

Object's procedures can access and often modify the data fields of the object with which they are associated (objects often have a notion of `this` or `self`).

OOP languages are diverse, but the most popular ones are _class-based_, meaning that objects are _instances of classes_, which also determine their types. Many of the most widely used programming languages are _multi-paradigm_ and they support object-oriented programming to a greater or lesser degree, typically in combination with Imperative and Procedural programming.

## History

Discovered in _1966_ by _Ole Johan Dahl_ and _Kirsten Nygaard_. These two programmers noticed that the function call stack frame in the _ALGOL_ language could be moved to a heap, thereby allowing local variables declared by a function to exist long after the function returned. The function became a constructor for a class, the local variables became instance variables, and the nested functions became methods. This led inevitably to the discovery of polymorphism through the disciplined use of function pointers.

## Objects and Classes

OOP typically uses __Inheritance__ for code reuse and extensibility in the form of either _Classes_ or _Prototypes_. Those that use classes support two main concepts:

* __Classes__: definitions for the data format and available procedures for a given type or class of object, may also contain data and procedures themselves.
* __Objects__: instances of classes. 

Objects provide a layer of _Abstraction_, which can be used to separate internal from external code. External code can use an object by calling a specific instance method with a certain set of input parameters, read an instance variable, or write to an instance variable.

Objects are created by calling a special type of method in the class known as _Constructor_. A program may create many instances of the same class as it runs, which operate independently.

In some languages classes and objects can be composed using other concepts like __Traits__ and __Mixins__.


