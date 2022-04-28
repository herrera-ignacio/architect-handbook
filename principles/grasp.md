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

### Controller

### Indirection

### Low coupling

### High cohesion

### Polymorphism

### Protected variations

### Pure fabrication
