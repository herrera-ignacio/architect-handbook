# Side Effect

An operation, function or expression is said to have a _Side Effect_ if it __modifies some state variable value(s) outside its local environment/scope__, that is to say __it has an observable effect besides returning a value__ (the main effect) to the invoker of the operation.

Example side effects include modifying a non-local variable, modifying a static local variable, modifying a mutable argument passed by reference, performing I/O or calling other side-effect functions.

In the presence of side effects, a program's behaviour my depend on the order of evaluation. Understanding and debugging a function with side effects requires knowledge about the context and its possible histories

## Programming paradigms

The degree of which side effects are used depends on the programming paradigm.

* _Imperative programming_ is commonly used to produce side effects, to update a system's state.

* _Declarative programming_ is commonly used to report on the state of system, without side effects.

* _Functional programming_ rarely uses side effects. This makes it easier to do formal verifications of a program. Some functional languages do not restrict side effect, but it is customary for programmers to avoid them.

* _Assembly_ language programmers must be aware of _hidden_ side effects (instructions that modify parts of the processor state which are not mentioned in the instruction's mnemonic). A classic example is an arithmetic instruction that implicitly modifies _condition codes_ while it explicitly modifies a register.

## Temporal side effects

Side effects caused by the time taken for an operation to execuite are usually ignored when discussing side effects and _referential transparency_. There are some cases, such as hardware timing or testing, where operations are inserted specifically for their temporal side effects e.g. `sleep(5000)`. These instructions do not change state other than taking an amount of time to complete.
