# Clean Architecture

The Clean Architecture style aims for a loosely coupled implementation focused on use cases and it is summarized as:

1. It is an architecture style where the _Use Cases_ are the centran organizing structure.

2. Follows the _Ports and Adapters_ pattern.
  * Implementation guided by tests (TDD Outside-In).
  * Decoupled from technology details.

3. Follows lots of principles (_Stable Abstractions Principle_, _Stable Dependencies Principle_, _SOLID_, and so on).

## Uses Cases

Use Cases are algorithms that interpret the input to generate the output data, their implementation should be closer as possible to the business vocabulary.

A set of use cases is used to describe software.
