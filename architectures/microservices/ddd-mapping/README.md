# Mapping Aggregates and Bounded Contexts to Microservices

Both the *aggregate* and the *bounded context* give us units of cohesion with well-defined interfaces iwth the wider system. The aggregate is a self-contained state machine that focuses on a single domain concept in our system, with the bounded context representing a collection of associated aggregates, again with an explicit interface to the wider world.

You should probably target services that encompass entire bounded contexts. As you find your feet, and decide to break these services into smaller services, look to split them around aggregate boundaries.

A trick here is that even if you decide to split a service that models an entire bounjded context into smaller services later on, you can still hide this decision from the outside world (e.g., by presenting a coarser-grained API to consumers).

> The decision to decompose a service into smaller parts is arguably an implementation decision, so we might as well hide it if we can.
