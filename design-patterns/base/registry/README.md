# Registry

> A well-known object that other objects can use to find common objects and services.

* Overview
* How It Works
  * Interface
  * Implementation
* When to Use It

## Overview

![](2021-07-28-01-06-17.png)

You may know an object's ID number but not have a reference. A *Registry* acts as a global object (or at least looks like one) and **provides finder methods**.

## How It Works

* You have to think about the design of a *Registry* in terms of interface and implementation.

### Interface

* Static methods prefered.
* Data shouldn't be in static fields unless they're constants.

### Implementation

You should consider data's scope. Different scopes call for different implementations,.

* For a **process-scoped** *Registry*, the usual option is a *Singletion*.
* For a **thread-scoped** *Registry*, you need some form of thread-specific storage, such as a dictionary keyed by thread.
* For **session-scoped** data you can also use a dictionary lookup with session IDs, but the ID can be put into a thread-scoped registry when a request begin.

Some applications may have a single *Registry*; some may have several. Registries are usually divided up by system layer or by execution context.

## When to Use It

You should only use a *Registry* as a last resort, because despite the encapsulation of a method, a *iRegistry* is still global data.

There are alternatives:

* *Pass around any widely needed data in parameters*. The problem with this is that parameters are added to method calls where they aren't needed by the called method but only by some other method that's called several layers deep in the call tree.

* *Add a reference to the common data to objects when they're created*. Although this leads to an extra parameter in a constructor, and it's still more trouble thatn it's often worth, but if you have data that's only used by a subset of classes, this technique allows you to restrict things that way.
