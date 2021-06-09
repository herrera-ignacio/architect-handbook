# Microservices Criticism

* **Cognitive load**.

* Inter-service calls over a network have a higher cost in terms of network latency and message processing time than in-process calls within a monolithic service process.

* Testing and deployment are more complicated.

* Moving responsibilities between services is more difficult. It may involve communication between different teams, rewriting the functionality in another language or fitting it into a different infrastructure.

* Viewing the size of services as the the primary structuring mechanism can lead to too many services when the alternative of internal modularization may lead to a simpler design.

* Two-phased commits are regarded as an anti-pattern in microservices-based architectures as this results in a tighter coupling of all the participants within the transaction. However, lack of this technology causes awkward orchestation that has to be implemneted by all the transaction participants in order to maintain data consistency.

* Development and support of many services is more challenging if they are built with different tools and technologies.

* The protocol typically used with microservices (HTTP) was design for public-facing services, and as such is unsuitable for working internal microserices that often must be impeccably reliable.

* The very concept of mciroservice is misleading, since they are only services. There is no sound definition of when a service starts or stops being a microservice.

## Cognitive Load

The architecture introduces additional complexity and new problems to deal with, such as *network latency*, *message format* design, *Backup/Availability/Consistency (BAC)*, *load balanncing* and, *fault tolerance*. All of these problems have to be addressed at scale.

The complexity of a monolithic application does not disappear if it gets re-implemented as a set of microservice applications. Some of the complexity gets translated into operational complexity. Other places where the complexity manifests itself is in the increasede network traffic and resulting slower performance.

Also, an application made up of any number of microservices has a larger number of interface points to access its respective ecosystem, which increases the architectural compelxility.