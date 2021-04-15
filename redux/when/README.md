# When and when not to reach out for Redux

> Resources used:
>  * [Changelog blog post](https://www.changelog.com/posts/when-and-when-not-to-reach-for-redux)
>  * [Redux docs](https://redux.js.org/understanding/thinking-in-redux/motivation)
>  * [Medium blog post](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367)

* Redux Origins & Motivations
* Redux vs Context Now
* Redux Use Cases Now
* Redux Tradeoffs
* Ask yourself

## Redux origins

Redux was invented as an implementation of the _Flux architecture_), which was in turn created to deal with limitations people had found in event-trigger-based state management, like Backbone specifically.

> As requirements for JS single-page applications have become increasingly complicated, __our code must manage more state than ever before__.

So I set `user.firstName`, it triggers a "change firstName" event, some other code is listening to that, it triggers another event...

Next thing you know, you're 15 events down one big synchronous call stack, and you have no idea why this happened in the first place. That's what Flux was invented to solve, and Redux basically perfected that particular approach. And that was the problem people were trying to solve in 2015.

> At some point, you no longer understand what happens in your app as you have __lost control over the when, why, and how of its state__. When a system is opaque and non-deterministic, it's hard to reproduce bugs or add new features.

Now, it also happens that because Redux used the _old-style React Context API_ from its beginning, using Redux in a React app also accidentally solve another common problem, which is that _many different parts of my app need to use the same state at the same time, and I would normally have to lift that state up maybe all the way to the root app component_ in order for many components to share the data. But if I do that, I would then have to _prop-drill_ and pass that data as props through every level of the component tree.

> __We're mixing two concepts: mutation and asynchronicity__.

> Following in the steps of Flux, CQRS, and Event Sourcing, __Redux attempts to make state mutations predictable__ by imposing certain restrictions on how and when updates can happen ([three principles of Redux](../three-principles)). 

## Redux vs Context Now

With React 16.3, it came a new, improved Context API, which unlike the old one, was recommended for production usage from the day it came out. And __the only purpose of Context is to act as a dependency injection mechanism scoped to some portion of your subtree__.

> So if the only thing you need to do with Redux is avoid passing data as props through 15 levels of your components, that's literally what Context was invented to do.

__Context is not a state management system but a dependency injection mechanism__. Most often you are the one managing that state in a React Component, with the `useState` hook or the `useReducer` hook. And you're the one deciding where the state lives, handling how to update it, and then putting the value into Context for distribution.

So, `useReducer` plus `useContext` together kind of make up a state management system more equivalent to what Redux does with React.

## Redux Use Cases Now

* Data caches.
* Things that are like "global variables" (e.g. authentication).
* Things that have a very complex update logic (e.g. a multimedia post editor).
* Things that many distant components care about.
* In general, when the state tree shape is too different from the UI tree shape.

But it's probably not going to be the best or most efficient tool at any of those use cases. It might not be quite the best at all of them, but you can do lots of different things.

## Redux Tradeoffs

* Describe application state as plain objects and arrays.

* Describe changes in the system as plain objects.

* Describe the logic for handling changes as pure functions.

None of these limitations are required to build an app, with or without React. In fact these are pretty strong constraints, and you should think carefully before adopting them even in parts of your app.

These limitations help build apps that:

* Persist state to a local storage and then boot up from it, out of the box.

* Pre-fill state on the server, send it to the client in HTML, and boot up from it, out of the box.

* Serialize user actions and attach them, together with a state snapshot, to automated bug reports (`redux-bug-reporter`).

* Pass action objects over the network ot implement collaborative environments without dramatic changes to how the code is written (`redux-swarmlog`).

* Maintain an undo history or implement optimistic mutations without dramatic changes to how the code is written. 

* Travel between state history in development, and re-evaluate the current state from the action history when the code changes (`redux-devtool`).

* Provide full inspection and control capabilities to the development tooling so that product developers can build custom tools (`redux-devtools-chart-monitor`).

* Provide alternative UIs while reusing most of the business logic.

## Ask yourself

* Do other parts of the application care about that state?

* Do you need to be able to derive data from that state?

* Is the same data being used to derive multiple components/features?

* Is there value to you, to being able to restore the state to a given point in time?

* Do you want to cache the data, i.e: reload it from state if it's already there instead of requesting it again?
