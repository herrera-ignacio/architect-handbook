# Interface & Type

## Interface

The set of __all signatures defined by an object's operations__ is called the interface.

An object's interface __characterizes the complete set of requests that can be sent to a target__.

An object's interface says nothing about its implementation, different objects are free to implement requests differently. Two objects with completely different implementations can have identical interfaces.

# Type

Name used to __denote a particular interface__.

We speak of an object as having the type "Window" if it accepts all requests for the operations defined in the interface named "Window".

An object may have many types, and widely different objects can share a type.

Part of an object's interface may be characterized by one type, and other parts by other types. Two objects of the same type need only share parts of their interfaces.

We say that a type is a __subtype__ of another if its interface contains the interface of its supertype. Often we speak of a subtype _inheriting_ the interface of its supertype.
