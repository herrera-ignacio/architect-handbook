# Plugin Architecture: Model Controller Presenter

MCP, Also known as a __Plugin Architecture__.

* Overview
* Flow
* Plugins Analogy

## Overview

> It introduces the concept of _Architectural Boundary_ (do not confuse with Boundary object), that separates the business rules from whatever technology dependency we use.

You first partitionn the system into components. Some of those compopnents aree corer business rules, others are plugins that contain necessary functions that are not directly related to the core business. Then you arrange the code in those components such that the arrows between them point in one direction, toward the core business.

Dependency arrows are arranged to point from lower-level details to higher-level abstractions.

> You should recognize this as an application of the *Dependency Inversion Principle* and the *Stable Abstractions Principle*.

## Flow

![mcp](./mcp.gif)

The `Interactor` is going to take `Response Model Data Structure`, and pass it through the `Boundary` object (and through the Architectural Boundary) to a `Presenter`.

Controller passes data trough a Boundary object, and a Request Model (Input Data) Data Structure, to an Interactor.

Interactor it's going to take Response Model Data Structure, and pass it through the Boundary (and through the Architectural Boundary) to a Presenter.

## Plugins Analogy

Plugins are defenselss and vulnerable against the thing they plug into, because if it changes its interface, plugin will need to change too.

We can think of our own modules as plugins.

There are things in our system that we want to be __immune__ from other things in the system. For example, we'd want Business Rules to be immune to changes in the UI. That means, we'd like the UI to act as a plugin for the Business Rules.

__If something changes a lot, it should be a Plugin__.
