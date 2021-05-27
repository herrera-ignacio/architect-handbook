# Screaming Architecture

* Theme
* Purpose

> What does the architecture of your application scream? When you look at the top-level directory structure, and the source file in the highest-level package, do they scream "Health Care System", or "Accounting System", or "Inventory ManagementSystem"? Or do they scream "Rails" or "Sring/Hibernate" or "ASP"?

## Theme

Just as the plans for a house or a library scream about the use cases of those buildings, so should the architecture of a software application scream about the use cases of the applications.

*Architectures are not (or should not be) about frameworks*. Architectures should not be supplied by frameworks, frameworks are tools to be used, not architectures to be conformed to.

## Purpose

> Good architecture emphasizes the use cases and decouples them from peripheral concerns.

Good architectures can safely describe the structures that supports use cases without commiting to frameworks, tools, and environments.

A good software architecture allows decisions about frameworks, databases, web servers, and other environmental issues and tools to be deferred and delayed. *Frameworks are options to be left on*. A good architecture makes it easy to change your mind about those decisions, too.

> Look at each framework with a jaded eye. Yes, it might help, but at what cost? Ask yourself how you should use it, and how you should protect yourself from it. Think about how you can preserve the use case emphasis of your architecture. Develop a strategy that prevents the framework from taking over that architecture.
