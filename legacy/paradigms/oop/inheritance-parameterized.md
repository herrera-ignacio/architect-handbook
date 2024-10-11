# Parameterized Types vs Inheritance

Parameterized types, also known as _generics_ (Ada, Eiffel) and _templates_ (C++) is a technique that lets you define a type without specifying all the other types it uses.

The unspecified types are supplied as parameters at the point of use. The language implementation will create a customized version of the class template for each type of element.

Parameterized types gives us a third way, in addition to Class Inheritance and Object Composition, to __compose behavior in Object-Oriented designs, letting you change the types that a class can use, in this case at compile-time__.

> Parameterized types aren't needed at all in a language that doesn't have compile-time type checking.
