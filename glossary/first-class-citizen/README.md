# First-class citizen

In a programming language design, a __first-class citizen__ (also __type, object, entity__ or __value__) in a given programming language is an entity which supports all the operations generally available to other entities. These operations typically include being passed as an argument, returned from a function, modified, and assigned to a variable.

## Definition

_Robin Popplestone_ gave the following definition: All items have certain fundamental rights:

1. Can be the actual parameters of functions.

2. Can be returned as results of functions.

3. Can be the subject of assignment statements.

4. Can be tested for equality.

## First-class function

A programming language is said to have __first-class functions__ if it threats functions as _first-class citizens_. This means the language supports passing functions as arguments to other functions, returning them as the values from other functions, and assigning them to variables or storing them in data structures. Some programming language theorists require support for anonymous functions as well.

First-class functions are a necessity for the _Functional Programming_ style, in which the use of _higher-order functions_ is a standard practice. A simple example of a higher-ordered function is the `map` function, which takes, as its arguments, a function and a list, and returns the list formed by applying the function to each member of the list.

### Equality of functions

This question appears more difficunt and one has to distinguish between several types of function equality:

1. _Extensional equality_: if they agree on their outputs for all inputs.

2. _Intensional equality_: if they have the same "internal structure".

3. _Reference equality_: functions or closures are assigned a unique identifier and equality is decided based on equality of the identifier.
