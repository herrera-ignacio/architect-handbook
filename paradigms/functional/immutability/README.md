# Immutability

* Immutable Object
* Benefits over mutable objects
* Weak vs Strong Immutability
* Immutability and Architecture

## Immutable Object

In object-oriented and functional programming, an __immutable object__ s an object whose state cannot be modified after it is created. In some cases, an object is considered immutable even if some internally used attribute change, but the object's state appears unchanging from an external point of view.

> For example, an object that uses memoization to cache the results of expensive computations could still be considered an immutable object.

> Strings and other concrete objects are typically expressed as immutable objects to improve readability and runtime efficiency in object-oriented programming.

## Benefits over mutable objects

* _Thread safety_: Multiple threads can act on data represented by immutable objects without concern of data being changed by other threads.

* Simpler to understand and reason about.

* Higher security.

## Weak vs Strong Immutability

__Weakly immutable__ means that there is no way to change object's state's parts, even though other parts of the object may be changeable. Means that certain _fields_ of an object are immutable.

If the whole object cannot be extended by another class, if all fields are immutable, then the object is called __strongly immutable__.

## Immutability and Architecture

> All race conditions, deadlock conditions, and concurrent update problems are due to mutable variables.

In other words, all the problems that we face in concurrent applications (multithreading and multiprocessing) cannot happen if there are no mutable variables.

Immutability can be practicable, in the lack of infinite resources (storage and processor speed), if certain compromises are made: _Segregation of Mutability_ & _Event Sourcing_.

### Segregation of Mutability

> Segregate the application, or the services within the application, into mutable and immutable components.

The immutable components perform their tasks in a purely functional way, without using any mutable variables. They communicate with one or more other components that are not purely functional, and allow for the state of variables to be mutated.

Since mutating state exposes those components to all the problems of concurrency, it is common practice to use some kind of _transactional memory_ to protect the mutable variables from concurrent updates and race conditions. Transactional memory simply treats variables in memory the same way a database treats records on disk. It protects those variables with a transaction- or retry-based scheme.

This kind of segregation is supported by the use of appropriate disciplines to protect those mutated variables.

> Architects would be wise to push as much processing as possible into the immutable components, and to drive as much code as possible out of the components that must allow mutation.

### Event Sourcing

> Event Sourcing is a strategy wherein we store the transactions, but not the state. When state is required, we simply apply all the transactions from the beginning of time.

As a simple examle, imagine a banking application that maintains the account balances of its customers. It mutates those balances when deposit and withdrawal transactions are executed. If we wanted a scheme that requires no mutable variables, we could instead store only the transactions. Whenever anyone wants to know the balance of an account, we simply add up all the transactions for that account (perhaps we have enough storage and processing power tyo make the scheme work for the reasonable lifetime of the application).

Of course, we can take shortcuts. For example, we can compute and save the state every midnight. Then, when the state information is required, we need compute only the transactions since midnight.

Now consider the data storage required for this scheme. Nothing ever gets deleted or updated from such a data store. Because neither updates nor deletions occur in the data store, there cannot be any concurrent update issues.

> If we have enough storage and processor power, we can make our applications _entirely immutable_ and, therefore, _entirely functional_.

Another good example is _source code control systems_.
