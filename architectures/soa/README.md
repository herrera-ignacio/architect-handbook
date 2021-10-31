# Service Oriented Architecture

- [Service Oriented Architecture](#service-oriented-architecture)
  - [Overview](#overview)
  - [SOA vs Three-tiered architecture](#soa-vs-three-tiered-architecture)
  - [Service definition](#service-definition)
  - [SOA Manifesto](#soa-manifesto)

## Overview

SOA is an architectural style where different *services* can be used in conjunction as a *service mesh* to provide the functionality of a large software applicatioon. It integrates distributed, separately maintained and deployed software components. These services and their corresponding consumers communicate by passing data in a well-defined, shared format, through a *communication protocol* over a network.

> Service orientation is a way of thinking in terms of services and service-based development, and the outcomes of services.

Our bisness domain becomes the primary force driving our system architecture, hopefully making it easier to make changes, and for us to **organize our teams around our business domain**.

## SOA vs Three-tiered architecture

The three-tiered architecture is so common partly because everyone has heard about it and it is based on how we usually organize our teams. In the past, the primary way IT organizations grouped people was in terms of their core competency. But this has changed. We now group people in poly-skilled teams, to reduce hand-offs and silos.

Changes in functionality are imprimarly about changes in business functionality. But if our business functionality is in effect spread across all three tiers, it increases the chance that a change in functionality will cross layers. This is an architecture in which we have *high* cohesion of related technology, but *low* cohesion of business functionality.

If we want to make it easier to make changes, instead we need to change how we group code. **We choose cohesion of business functionality**, rather than technology.

> Each service may or may not end up containing a mix of these three-layers, but that is a local service implementation concern.

## Service definition

A *service* is a discrete unit of functionality that can be accessed remotely, acted upon and updated independently. It provides a simple interface to the requester that abstract away the underlying complexity.

A service has four properties:

1. It logically represents a repeatble business activity with a specified outcome.
2. It is self-contained.
3. It is a *black box* for its consumers, meaning the consumer does not have to be aware of the service's implementation details.
4. It may be composed of other services.

## SOA Manifesto

> You can check the manifesto in http://www.soa-manifesto.org/.

This came up in October 2009 with six core values:

1. **Business value** is given more importance than technical strategy.
2. **Strategic goals** are given more importance than project-specific benefits.
3. **Intrinsic interoperability** is given more importance than custom integration.
4. **Shared services** are given more importance than specific-purpose implementations.
5. **Flexibility** is given more importance than optimization.
6. **Evolutionary refinement** is given more importance than pursuit of initial perfection.
