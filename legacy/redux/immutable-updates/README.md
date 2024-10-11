# Immutable Update Patterns

* Updating Nested Objects
* Inserting and Removing Items in Arrays
* Updating an Item in an Array
* Immutable Update Utility Libraries

## Updating Nested Objects

Every level of nesting must be copied and updated appropriately.

Unfortunately, the process of correctly applying immutable updates to deeply nested state can easily become verbose and hard to read. Each layer of nesting makes reading harder, and gives more chances to make mistakes. This is one of several reasons why you are encouraged to keep your state flattened, and compose reducers as much as possible.

Common mistakes:

1. New variables that point to the same objects.

2. Only making a shallow copy of one level.

## Inserting and Removing Items in Arrays

Normally, Javascript array's contents are modified using mutative functions like `push`, `unshift`, and `splice`. Since we don't want to mutate state directly in reducers, those should normally be avoided and instead use "insert" or "remove" behavior implemented with `array.slice`.

The key is to modify the original in-memory reference. As long as we make a copy first, we can safely mutate the copy. Note that this is true for both arrays and objects, but nested values still must be updated using the same rules.

## Updating an Item in an Array

Updating one item in an array can be accomplished by using `Array.map`, returning a new value for the item we want to update, and returning the existing values for all other items.

## Immutable Update Utility Libraries

_Immer_ makes immutable updates a simple function and plain Javascript objects.

> A list of many immutable update utilities can be found in the [Immutable Data#Immutable Update Utilities](https://github.com/markerikson/redux-ecosystem-links/blob/master/immutable-data.md#immutable-update-utilities).

### Redux Toolkit

Redux Toolkit package includes a `createReducer` utility that uses _Immer_ internally (wraps reducer in Immer's `produce` function). Because of this, you can write reducers that appear to "mutate" state, but the updates are actually applied immutably.

It's not obvious just by looking at the code that the function is actually safe and updates the state immutable.

In addition, Redux Toolkit's `createSlice` utility will auto-generate action creators and action types based on the reducer functions you provide, with the same Immer-powered update capabilities inside.
