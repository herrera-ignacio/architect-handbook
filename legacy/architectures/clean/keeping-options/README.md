# Keeping Options Open

* General idea
* Decoupling Layers
* Decoupling Use Cases
* Decoupling Mode

## General idea

> Software has two types of values, the value of its behavior and the value of its structure. The second of these is the greater of the two because it is this value that makes software *soft*.

The way you keep software *soft* is to **leave as many options open as possible for as long as possible**. The options *are the details that don't matter*.

> The goal of the architect is to create a shape for the system that recognizes policy as the most essential element of the system while making the details irrelevant to that policy.

This allows decisions abnout those details to be *delayed* and *deferred*. The longer you wait to make those decisions, *the more information you have with which to make them properly*.

> A good architect maximizes the number of decisions not made.

It is hard to balance all architectural concerns with a component structure that mutually satisfies them all, specially during the system life cycle, in which the goals we must meet are indistinct and inconstant, but **there are some principles or architectures relatively inexpensive to implement that can help** balance those concerns, **even when you don't have a clear picture yet**.

## Decoupling Layers

The architect does not know what all necessary use cases are but *does* know the basic intent of the system. It's a shopping cart system, or it's a bill of materials system, or it's an order processing system, etc... So the architect can empy the **Single Responsibility Principle** and the **Common Closure Principle** to separate those things that change for different reasons, and to collect those things that change for the same ereasons, given the context of the intent of the system.

> There are some obvious things that change for different reasons, such as user interfaces that have nothing to do with business rules. Validation of input fields is a business rule that is closely tied to the application itself. In contrast, the calcuation of interest on an account and the counting of invetory are business rules that are more closely associated with the domain. These two different kinds of rules will change at different rates, and for different reasons.

Then we find the **ystem divided into decoupled horizontal layers**, the UI, application-specific business rules, application-independent business rules, database, etc...

## Decoupling Use Cases

Use cases are a **very natural way to divide the system**. Use cases are norrow vertical slices that cut through the horizontal layers of the system. 

> The use case for adding an order to an order entry system almost certainly will change at a different rate, and for different reasons, than the use care that deletes an order from the system.

Each use case uses some UI, some application-specific business rules, some application-independent business rules, etc... Thus, as we are dividing the system into horizontal layers, we are also dividing the system into thin vertical use cases that cut through those layers.

> To achieve this decoupling, we separate the UI of the add-order use case from the UI of the delete-order use case. We do the same with the business rules, and so on. We keep the use cases separate down the vertical height of the system.

If you decouple the elements of the system that change for different reasons, then you can continue to add new use cases without interfering with old ones.

## Decoupling Mode

The decoupling that we did for the sake of the use cases also help with operations. However, to take advantage of the operational benefit, the decoupling must have the appropriate mode. To run in separate servers, some concerns must be addressed, for example the separated components cannot depend on being together in the same address space of a processor. They must be independent services with some way of communicating between themselves.

> An architecture based on services is often called a **service-oriented architecture (SOA)**.

A good architecture leaves options open. The *decoupling mode is one of those options*.
