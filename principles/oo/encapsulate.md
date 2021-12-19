# Encapsulate what varies

> It's all about letting one part of the system vary independently of another part.

This principle has two aspects that roughly dcorrespond to [SRP](../../principles/solid/srp) and [OCP](../../principles/solid/ocp) principles.

1. **Make changes local**. Everything which is supposed to change in the future should be encapsulated in a single module. This means *cross-cutting concerns* are avoided as much as possible.

2. **Introduce abstractions**. Sometimes the varying concept is one which varies at runtime rather than by maintenance. In this case, there has to be an *abstract base class* or an *interface* which encapsulates the varying concepts.

## Program to an interface, not an implementation

Implementation reuse is only half the story. Inheritance's ability to define families of objects with _identical_ interfaces is also important. Why? Because __polymorphism depends on it__.

When inheritance is used _properly_, all classes derived from an abstract class will share its interface. This implies that a subclass merely adds or overrides operations, and does not hide operations of the parent class.

All subclasses can then respond to the requests in the interface of the abstract parent class, making them __subtypes of the abstract class__.

There are two benefits to manipulating objects solely in terms of the interface defined by abstract classes:

1. Clients remain unaware of the specific types of objects they use, as long as the objets adhere to the interface that client expect.
2. Clients remain unaware of the classes that implement these objects, they only know about the abstract clas(es) defining the interface.

This so __greatly reduces implementation dependencies__ between subsystems that it leads to the principle: _PRogram to an interface, not an implementation.
