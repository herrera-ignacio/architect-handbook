# Clean Architectures Precursors

The precursor of layered architectures is the __classic MVC pattern from Smalltalk. This disentangles the model from the user interface (controller and view), so that the model does not depend on the UI__.

More complex systems do not have just one user interface, but possibly multiple user interfaces (such as a web app or a mobile app). MVC isolates the business logic on the server from these UIs, so the server doesn't care about which kind of app accesses it.

Typically, the server still depends on backend services such as databases or third party providers. This is perfectly fine, and leads to a simple layered architecture.

The __Hexagonal Architecture goes further and stops making a distinction between frontend and backend__. Any external system might be an input (data source) or an output. Our core system defines the necessary interface (ports), and we create adapters for any external systems.

One classic approach for strong decoupling is a __Service Oriented Architecture (SOA)__, where all serices publich events to and consume events from a shared bus. A similar approach was later popularized by microservices.

> Clean Architecture could be considered an evolution of related approaches like the __Onion Architecture__ by Jeffrey Palermo (2008) and the __Hexagonal Architecture__ ("_Ports and Adapters_") by Alistar Cockburn and others (< 2008).
>
> Different problems have different requirements. Clean Architecture and related approaches favor decoupling, flexibility, and dependency inversion, but sacrifice simplicity. This is not always a good deal.
