# Object Oriented Programming

> OOP imposes discipline on indirect transfer of control.

Programming paradigm based on the concept of _objects_, which can contain data in the form of fields (often known as _attributes_ or _properties_), and code in the form of procedures (often known as _methods_).

Object's procedures can access and often modify the data fields of the object with which they are associated (objects often have a notion of `this` or `self`).

OOP languages are diverse, but the most popular ones are _class-based_, meaning that objects are _instances of classes_, which also determine their types. Many of the most widely used programming languages are _multi-paradigm_ and they support object-oriented programming to a greater or lesser degree, typically in combination with Imperative and Procedural programming.

## History

Discovered in _1966_ by _Ole Johan Dahl_ and _Kirsten Nygaard_. These two programmers noticed that the function call stack frame in the _ALGOL_ language could be moved to a heap, thereby allowing local variables declared by a function to exist long after the function returned. The function became a constructor for a class, the local variables became instance variables, and the nested functions became methods. This led inevitably to the discovery of polymorphism through the disciplined use of function pointers.

## Features

### Objects and Classes

OOP typically uses __Inheritance__ for code reuse and extensibility in the form of either _Classes_ or _Prototypes_. Those that use classes support two main concepts:

* __Classes__: definitions for the data format and available procedures for a given type or class of object, may also contain data and procedures themselves.
* __Objects__: instances of classes. 

Objects provide a layer of _Abstraction_, which can be used to separate internal from external code. External code can use an object by calling a specific instance method with a certain set of input parameters, read an instance variable, or write to an instance variable.

Objects are created by calling a special type of method in the class known as _Constructor_. A program may create many instances of the same class as it runs, which operate independently.

In some languages classes and objects can be composed using other concepts like __Traits__ and __Mixins__.

### Class-based vs Prototype-based

In Class-based languages the _classes_ are defined beforehand and the _objects_ are instantiated based on the classes. If two objects _apple_ and _orange_ are instantiated from the class _Fruit_, they are inherently fruits and it is guaranteed that you may handle them in the same way.

In Prototype-based languages the _objects_ are the primarty entities. No _classes_ even exist. The _prototype_ of an object is just another object to which the object is linked. Every object has one prototype link (and only one). New objects can be created based on already existing objects chosen as their prototype. You may call two different objects _apple_ and _orange_ a fruit, if the object _fruit_ exists, both apple and orange may have fruit as their prototype. The idea of the fruit class doesn't exist explicitly, but as the equivalence class of the object's sharing the same prototype. The attributes and methods of the prototype are delegated to all the objects of the equivalence class defined by this prototype. The key difference is that the attributes and methods _owned individually_ by the object may not be shared by others of the same equivalence class, thus it is not guaranteed that two objets linked to the same prototype may be handled the same way.

Only single inheritance can be implemented through the prototype.
