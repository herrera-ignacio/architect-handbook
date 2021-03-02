# Referential Transparency

An expression is called _Referentially Transparent_ if __it can be replaced with its corresponding value without changing the program's behavior__. Otherwise, it's called _Referentially Opaque_.

This requires that the expression is __pure__, that is to say the __expression value must be the same for the same inputs and its evaluation must have no side effects__.

## Side Effects

A function is said to have a _Side Effect_ if it __modifies some state variable value(s) outside its local environment/scope__, that is to say it has an observable effect besides returning a value (the main effect) to the invoker of the operation.

Example side effects include modifying a non-local variable, modifying a static local variable, modifying a mutable argument passed by reference, performing I/O or calling other side-effect functions.

In the presence of side effects, a program's behaviour my depend on the order of evaluation. Understanding and debugging a function with side effects requires knowledge about the context and its possible histories.

## Importance

The importance of referential transparency is that it allows the programmer and the compiler to reason about program behavior as a rewrite system.

This can help in proving correctness, simplifying an algorithm, assisting in modifying code without breaking it, or optimizing coed by means of memoization, common subexpression elimination, lazy evaluation, or parallelization.
