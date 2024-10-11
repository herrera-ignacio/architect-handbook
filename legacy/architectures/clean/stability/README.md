# Stability

Stability is not directly related with *frequency* of change, instead, it is related to the **amount of work required to make a change**.

Many factors make a software component hard to change, for example, its size, complexity, and clarity, among other characteristics. One sure way to make a software comonent difficult to change, is to make lots of other software components *depend* on it.

> A component wiwth lots of incoming dependencies is very stable because it requires a great deal of work to reconcile any changes with all the dependent components.

## Component example

Suppose we have a component `X`, which is a stable component. Three components depend on `X`, so it has three good reasons not to change. We say that `X` is *responsible* to those three components. Conversely, `X` depends on nothing, so it has no external influence to make it change. We say it is *independent*.

Suppose on the contrary, we have a component `Y`, which is a very unstable component. No other components depend on `Y`, so we say that it is *irresponsible*. `Y` also has three components that it depends on, so changes may come from three external sources. We say that `Y` is *dependent*.
