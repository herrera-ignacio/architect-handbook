# REST Architectural Properties

The constraints of the REST architectural style affect the following architectural properties:

* __Performance__ in component interactions, which can be a dominant factor in user-perceived performance and network efficiency.

* __Scalability__ allowing the support of large numbers of components and interactions among them.

* __Reliability__ in the resistance to failure at the system level in the presence of failures within components, connectors, or data.

* __Simplicity__ of a uniform interface.

* __Modifiability__ of components to meet changing needs.

* __Portability__ of components by moving program code with the data.

> Roy Fielding: "REST's client-server __separation of concerns__ simplifies component implementation, reduces the complexity of connector semantics, improves the effectiveness of performance tuning, and increases the scalability of pure server components."

> Roy Fielding: "Layered system constraints allow intermediaries (proxies, gateways, and fiewalls) to be introduced at various points in the communication without changing the interfaces between components, thus allowing them to assist in communication translation or improve performance via large-scale, shared caching. REST enables intermediate processing by constraining messages to be self-descriptive: interaction is stateless between requests, standard methods and media types are used to indicate semantics and exchange information, and responses explicitly indicate cacheability."
