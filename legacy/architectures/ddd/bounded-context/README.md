# Bounded Context

A *bounded context* typically represents a larger organizational boundary inside an organization. Within the scope of that boundary, explicit responsibilities need to be carried out.

Bounded contexts hide implementation detail. There are internal concerns that should be hidden from the outside world.

From an implementation point of view, bounded contexts *contain one or more aggregates*. Some aggregates may be exposed outside the bounded context; others may be hidden internally.

Bounded contexts may have relationships with other bounded contexts; when mapped to services, these dependencies become inter-service dependencies.
