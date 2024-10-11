# The Test Boundary

* Overview
* Design for testability
* Testing API
  * Structural Coupling
  * Security

## Overview

The tests are *part of the system*, and they participate in the architecture just like every other part of the system does.

Tests, by their very nature, follow the *Dependency Rule*, they are very detailed and concrete, and they always depend inward toward the code being tested. In fact, you can think of the tests as the outermost circle in the architecture.

Tests are also *independently deployable*. They are the *most isolated system component*. No user depends on them, and they are not necessary for system operation. Their roles is to support development, not operation.

## Design for testability

Tests that are not well integrated into the design of the system tend to be fragile, and they make the system rigid and difficult to change. The issue is *coupling*. Tests that are strongly coupled to the system must change along with the system. Even the most trivial change to a system component can cause many coupled tests to break or require changes.

> Changes to common system components can cause hundreds, or even thousands, of tests to break. This is known as the [*Fragile Tests Problem*](../fragile-tests).

The first rule of software desig, whether for testability or for any other reason, is always the same: *Don't depend on volatile things*.

## Testing API

To avoid the Fragile Test Problem, you can create a specific API that the tests can use to verfiy all the business rules. This API should have superpowers that wllow the tests to avoid security constraints, bypass expensive resources (such as databases), and force the system into particular testable states. This API will be a superset of the suite of *interactors* and *interface adapters* that are used by the user interface.

The purpose of the testing API is to decouple the *structure* of the tests from structure of the application.

### Structural Coupling

Imagine a test suite that has a test class for every production class, and a set of test methods for every production method. Such a test suite is deeply coupled to the structure of the application.

When one of those production methods or classes changes, a large number of tests must change as well. Consequently, the tests are fragile, and they make the production code rigid.

The role of the testing API is to *hide the structure of the application from the tests*. This allows the production code to be refactored and evolved in ways that don't affect the tests. It also allows the tests to be refacotred and evolved in ways that don't affect the production code.

### Security

The superpowers of the testing API could be dangerous if they were deployed in production systems, thus they should be kept in a separate, independently deployable component.
