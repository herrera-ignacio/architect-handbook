# Composition vs Inheritance 

_Class Inheritance_ is defined statically at compile-time and is straightforward to use. It also makes it easier to modify the implementation being reused. When a subclass overrides some but not all operations, it can affect the operations it inherits as well.

But _Class Inheritance_ has its disadvantages too:

* You can't change implementations inherited at run-time.
* Parent classes often define at least part of their subclasses' physical representation. Because inheritance exposes a subclass to details of its parent's implementation, it's often said that "__Inheritance breaks encapsulation__", as implementation of a subclass becomes so bound up with the implementation of its parent class that any change in the parent's implementation will force the subclass to change.

_Object Composition_ is defined dynamically at run-time through objects acquiring references to another objects, which requires objects to respect each others' interfaces, which in turn requires carefully designed interfaces.

Because objects in _Object Composition_ are accessed solely through their interfaces, we don't break encapsulation, there are substantially fewer implementation dependencies. __Object composition helps you keep each class encapsulated and focused on one task__. YOur classes and class hierarchies will remain small.
