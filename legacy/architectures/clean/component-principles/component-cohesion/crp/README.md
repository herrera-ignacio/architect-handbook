# Common Reuse Principle

## Principle

> Don't force users of a component to depend on things they don't need.

Classes and modules that tend to be reused together belong in the same component.

## Background

Reusable classes collaborate with other classes that are part of the **reusable abstraction**. CRP states that those belong together. In such a component, we would expect to see classes that have lots of dependencies on each other.

> A simple example might be a container class and its associated iterators.

When one component uses another, a **dependency is created** between the components. Perhaps the *using* component uses only one class within the *used* component, but that still doesn't weaken the dependency. Because of that dependency, every time the *used* component is changed, the *using* component will likely need corresponding changes. This is true even if the *using* component doesn't care about the changes made in the *used* component.

Thus, when we depend on a component, we want to make sure we depend on every class in that component. Put another way, we want to make sure that the **classes that we put into a component are inseparable** (that it is impossible to dpeend on some and not on the others).

Therefore the CRP tells us more about which classes *shouldn't* be together than about which classes *should* be together.

> The CRP says that classes that are not rightly bound to each other should not be in the same component.

### Relation to ISP

The *CRP* is generic version of the *ISP*. The ISP advises us not to depend on classes that have methods we don't use. The CRP advises us not to depend on components that have classes we don't use.

> Don't depend on things you don't need.
