# Software Architect Handbook

This attempts to be a collection of the minimal least required concepts, terminology, and skills that an architect should have.

I won't be covering most of the topics in detail, some of them will be references to external sources, there's plenty of information out there if you want to do research on your own, books, blogs, videos, open source projects, etc, I rather prefer just presenting to you the fundamentals and plant the seed of curiosity in you to go and do a deeper research as needed.

The idea of this collection is not to help you become a expert of, let's say a particular architectural style, but rather get an overall knowledge of different types of architectures, pros and cons, and technical concepts that have system impact and should be considered in the broader perspective an architect should have.

## TOC

* Design Principles
* Programming Paradigms
* Design Patterns
* Architecture Patterns & Principles
* Architectural Styles
* Language & Frameworks Specifics

## Design Principles

* SOLID
* DRY
* KISS

## Programming Paradigms

* [Imperative and Procedural](./paradigms/imperative)
* [Object Oriented Programming](./paradigms/oop)
	* [Dynamic Dispatch / Message Passing](./paradigms/oop/dynamic-dispatch.md)
	* [4 Pillars of OOP](./paradigms/oop/4pillars.md)
		* Abstraction
		* Inheritance
		* Encapsulation
		* Polymorphism
	* [Composition, Aggregation and Delegation](./paradigms/oop/cad.md)
	* [Subtyping - Interface Inheritance](./paradigms/oop/subtyping.md)
	* [Composition vs Inheritance](./paradigms/oop/inheritance-composition.md)
	* [Parameterized Types vs Inheritance](./paradigms/oop/inheritance-parameterized.md)
* Declarative
* Functional

## Design Patterns

* Object Oriented, Classical
* Functional

## Architecture Patterns & Principles

* [Best Architectural Decision](./principles/architectural.md)
* Active Record
* Data Mapper

## Architectural Styles

### Clean Architecture

* WIP

## Languages & Frameworks

Specifics that should be considered while developing a software solution relying on a particular language/framework.

### Javascript & Node.js

* [Considerations for a better architecture](./js/considerations.md)
* [AfterAcademy, backend architecture considerations](https://afteracademy.com/blog/design-node-js-backend-architecture-like-a-pro)
* [The Working Architecture - Viktor Turskyi](js/working-architecture)
