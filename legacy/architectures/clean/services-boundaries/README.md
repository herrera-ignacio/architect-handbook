# Service and Boundaries

Architectural boundaries do not fall *between* services. Rather, those boundaries run *through* the services, dividing them into components.

To deal with the cross-cutting concerns that all significant systems face, *services must be designed with internal component architectures that follow the Dependency Rule*. Those services do not define the architectural boundaries of the system; instead, the components within the services do.

> As useful as services are to the scalability and develop-ability of a system, they are not, in and of themselves, architecturally significant elements.

The architecture of a system is defined by the boundaries drawn within that system, and by the dependencies that cross those boundaries. That *architecture is not defined by the physical mechanisms by which elements communicate and execute*.

A service might be a single component, completely surrounded by an architectural boundary. Alternatively, a service might be composed of several components separated by architectural boundaries. In some cases, clients and services may be so coupled as to have no architectural significance whatsoever.
