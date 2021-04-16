# Referential Transparency

An expression is called _Referentially Transparent_ if __it can be replaced with its corresponding value without changing the program's behavior__. Otherwise, it's called _Referentially Opaque_.

This requires that the expression is __pure__, that is to say the __expression value must be the same for the same inputs and its evaluation must have no side effects__.

## Importance

The importance of referential transparency is that it allows the programmer and the compiler to reason about program behavior as a rewrite system.

This can help in proving correctness, simplifying an algorithm, assisting in modifying code without breaking it, or optimizing coed by means of memoization, common subexpression elimination, lazy evaluation, or parallelization.
