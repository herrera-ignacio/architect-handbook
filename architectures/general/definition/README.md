# Software Architecture

## Robert C. Martin

The obvious appeal of architecture is __structure__ (components, classes, functions, modules, layers, and services, micro or macro).

> _Architecture represents the significant design decisions that shape a system, where significant is measured by cost of change._ - Grady Booch

This measure tells us how we can determine whether an architecture is good or not: Not only does a good architecture meet the needs of its users, developers, and owners at a given point in time, but it also meets them over time.

> _If you think good architecture is expensive, try bad architecture._ - Brian Foote and Joseph Yoder

This throws some light on the problem software architecture tries to solve. How to know what typical changes will be so that we can shape the system through _significant design decisions_ around them? How do we reduce future development effort and cost? 

> _Architecture is a hypothesis, that needs to be proven by implementation and measurement._ - Tom Gilb

Good software architecture __recognizes the softness__ of software and __aims to preserve it__ as a first-class property of the system. It recognizes that we operate with incomplete knowledge, but it also understands that, as humans, operating with incomplete knowledge is something we can do through experimentation and discovery. A good architecture comes form understanding it more as a journey than as a destination, more as an __ongoing process of enquiry than as a frozen artifact__.

> _The only way to go fast, is to go well._ - Robert C. Martin

When software is done right, it requires a fraction of the human resources to create and maintain. Changes are simple and rapid. Defects are few and far between. Effort is minimizsed, and functionality and flexibility are maximized.

> The goal of software architecture is to minimize the human resources required to build and maintain the required system.

The measure of design quality is simply the measure of the effort required to meeth the needs of the customer. If that effort is low, and stays low throughout the lifetime of the system, the design is good. If that effort grows with each new release, the design is bad.

> To build a system with a design and an architecture that minimize effort and maximize productivity, you need to know which attributes of system architecture lead to that end.

## Ralph Johnson

Architecture is a subjective thing, a **shared understanding of a system's design** by the expert developers on a project. Commonly this shared understanding is in the form of the major components of the system and how they interact.

It's also about decisions, in that it's the decisions that developers wish they could get right early on because they're perceived as hard to change.

> In the end, architecture boils down to the important stuff, whatever that is.

