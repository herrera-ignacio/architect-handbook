# GRASP

- [GRASP](#grasp)
  - [Definition](#definition)
  - [Patterns](#patterns)
    - [Information expert](#information-expert)
    - [Creator](#creator)
    - [Controller](#controller)
    - [Indirection](#indirection)
    - [Low coupling](#low-coupling)
    - [High cohesion](#high-cohesion)
    - [Polymorphism](#polymorphism)
    - [Protected variations](#protected-variations)
    - [Pure fabrication](#pure-fabrication)

## Definition

General Responsibility Assignment Software Patterns/Principles is a set of nine fundamental principles in object design.

First published by Craig Larman in his 1997 book _Applying UML and Patterns_.

> "The critical design tool for software development is a mind well educated in design principles. It is not UML or any other technology. Thus, the GRASP principles are really a mental toolset, a learning aid to help in the design of objectoriented software." - Craig Larman.

## Patterns

### Information expert

> Also known as the _expert principle_. It is related to [high cohesion](#high-cohesion) and [low coupling](#low-coupling) patterns.

It is a principle used to determine where to delegate responsibilities such as methods, computed fields, and so on.

Using this principle, a general approach is to look at a given responsibility, determine the information needed to fulfill it, and then determine where that information is stored.

This will lead to __placing the responsibility on the class with the most information required to fulfill it__.

### Creator

In general, assign class `B` the responsibility to create object `A` if one, or preferably more, of the following apply:

* Instances of `B` contain or compositely aggregate instances of `A`.
* Instances of `B` record instances of `A`.
* Instances of `B` closely use instances of `A`.
* INstances of `B` have the initializing information for instances of `A` and pass it on creation.

### Controller

The controller is the first object beyond the UI layer that receives and coordinates a system operation. It should delegate the work that needs to be done to other objects; it should not do much work itself. 

A use case controller should be used to deal with _all_ system events of a use case, and may be used for more than one use case.

> For instance, for the use cases _Create User_ and _Delete User_, one can have a single class called `UserController`, instead of two separate use case controllers.

### Indirection

Assign the responsibility to an intermediate object to mediate between other components or services so that they are not directly coupled.

The intermediary _creates an indirection_ between other components.

### Low coupling

Low coupling is an evaluative pattern that dictates how to assign responsibilities for the following benefits:

* Lower dependency between the classes.
* Change in one class having a lower impact on other classes.
* Higher reuse potential.

> Coupling is a measure of how strongly one element is connected to, has knowledge of, or relies on other components.

### High cohesion


High cohesion means that the responsibilities of a given set of elements are strongly related and highly focused on a rather specific topics. Breaking programs into classes and subsystems should icnrease the cohesive properties of those.

> High cohesion is an evaluative pattern that attempts to keep objects appropriately focused, manageable and understandable. It is generally used in support of low coupling.

Alternatively, low cohesion is a situation in which a set of elements has too many unrelated responsibilities. Those often suffer from being hard to comprehend, reuse, maintain and change as a whole.

### Polymorphism

When related alternatives or behaviors vary by type (class), assign responsibility for defining the variaton of behaviors based on types to the type for which the behavior varies. This is achievied using polymorphic operations instead of explicit branching based on type.

> Polymorphism has several related meanings. In this context, it means "giving the same name to services in different objects". You can further research this topic with SOLID _Liskov Substitution Principle_ and classic OOP Polymorphism.

### Protected variations

Identify points of predicted variation or instability; assign responsibilities to create a stable interface around them.

This pattern protects elements from the variations on other components by wrapping the focus of instability with an interface and using polymorphism to create various implementations of this interface.

> This favors _Open/Closed principle_ from SOLID.

### Pure fabrication

A pure fabrication is a class that does not represent a concept in the problem domain, specially made up to achieve low coupling, high cohesion, and the reuse potential thereof derived. This kind of class is called a "service" in Domain Driven Design.
