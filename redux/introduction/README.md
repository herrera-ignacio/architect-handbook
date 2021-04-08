# Redux Introduction

* What is Redux?
* Why should I use Redux?
* When should I use Redux?
* Core Terminology
  * State Management
  * Immutability
  * Actions
  * Action Creators
  * Reducers
  * Store
  * Dispatch
  * Selectors

## What is Redux/

Redux is a pattern and library for __managing and updating application state__, using events called "actions". It serves as a __centralized__ store for state that needs to be used across your entire application, with rules ensuring that the state can only be updated in a __predictable__ fashion.

## Why should I use Redux?

Redux helps you manage "global" state (state that is needed across many parts of your application).

The patterns and tools provided by Redux make it easier to understand when, where, why, and how the state in your application is being updated, and how your application logic will behave when those changes occur.

Redux guides you towards writing code that is predictable and testable.

## When should I use Redux?

There are more concepts to learn, and more code to write. It also adds some indirection to your code, and asks you to follow certain restrictions. It's a trade off between short term and long term productivity:

* You have large amounts of application state that are needed in many places in the app.

* The app state is updated frequently over time.

* The logic to update the state may be complex.

* The app has a medium or large-sized codebase, and might be worked on by many people.

## Core Terminology

> Take a look at [Redux Documentation](https://redux.js.org/tutorials/essentials/part-1-overview-concepts#redux-terms-and-concepts).

### State Management

In a self-contained app with the following parts:

* __State__: Source of truth that drives our app.

* __View__: Declarative description of the UI based on the current state.

* __Actions__: Events that occur based on user input, and trigger updates in the sate.

#### Traditional way

We can observe a __"one-way data flow"__:

* State describes condition of the app at a specific point in time.

* UI is rendered based on that state.

* When something happens, the state is updated based on what occurred.

* UI re-renders based on the new state.

![one-way data flow](https://redux.js.org/assets/images/one-way-data-flow-04fe46332c1ccb3497ecb04b94e55b97.png)

However, the simplicity can break down when we have __multiple components that need to share and use the same state__, especially if those components are located in different parts of the application. Somethimes this can be solved by __"lifting state up"__ to parent components, but that doesn't always help.

One way to solve this is to extract the shared state from the components, and put it into a centralized location outside the component tree. With this, our component tree becomes a big "view" and any component can access the state or trigger actions, no matter where they are in the tree.

By defining and separating the concepts involved in state management and enforcing rules that maintain independence between views and states, we give our code more structure and maintainability.

This is the basic idea behind Redux: __a single centralized place to contain the global state in your application, and specific patterns to follow when updating the state to make the code predictable__.

#### Redux way

![redux flow](https://redux.js.org/assets/images/ReduxDataFlowDiagram-49fa8c3968371d9ef6f2a1486bd40a26.gif)

### Immutability

In order to update values immutably, your code must make _copies_ of existing objects/arrays, and then modify the copies. __Redux expects that all state updates are done immutably__.

### Actions

An __action__ is a plain JavaScript object that has a `type` field. You can think of an action as an __event that describes something that happened in the application__.

The `type` field should be a string that gives this action a descriptive name. We usually write that type string like `"domain/eventName"`.

An action object can have other fields with additional information about what happened. By convention, we put that information in a field called `payload`.

```javascript
const addTodoAction = {
  type: 'todos/todoAdded',
  payload: 'Buy milk'
}
```

### Action Creators

An __action creator__ is a function that creates and returns an action object. We typically use these so we don't have to write the action object by hand every time.

```js
const addTodo = text => {
  return {
    type: 'todos/todoAdded',
    payload: text
  }
}
```

### Reducers

A __reducer__ is a function that receives the current `state` and an `action` object, decides how to update the state if necessary, and returns the new state: `(state, action) => newState`. You can think of a reducer as an __event listener which handles events based on the received action (event) type__.

Reducers must _always_ follow some specific rules:

* They should only calculate the new state value based on the `state` and `action` arguments.

* They are not allowed to modify the existing `state`. Instead, they must make _immutable updates_, by copying the existing `state` and making changes to the copied values.

* They must not do any asynchronous logic, calculate random values, or cause other "side effects".