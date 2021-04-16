# Component Cohesion Principles

> Cohesion is a measure of the degree to which the elements of the module are functionally related.

> It is the degree to which all elements directed towards performing a single task are contained in the component. Basically, cohesion is the internal glue that keeps the module together.


* [REP: Reuse/Release Equivalence Principle](./rep.md)
* [CCP: Common Closure Principle](./ccp.md)
* [CRP: Common Reuse Principle](./crp.md)

## Cohesion and design principles

Today we have a much more complex variety of cohesion that a module performs one, and only one, function.

If the Design Principles, such as SOLID, tell us how to arrange the bricks into walls and rooms, then the component principles tell us how to arrange the rooms into buildings.

> A good software design will have high cohesion.

Large software systems, like large buildings, are build out of smaller components.

In choosing the classes to group together into components, we must consider the opposing forces involved in reusability and develop-ability. Balancing these forces with the needs of the application is nontrivial. Moreover, the balance is almost always dynamic.