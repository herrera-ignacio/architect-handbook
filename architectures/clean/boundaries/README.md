# Boundaries

* Overview
* Implementation
* Boundary Crossing
* What Data Crosses The Boundaries
* Monolith example

## Overview

> Software architecture is the art of drawing lines called *boundaries*. The architecture of the system is defined by a set of software components and the boundaries that separate them.

Boundaries separate software elements from one another, and restrict those on one side from knowing about those on the other.

> You draw lines between things that matter and things that don't. The GUI doesn't matter to the business rules, so there should be a line between them. The database doesn't matter to the GUI, so there should be a line between them.

Some boundaries are drawn very early in a project's life, even before any code is written. Others are drawn much later. Those that are drawn early are *drawn for the purposes of deferring decisions for as long as possible*, and of keeping those decisions from polluting the core business logic.

![](2021-05-26-01-51-52.png)

> Note the two arrows leaving `DatabaseAccess` class. That means that none of these classes knows the class exists.

## Implementation

> Boundaries objects are _Interfaces_, that are implemented usually by Interactors.

![example](https://i.imgur.com/WkBAATy.png)

Data goes into an Interactor, through Boundary, and goes out from an Interactor also through a Boundary.

## Boundary Crossing

At runtime, a boundary crossing is nothing more than a function on one side of the boundary calling a function on the other side and passing along some data. The trick to creating an appropriate boundary crossing is to *manage source code dependencies*.

![](../CleanArchitecture.jpg)

At the lower right of the diagram is an example of how we cross the circle boundaries. It shows the _Controllers_ and _Presenters_ communicating with the _Use Cases_ in the next layer. It begins in the controller, moves through the use case, and then winds up executing in the presenter. Note also the source code dependencies. Each one points inwards towards the use cases.

> We usually resolve this apparent contradiction by using the __Dependency Inversion Principle__.

In a language like Java, for example, we would arrange interfaces and inheritance relationships such that the source code dependencies oppose the flow of control at just the right points across the boundary.

> For example, consider that the use case needs to call the presenter. However, this call must not be direct because that would violate _The Dependency Rule_. No name in an outer circle can be mentioned by an inner circle. So we have the use case call an interface (_Use Case Output Port_) in the inner circle, and have the presenter in the outer circle implement it.

The same technique is used to cross al the boundaries in the architectures. We take advantage of dynamic polymorphism to create source code dependencies that oppose thw flow of control so that we can conform to _The Dependency Rule_ no matter what direction the flow of control is going in.

## Which Data Crosses The Boundaries

Typically the data that crosses the boundaries is simple data structures. You can use basic structs or _Data Transfer_ objects if you like. The important thing is that __isolated, simple, data structures are passed across the boundaries__. We don't want the data to have any kind of dependency that violates _The Dependency Rule_.

For example, many database frameworks return a convenient data format in response to a query. We might call this a `RowStructure`. We don't want to pass that row structure inwards across a boundary. That would violate _The Dependency Rule_ because it would force an inner circle to know something about an outer circle.

So when we pass data across a boundary, __it is always in the form that is most convenient for the inner circle__.

## Monolith Example

The simplest and most common of the architectural boundaries has no strict physical representation. It is simply a disciplined segregation of functions and data within a single processor and a single address space.

When a higher-level client needs to invoke a lower-level service, dynamic polymoprhism is used to invert the dependency against the flow of control. *The runtime dependency opposes the compile-time dependency*.

![](2021-05-26-11-18-39.png)

In the figure, the flow of control crosses the boundary from left to right. The `Client` calls function `f()` on the `Service`. It passes along an instance of `Data` (data structure). The `Data` may be passed as a function argument or by some other more elaborate means. Note that the definition of the `Data` is on the *called* side of the boundary.

> The boundary is crossed as flow of control, from a higher level to a lower level. We want to avoid this.

![](2021-05-26-11-25-33.png)

In the latest figure, the flow of control crosses the boundary from left to right as before. The high-level `Client` calls the `f()` function of the lower level `ServiceImpl` through the `Service` interface. Note, however, that all dependencies cross the boundary from right to left *toward the higher-level component*. Note, also, that the definition of the data structure is on the calling side of the boundary.

> Crossing the boundary against the flow of control allows higher-level components to remain independent of lower-level details.
