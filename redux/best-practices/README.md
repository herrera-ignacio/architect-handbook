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
* Connect More Components to Read Data from the Store
* Call `useSelector` Multiple Times in Function Components
* Use Plain JavaScript Objects For State
* Write Action Types as `domain/eventName`
* Write Actions Using the Flux Standard Action (FSA) Convention
* Use Thunks for Async Logic
* Use Selector Functions to Read from Store State
* Name Selector Functions as `selectThing`
* Avoid Putting Form State In Redux

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

## Connect More Components to Read Data from the Store

Prefer having more UI components subscried to the Redux store and reading data at a more granular level. This typically leads to better UI performance, as fewer components will need to render when a given piece of state changes.

For example, rather than just connecting a `<UserList>` component and reading the entire array of users, have `<UserList>` retrieve a list of all user IDs, render list tems as `<UserListItem userId={userId}>`, and have `<UserListItem>` be connected and extract its own user entry from the store.

## Call `useSelector` Multiple Times in Function Components

When retrieving data using the `useSelector` hook, prefer calling `useSelector` many times and retrieving smaller amounts of data, instead of having a single larger `useSelector` call that returns multiple results in an object. Unlike `mapState`, `useSelector` is not required to return an object, and having selectors read smaller values means it is less likely that a given state change will cause this component to render.

However, try to find an appropriate balance of granualarity. If a single component does need all fields in a slice of the state, just write one `useSelector` that returns the whole slice instead of separate selectors for each individual field.

## Use Plain JavaScript Objects For State

Prefer using plain JS objects and arrays for your state tree, rather than specialized libraries like _Immutable.js_. While there are some potential benefits to using _Immutable.js_, most of the commonly stated goals such as easy reference comparisons are a property of immutable updates in general, and do not require a specific library. This also keeps bundle sizes smaller and reduces complexity from data type conversions.

It is specifically recommended using Immer if you want to simplify immutable update logic, specifically as part of Redux Toolkit.

Immtuable.js has been semi-frequently used in Redux apps since the beginning. There are several common reasons stated for using Immutable.js:

* Performance improvements from cheap reference comparisons.

* Performance improvements from making updates thanks to specialized data structures.

* Prevention of accidental mutations.

* Easier nested updates.

There are some valid aspects to those reasons, but in practice, the benefits aren't as good as stated, and there's multiple negatives to using it:

* Cheap reference comparisons are a property of any immutable updates, not just _Immutable.js_.

* Accidental mutations can be prevented via other mechanisms, such as using _Immer_ or `redux-immutable-state-invariant`.

* Immer allows simpler update logic overall, eliminating the need for specific libraries APIs.

* Immutable.js has a very large bundle size, and API is fairly complex.

* Libraries APIs "infects" your application code. All logic must know whether it's dealing with plain JS objects or Immutable objects.

* Converting from Immutable.js objects to plain JS objects is relatively expensive, and always produce completely new deep object references.

The strongest remaining reason to use Immutable.js is fast updates of _very_ large objects (tens of thousands of keys). Most applications won't deal with objects that large.

Overall, Immutable.js adds too much overhead for too little practical benefit. Immer is much better option.

## Write Action Types as `domain/eventName`

Redux Toolkit's `createSlice` function currently generates action types that look like `"domain/action"`, such as `"todos/addTodo"`. It is encouraged this convention for readability.

## Write Actions Using the Flux Standard Action (FSA) Convention

The original "Flux Architecture" documentation only specified that action objects should have a `type` field, and did not give any further guidance on what kinds of fields or naming conventions should be used for fields in actions. To provide consistency, Andrew Clark created a convention called ["Flux Standard Actions"](https://github.com/redux-utilities/flux-standard-action) early in Redux's development. 

Summarized, the FSA convention says that actions:

* Should always put their data into a `payload` field.

* May have a `meta` field for additional info.

* May have an `error: true` field to indicate the action represents a failure of some kind, and use the same action type as the "valid" form of the action. In practice, most developers write separate action types for the "success" and "error" cases. Either is acceptable.

Redux Toolkit generates action creators that match the FSA format, and it is prefered using FSA-formatted actions for consistency.

## Use Thunks for Async Logic

The middleware API was specifically created to allow different forms of async logic to be plugged into the Redux store.

It is recommended __using the Redux Thunk middleware by default__, as it is sufficient for most typical use cases (such as basic AJAX data fetching). In addition, use of the `async/await` syntax in thunks makes them easier to read.

If you have truly complex async workflows that involve things like cancelation, debouncing, running logic after a given action was dispatched, or "background-thread"-type behavior, then consider adding more powerful async middleware like __Redux-Saga__ or __Redux-Observable__.

## Use Selector Functions to Read from Store State

"Selector functions" are a powerful tool for encapsulating reading values from the Redux store state and deriving ruther data from those values.

It is strongly recommended __using memoized selector functions for reading store state whenever possible__, and recommended creating those selectors with __Reselect__.

Find a reasonable balance for granularity, based on how often fields are accessed and updated, and how much actual benefit the selectors are providing in your application.

## Name Selector Functions as `selectThing`

It is recommended __prefixing selector function names with the word `select`__, combined with a description of the value being selected.

> Examples of this would be `selectTodos`, `selectVisibleTodos`, and `selectTodoById`.

# Avoid Putting Form State In Redux

Most form state shouldn't go in Redux. __In most use cases, the data is not truly global, is not being cached, and is not being used by multiple components at once__.

In addition, connecting forms to Redux often involves dispatching actions on every single change event, which causes performance overhead and provides no real benefit.

Even if the data ultimately ends up in Redux, prefer keeping the form edits themselves in local component state, and only dispatching an action to update the Redux store once the user has completed the form.

There are use cases when keeping form state in Redux does actually make sense, such as WYSIWYG live prefies of edited item attributes. But, in most cases, this isn't necessary.
