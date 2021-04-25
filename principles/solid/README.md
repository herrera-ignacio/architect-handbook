# SOLID

SOLID is a set of 5 principles that tell us how to arrange our functions and data structures into classes, and how those classes should be interconnected.

> A class is simply a coupled grouping of functions and data, and does not imply these principles are applicable only to object-oriented software.

## The Goal

These principles seek to achieve the creation of mid-level software structures that:

* Tolerate change

* Are easy to understand

* Are the basis of components that can be used in many systems

> The term "_mid-level_" refers to the fact that these principles are applied by programmers working at the _module level_, just above the code level, helping to define the kinds of structures used within modules and components.

> Just as it is possible to create a substantial mess with well-made bricks of code, so it is also possible to create a system-wide mess with well-designed mid-level components. For this reason, above SOLID principles, there are counterparts in the component world and principles of high-level architecture.

## 5 Principles

### [SRP - Single Responsibility Principle](./srp)

The best structure for a software system is _heavily_ influenced by the social structure of the organization that uses it, so that each software module has one, and only one, reason to change.

### [OCP - Open Close Principle](./ocp)

For software systems to be easy to change, they must be designed to allow the behavior to be changed by adding new code, rather than changing existing code.

### [LSP - Liskov Substitution Principle](./lsp)

To build software systems for interchangeable parts, those parts must adhere to a contract that allows those parts to be substituted one for another (Liskov's famous definition of subtypes).

### [ISP - Interface Segregation Principle](./isp)

Software designers should avoid depending on things that they don't use.

### [DIP - Dependency Inversion Principle](./dip)

The code that implements high-level policy should not depend on the code that implements low-level details. Rather, details should depend on policies.
