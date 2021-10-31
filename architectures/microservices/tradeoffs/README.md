# Tradeoffs

- [Tradeoffs](#tradeoffs)
  - [Benefits](#benefits)
  - [Potential Drawbacks](#potential-drawbacks)
    - [Microservices & SOA](#microservices--soa)
    - [Distributed Services](#distributed-services)
    - [New Technologies](#new-technologies)
    - [Size](#size)
    - [Ownership](#ownership)

## Benefits

> Perhaps, above all, microservice architectures give you *flexibility*. However, it's important to note that **none of these advantages come for free**.

* __Modularity__: Application is easier to understand, develop, test, and become more resilient to architecture erosion. This benefit is often argued in comparision to the complexity of monolithic architectures.

* __Scalability__: Since microservices are implemented and deployed independently of each other, i.e. they run within independent processes, they can be monitored and scaled independently.

* __Integration of heterogeneous and legacy systems__: Microservices is considered as a viable means for modernizing existing monolithic applications, by replacing parts of the existing software using an *incremental approach*.

* __Distributed development__: It parallelizes development by enabling small autonomous teams to develop, deploy and scale their respective services independently. It facilitates *continuous integratio, delivery and deployment*.

## Potential Drawbacks

### Microservices & SOA

Microservices as a way of applying a *Service Oriented Architecture* comes with some concerns:

* Viewing the size of services as the the primary structuring mechanism can lead to too many services when the alternative of **internal modularization may lead to a simpler design**.

* There is **no sound definition** of when a service starts or stops being a microservice.

### Distributed Services

Microservices come associated with most of the general drawbacks of any distributed service:

* Network latency & failures
* Message format design
* *BAC*: Backup, Availability & Consistency
* Load balancing
* Fault tolerance

> Two-phased commits are regarded as an anti-pattern in microservices-based architectures as this results in a tighter coupling of all the participants within the transaction. However, lack of this technology causes **awkward orchestation** that has to be implemneted by all the transaction participants **in order to maintain data consistency**.

Having to deal with all those concerns at scale increase the **architectural complexity** of the whole system.

> Some of the complexity from the monolith application gets translated into operational complexity.

### New Technologies

Adopting any new technologhy will have a *cost*, it will create some *upheaval*. Hopefully, that will be worth it if you've picked the right technology, but when first adopting a microservice architecture, you have *enough* going on.

It can be much more useful to get your head around all the challenges of how to properly evolve and manage a microservice architecture as you encounter them, making use of a technology stack you are familiar with, and then consider whether changing your existing technology may help address those problems as you find them.

> "Choose the approach that works for you, and change things to address problems as and when you see them." - Sam Newman

### Size

The goal of microservices is to have *as small an interface as possible*. Ultimately, the concept if *size* is highly contextual. The idea beign that the *scope* of functionality should be *easy* to understand, and therefore easy to change.

When you are first starting out, it's much more important that you focus on two key things:

1. How many microservices can you handle? As you have more services, the complexity of your system will increase, and you'll have to learn new skill (and perhaps adopt new technology) to cope with this.
2. How do you define microservice boundaries to get the most of them, without everything becoming a horribly coupled mess?

### Ownership

In traditional IT organizations, the act of developing osftware is often handled by an entirely separate part of the business from that which actually defines requirements and has a connection with the customers.

Product owners now work directly as part delivery teams, with these teams being aligned around customer-facing product lines, rather than around arbitrary technical groupings.

> "Rather than centralized IT functions being the norm, the existence of any central IT function is to support these customer-focused delivery teams." - Sam Newman

Reducing services that are shared across multiple teams is key to minimizing delivery contention; business-domain-oriented microservice architectures make this shift in organizational structures much easier.
