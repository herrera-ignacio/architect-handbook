# Service Granularity

A key step in defining a microservice architecture is figuring out how big an individual microservice has to be.

There is no consensus for this, as the right answer depends on the business and organizational context.

> For instance, Amazon famously uses a SOA where a service often maps 1:1 with a team of 3 to 10 engineers.

Generally, services that are dedicated to a single task, such as calling a particular backend system or making a particular type of calculation, are called as **atomic services**. Similarly, services that call such atomic services in order to consolidate an output, are called as **composite services**.

> It is considered a bad practice to make the service to small, as then the runtime overhead and the operational complexity can overwhelm the benefits of the approach. When things get too fine-grained, alternative approaches must be considered, such as packaging the function as a library, moving the function into other microservices.

If *Domain Driven Design* is employed, then a microservice could be as small as an *Aggregate* or as large as a *Bounded Context*.
