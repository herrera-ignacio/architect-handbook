# Redux Best Practices

> This is a selection from [Redux Official Style Guide](https://redux.js.org/style-guide/style-guide).

* Do Not Mutate State
* Reducers Must Not Have Side Effects
* Do Not Put Non-Serializable Values in State or Actions
* Only One Redux Store Per App
* Structure Files as Feature Folders with Single-File Logic
* Put as Much Logic as Possible in Reducers
* Reducers Should Own the State Shape
* Treat Reducers as State Machines
* Normalize Complex Nested/Relational State
* Model Actions as Events, Not Setters / Meaningful Action Names
* Allow Many Reducers to Respond to the Same Action
* Avoid Dispatching Many Actions Sequentially

## Do Not Mutate State

Mutating state is the most common cause of bugs in Redux applications, including components failing to re-render properly, and will also break time-travel debugging in the Redux DevTools. __Actual mutation of state values should always be avoided__, both inside reducers and in all other application code.

> Use tools such as [redux-immutable-state-invariant](https://github.com/leoasis/redux-immutable-state-invariant) to catch mutations during development and [Immer](https://immerjs.github.io/immer/) to avoid accidental mutations in state updates.

It's okay to modify _copies_ of existing values, that is a normal part of writing immutable update logic.
Reducers Should Own the State Shapeuld _only_ depend on their `state` and `action` arguments, and you should only calculate and return new state value based on those arguments. They must not execute any kind of asynchronous logic (AJAX calls, timeouts, promises), generate random values, modify variables outside the reducer, or run other code that affects things outside the scope of the reducer function.

> It is acceptable to have a reducer call other functions that are defined outside of itself, such as imports from libraries or utility functions, as long as they follow the same rules.

The purpose of this rule is to guarantee that reducers will behave predictably when called.

> For example, if you are doing time-travel debugging, reducer functions may be called many times with earlier actions to produce the "current" state value. If a reducer has side effects, this would cause those effects to be executed during the debugging process, and result in the application behaving in unexpected ways.

> There are some gray areas to this rule. Strictly speaking, code such as `console.log(state)` is a side effect, but in practice has no effect on how the application behaves.

## Do Not Put Non-Serializable Values in State or Actions

Avoid putting non-serializable values such as Promises, Symbols, Maps/Sets, functions, or class instances into the Redux store state or dispatched actions.

This ensures that capabilities such as debugging via the Redux DevTools will work as expected. It also ensures that the UI will update as expected.

> You may put non-serializable values in actions _if_ the action will be intercepted and stopped by a middleware before it reaches the reducers. Middleware such as `redux-thunk` and `redux-promise` are examples of this.

## Only One Redux Store Per App

A standard Redux application should only have a single Redux store instance, which will be used by the whole application.

It should typically be defined in a separate file such as `store.js`.

Ideally, no app logic will import the store directly. It should be passed to a React component tree via `<Provider>`, or referenced indirectly via middleware such as thunks. 

## Structure Files as Feature Folders with Single-File Logic

Redux itself does not care about how your application's folders and files are structured. However, co-locating logic for a given feature in one place typically makes it easier to maintain that code.

Because of this, it is recommended that most application should structure files using a __"feature folder" approach__ (all files for a feature in the same folder). Within a given feature folder, the Redux logic for that feature should be written in a single "slice" file, preferably using the Redux Toolkit `createSlice` API.

> This is also known as the "__ducks__" pattern.

> While older Redux codebases often used a __"folder-by-type" approach__ with separate folders for "actions" and "reducers", keeping related logic together makes it easier to find and update that code.

An example folder structure might look something like:

* `/src`
  * `index.tsx`: Entry point file that renders the React component tree.
  * `/app`: contains app-wide setup and layout that depends on all the other folders.
    * `store.ts`: store setup.
    * `rootReducer.ts`: root reducer (optional).
    * `App.tsx`: root React component.
  * `/common`: contains truly generic and reusable utilities and components, such as hooks, generic components, utils, etc.
  * `/features`: contains all "feature folders".
    * `/todos`: a single fature folder.
      * `todosSlice.ts`: Redux reducer logic and associated actions.
      * `Todos.tsx`: a React component.

## Put as Much Logic as Possible in Reducers

Wherever possible, try to put as much of the logic for calculating a new state into the appropriate reducer, rather that in the code that prepares and dispatches the action (like a click handler).

Reducers are always easy to test, because they are pure functions. So the more logic you can put in a reducer, the more logic you have that is easily testable.

> There are valid cases where some or all of the new state should be calculated first (such as generating a unique ID), but that should be kept to a minimum.

Redux state updates must always follow _the rules of immutable updates_. Most Redux users realize they have to follow these rules inside a reducer, but it's not obvious that you _also_ have to do this if the new state is calculated _outside_ the reducer. This can easily lead to mistakes like accidental mutations, or even reading a value from the Redux store and passing it right back inside an action. Doing all of the state calculations in a reducer avoids those mistakes.

Finally, putting logic in reducers means you know where to look for the update logic, instead of having it scattered in random other parts of the application code.

## Reducers Should Own the State Shape

The Redux root state is owned and calculated by the single root reducer function. For maintainability, that reducer is intended to be split up by key/value "slices", with each _"slice reducer"_ being responsible for providing an initial value and calculating the updates to that slice of the state.

In addition, slice reducers should exercise control over what other values are returned as part of the calculated state. __Minimize the use of "blind spreads/returns"__ like `return action.payload` or `return { ...state, ...action.payload }`, because those rely on the code that dispatched the action to correctly format the contents, and the reducer effectively gives up its ownership of what the state looks like.

> A "spread return" reducer may be a reasonable choice for scenarios like editing data in a form, where writing a separate action type for each individual field would be time-consuming and of little benefit.

> Use of static typing does make "blind spreads/returns" and somewhat more acceptable. If the reducer knows the `action` is a `PayloadAction<User>`, then it _should_ be safe to do `return action.payload`.

## Treat Reducers as State Machines

Many Redux reducers are written "unconditionally". They only look at the dispatched action and calculate a new state value, without basing any of the logic on what the current state might be. This can cause bugs, as some actions may not be "valid" conceptually at certain times depending on the rest of the app logic.

> For example, a "request succeeded" action should only have a new value calculated if the state says that it's already "loading", or an "update this item" action should only be dispatched if there is an item kared as "being edited".

To fix this, treate reducers as "state machines", where the __combination of both the current state _and_ the dispatched action determines whether a new state value is actually calculated__, not just the action itself unconditionally.

> A finite state machine is a useful way of modeling something that should only be in one of a finite number of "finite states" at any time.

Since you're defining behavior per state instead of per action, you also prevent impossible transitions, and you can enforce that, instead of accidentally introducing edge-cases.

## Normalize Complex Nested/Relational State

Many applications need to cache complex data in the store. That data is often received in a nested form from an API, or has relations betweens different entities in the data (such as a blog that contains Users, Posts, and Comments).

Prefer storing that data in a "normalized" form in the store. This makes it easier to look up items based on their ID and update a single item in the store, and ultimately leads to better performance patterns.

## Model Actions as Events, Not Setters / Meaningful Action Names

Redux does not care what the contents of the `action.type` feild are, it just has to be defined.

It is recommended trying to treat actions more as __"describing events that occurred"__, rather than "setters". Treating actions as "events" generally leads to more meaningful action names, fewer total actions being dispatched, and a more meaningful action log history.

Actions should be written with meaningful, informative, descriptive type fields. Ideally, you should be able to read through a list of dispatched action types, and have a good understanding of what happened in the application without even looking at the contents of each action.

## Allow Many Reducers to Respond to the Same Action

You are encouraged to have many reducer functions all handle the same action separately if possible.

In practice, experience has shown that most actions are typically only handled by a single reducer function, which is fine. But, modeling actions as "events" and allowing many reducers to respond to those actions will typically allow your application's codebase to scale better, and minimize the number of times you need to dispatch multiple actions to accomplish one meaningful update.

## Avoid Dispatching Many Actions Sequentially

Avoid dispatching many actions in a row to accomplish a larger conceptual "transaction". This is legal, but will usually result in multiple relatively expensive UI updates, and some of the intermediate states could be potentially invalid by other parts of the application logic.

Prefer dispatching a single "event"-type action that results in all of the appropriate state updates at once, or consider use of action batching addons to dispatch multiple actions with only a single UI update at the end.

> Each dispatched action does result in execution of all store subscription callbacks, and will usually result in UI updates.

> If multiple dispatches are truly necessary, consider batching the updates in some way. Depending on your use case, this may just be batching React's own renders (possibly using `batch()` from `react-redux`), debouncing the store notification callbacks, or grouping many actions into a larger single dispatch that only results in one subscriber notification.