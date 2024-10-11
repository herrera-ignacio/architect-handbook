# Flux

- [Flux](#flux)
  - [The Need for Flux](#the-need-for-flux)
  - [How Flux Works](#how-flux-works)

> I don't agree with most of this; I consider Facebook's description of MVC to be erratic. If you are interested about this point of view, I invite you to read my notes on [MVC - Unidirectional Data Flow](../../design-patterns/web-presentation/mvc).

## The Need for Flux

In 2011, Facebook engineers had a problem, __the zombie notification__: users would see they had a chat notification, but when they clicked on it there would be no new message waiting for them. Each solution would only address some particular edge case.

The problem was that at that time, Facebook was using the MVC architecture, which was becoming increasingly unstable as the application grew more and more complicated.

![mvc](./mvc.png)

The number of models and views had compunded, and the the relationships between them had become unmanageably difficult to keep track of. Likewise, the code which dictated their interactions was largely imperative and easily prone to breaking.

Unveiled in 2014, Flux an entirely new approach to state management. It's __goal was to make changes in state predictable__ (and thus more easily manageable, especially in complex applications) by imposing certain _restrictions_ on how and when could happen.

## How Flux Works

> Flux is a generalized pattern, not a specific library.

__Unidirectional data flow__ is one of the integral concepts of Flux: __All data must flow in only one direction__, and is a significant part of what keeps everything so predictable.

Consider MVC, the views and models have arrows running in both directions, in other words, __data flow in MVC is bidirectional__. Bidirectional data flow becomes harder to maintain as complexity grows, because it gets increasingly difficult to pinpoint exactly where a particular change originates. Since the models and views are so complexly interconnected, effects can cascade in unanticipated ways, increasing the likelihood of unwanted bugs.

> The unidirectional data flow enforced by Flux helps avoiding cascading effects.

![flux](./flux.png)

* __Actions__: Representations of the ways users can interact with the application.

* __Dispatcher__: Receives an action and forwards it to each of the application's store.
  * Flux only has _one_ dispatcher.
  * _Every_ action is sent to _every_ store.

* __Stores__: Structures which hold the application's state, as well as the logic around how to update that state.

* __Views__: What the user sees and interacts with. They are the interface for displaying the data from the stores, as well as for sending actions back to the stores through the dispatcher.
