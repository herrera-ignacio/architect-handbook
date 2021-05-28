# The Main Component

In every system, there is at least one component that creates, coordinates, and oversees the others.

The `Main` component is the *ultimate detail*, the lowest-level policy. It is the initial entry point of the system. It's job is to *create everything needed and then hand control over to the high-level abstract portions of the system*.

It is in this `Main` component that dependencies should be injected by a Dependency Injection framework. `Main` should distribute those dependencies normally, without using the framework.

> Think of `Main` as the dirtiest of all the dirty components. `Main` is a dirty low-level module in the *outermost circle* of the clean architecture.

Think of `Main` as a *plugin* that *sets up initial conditions and configurations, gathers all the outside resources* and then hands control over to the high-level policy of the application. Since it is a plugin, it is possible to have many `Main` components, one for each configuration of your application.

> For example, you could have a `Main` plugin for *Dev*, another for *Test*, and yet another for *Production*. You could also have one for each country you deploy to, or each jurisdiction, or each cvustomer.

When you thing about `Main` as a plugin component, sitting behind an architectural boundary, the problem of configuration becomes a lot easier to solve.
