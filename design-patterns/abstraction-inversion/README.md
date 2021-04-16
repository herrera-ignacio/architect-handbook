# Abstraction Inversion

Abstraction inversion is an _anti-pattern_ arising when users of a construct need functions implemented within it but not exposed by its interface. The result is that the users re-implement the required functions in terms of the interface, which in its turn uses the internal implementation of the same functions. This may result in implementing lower-level features in terms of higher-level ones, thus the term '_abstraction inversion_'.

## Possible ill-effects

* The user of such a re-implemented function may seriously understimate its running-costs.
* The user of the construct is forced to obscure their implementation with complex mechanical details.
* Many users attempt to solve the same problem, increasing the risk of error.

## Examples

Alleged examples from professional programming circles include:

* In _Ada_, choice of _rendezvous_ construct as a synchronisation primitive forced programmers to implement simpler constructs such as _semaphores_ on the more complex basis.
* Creating an object to represent a function is cumbersome in object-oriented languages such as Java and C++ (especially prior to C++11 and Java 8), in which functions are not first-class objects.
* Using stored procedures to manipulate data in relational database, without granting programmers right to deploy such procedures, leads to reimplementing queries outside the database. For example, large datasets are fetched and actual filtering takes place in application code. Alternatively, thousands of rows are updated (inserted or even fetched) one by one instead of running a multiple row query.

