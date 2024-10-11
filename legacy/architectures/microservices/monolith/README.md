# The Monolith

> We consider a *monolith* when all functionality in a system *needs* to be deployed together.

- [The Monolith](#the-monolith)
  - [Types](#types)
    - [Single Process Monolith](#single-process-monolith)
    - [Modular Monolith](#modular-monolith)
    - [Distributed Monolith](#distributed-monolith)
    - [Third-Party Black-Box Systems](#third-party-black-box-systems)
  - [Challenges](#challenges)
  - [Advantages](#advantages)

## Types

### Single Process Monolith

The most common example of monolith is a system in which all of the code is deployed as a *single process*.

You may have multiple instances of this process for robustness or scaling reasons. In reality, these single-process systems can be simple distributed systems in their own right, as they nearly always end up reading data from or storing data into a database.

### Modular Monolith

The modular monolith is a subset of the single process monolith: the single process consists of *separate modules*, each of which can be worked on independently, but which still need to be combined for deployment.

> For many organizations, the modular monolith can be an excellent choice.

If the module boundaries are well defined, it can allow for a high degree of parallel working, but sidesteps the challenges of the more distributed microservice architecture along with much simpler deployment concerns.

> Shopify is a great example of an organization that used this technique as an alternative to microservice decomposition. See [Kirsten Westeinde's talk](https://www.youtube.com/watch?v=ISYKx8sa53g).

One of the challenges of a modular monolith is that the database tends to lack the decomposition we find in the code leve, leading to significant challenges that can be faced if you want to pull the monolith in the future.

### Distributed Monolith

A distributed monolith is a system that consists of multiple services, but for whatever reason the entire system *needs* to be deployed together.

> A distributed monolity may well meet the definition of SOA, but all too often fails to deliver its promises.

It can have *all* the disadvantages of a distributed system, *and* the disadvantages of a single-process monolith, without having enough upsides of either.

Without enough focus on concepts like information hiding and cohesion of business functionality, it leads to highly coupled architectures in which changes *ripple* across service boundaries, and seemingly innocent changes that appear to be local in scope break other parts of the system.

### Third-Party Black-Box Systems

We can consider some *third-party software* as monoliths that we may want to "decompose" as part of a migration effort (e.g., payroll systems, CRM systems, and HR systems).

## Challenges

The monolith, in all of its variants, is often more *vulnerable* to the perils of coupling; specifically, implementation and deployment coupling.

It has to deal with the problem of **delivery contention**: As you have more and more people working in the same place, they get in each other's way. Confusion around who owns what, and who makes decisions. *Confused lines of ownership* come with a lot of challenges.

> ["Don't Touch My Code! Examining the Effects of Ownership on Software Quality"](https://www.microsoft.com/en-us/research/publication/dont-touch-my-code-examining-the-effects-of-ownership-on-software-quality/)

Having a monolith doesn't mean you will definitely face the challenges of a delivery contention, any more than having a microservice architecture means that you won't ever face the problem. But a microservice architecture does give you more concrete boundaries in a system around which ownership lines can be drawn, giving you much more flexibility regarding how you reduce this problem.

## Advantages

> A monolith architecture is a choice, and a valid one.

* **Simpler deployment topology** can avoid many of the pitfalls associated with distributed systems.

* It can result in much simpler:
  * Developer workflows
  * Monitoring & troubleshooting
  * End-to-end testing

* Simplify **code reuse** within the monolith itself. If we want to reuse code within a distributed system, we have to decide whether we want to copy code, break out libraries, our push the shared functionality into a service.
