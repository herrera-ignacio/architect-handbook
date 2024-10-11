# Acyclic Dependencies Principle

> Allow no cycles in the component dependency graph.

* The Weekly Build Problem
* Elimnating Dependency Cycles
  * Breaking the Cycle
* Top-Down Design

## The Weekly Build Problem

Used to be common in medium-sized projects. All the developers ignore each other for the first four days of the week. They all work on private copies of the code, and don't worry about integrating their work on a collective basis. Then, on Friday, they integrate all their changes and build the system.

This approach has the wonderful advantage of allowing the developers to live in an isolated world for four days out of five. The disadvantage, is the large integration penalty on the fifth day.

As the duty cycle of development versus integration decreases, the efficiency of the team decreases, too. **The integration time continues to grow with project size**. Integration and testing become increasingly harder to do, and team loses the benefit of rapid feedback.

## Eliminating Dependency Cycles

The solution is to **partition the development enviornment into releasable components**.

The components become units of work that can be the responsibility of a single developer, or a team of developers. When developers get a component working, they release it for use by the other developers. They then continue to modify their component in their own private areas.

As new releases of a component are made available, other teams can decide whether they will immediately adopt the new release. Thus no team is at the mercy of the others.

> Changes made to one component do not need to have an immediate affect on other teams.

You **must manage the dependency structure of the components. There can be no cycles**. If not, *"morning after syndrome"* cannot be avoided.

**Dependency structure should be a _direct graph_**. The components are the *nodes*, and the dependency relationships are the *directed edges*. No matter which component you begin at, it should be impossible to follow the dependency relationships and wind up hack at that component. This **structure has no cycles**. it is a **directed acycle graph (DAG)**.

> Comonent structure is volatile in the presence of changing requirements and must always be monitored for cycles. When cycles occur, they must be broken somehow.

### Breaking the cycle

1. Apply the *Dependecy Inversion Principle (DIP)*.
2. Create new component where you need to break the dependency.

## Top-Down Design

The **component structure cannot be designed from the top down**. it is not one of the first things about the system that is designed, but rather **evolves as the system grows and changes**.

Component dependency diagrams have very little to do with describing the function of the application. Instead, they are a map to the *buildability* and *maintainability* of the application. As more modules accumulate in the early stages of implementation and design, there is a growing need to manage the dependencies so that the project can be developed without the *"morning after syndrome"*.
