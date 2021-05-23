# Stable Abstractions Principle

> A component should be as abstract as it is stable.

## Principle

A stable component should also be abstract so that its stability does not prevent it from being extended. On the other hand, it says that an unstable component should be concrete since its instability allows the concrete code within it to be changed.

Thus, if a component is to be stable, it should consist of *interfaces* and *abstract classes* so that it can be extended. Stable components that are extensible and flexible do not overly constrain the architecture.

## Background

Software that represents **high-level architecture and policy decisions should not change very often**. Thus, this software should be placed in **stable components**.

However, if high-level policies are placed into stable components, the source code that represents those policies will be difficult to change. This could make the overall architecture inflexible. *Abstract classes* are flexible enough to be extended without requiring modification, complying with *Open-Closed Principle*.