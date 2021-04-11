# Three Fundamental Principles

* Single Source of Truth
* State is read-only
* Changes are made with pure functions

## Single Source of Truth

> The global state of your application is stored in an object tree within a single store.

This makes it easy to create universal apps, as the state from your server can be serialized and hydrated into the client with no extra coding effort.

## State is read-only

> The only way to change the state is to emit an action, an object describing what happened.

This ensures that neither the views nor the network callbacks will ever write directly to the state. Instead, they express an intent to transform the state. Because all changes are centralized and happen ony by one in a strict order, there are no subtle race conditions to watch out for.

As actions are just plain objects, they can be logged, serialized, stored, and later replayed for debugging or testing purposes.

## Changes are made with pure functions

> To specify how the state tree is transformed by actions, you write pure reducers.

Reducers are just pure functions that take the previous state and an action, and return the next state (a new one, instead of mutating the previous state). Because reducers are just functions, you can control the order in which they are called, pass additional data, or even make reusable reducers for common tasks such as pagination.
