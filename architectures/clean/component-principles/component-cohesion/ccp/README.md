# Common Closure Principle

> Gather into components those classes that change for the same reasons and at the same times. Separate into different components those classes that change at different times and for different reasons.

## Principle

This is the *Single Responsibility Principle* restated for components. A **component should not have multiple reasons to change**.

## Background

For most applications, **maintainability is more important than reusability**. If the code in an application must change, you would rather that all of the changes occur in one component, rather than being distributed across many components. Other components that don't depend on the changed component do not need to be revalidated or redeployed.

### Relation to OCP

This principle is closely associated with the *Open Closed Principle (OCP)*. Classes should be closed for modification but open for extension. **Because 100% closure is not attainable, closure must be strategic**. We design our classes such that they are closed to the most common kinds of changes that we expect or have experienced. *CCP* amplifies this lesson by gathering together into the same components those classes that are closed to the same types of changes.

> When a change in requirements comes along, that change has a good chance of being restricted to a minimal number of components.
