# HTTP Methods

- [HTTP Methods](#http-methods)
  - [Native HTTP Actions](#native-http-actions)
  - [Semantics of HTTP APIs](#semantics-of-http-apis)

## Native HTTP Actions

- GET (Safe & Idempotent)
- POST
- PUT (Idempotent)
- DELETE (Idempotent)
- HEAD
- OPTIONS
- TRACE
- CONNECT

__Safe__ means that, when requested, it does not modify or cause any side effects on the state of the resource.

__Idempotent__ means that, response stays the same, regardless of the number of times it is requested.

## Semantics of HTTP APIs

- __GET__: Get a representation of the targer resource's state.

- __POST__: Let the target resource process the representation enclosed in the request.

- __PUT__: Set the target resource's state to the state defined by the representation enclosed in the request.

- __DELETE__: Delete the target resource's state.
