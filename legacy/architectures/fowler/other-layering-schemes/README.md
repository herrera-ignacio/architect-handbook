# Other Layering Schemes

* Brown model
* Core J2EE Layers
* Microsoft DNA (Kirtland)
* Marinescu Layers
* Marinescu Layers
* Nilsson Layers

## Brown Model

This model has five layers:

* **Presentation**: Presentation
* **Controller/Mediator**: Presentation (*Application Controller*)
* **Domain**: Domain
* **Data Mapping**: Data Source (*Data Mapper*)
*** Data Source**: Data Source

Essentially it places **additional mediating layers between the basic three layers**. The *Controller/Mediator* mediates between the basic three layers, while the *Data Mapping* layer mediates between the *Domain* and *Data Source* layers.

> "I find that the mediating layers are useful some of the time but not all of the time, so I describe them in terms of patterns. The *Application Controller* is the mediator between the *presentation* and *domain*, and the *Data Mapper* is the mediator between the data source and the domain." - Martin Fowler

You can start with three base layers, see if any of them is getting too complex, and if so add the mediating layer to separate the functionality.

## Core J2EE Layers

This model has five layers:

* **Client**: Presentation that runs on client (e.g., rich-client systems)
* **Presentation**: Presentation that runs on server (e.g, HTTP handlers, server pages)
* **Business**: Domain
* **Integration**: Data Source
* **Resource**: External resource that data source communicates with

The resource layer comprises external services that the integration layer connects to. The main difference is that they split the presentation between the part that runs on the client (*Client layer*) and the part that runs on the server (*Presentation layer*). This is often a useful split, but again it's not one that's needed all the time.

## Microsoft DNA (Kirtland)

It defines three layers that correspond pretty directly to the three base layers.

* **Presentation**: Presentation
* **Business**: Domain
* **Data Access**: Data Source

The biggest shift occurs in the way that data is passed up from the data access layers. In Microsoft DNA all the layers operate on record sets that result from SQL queries issued by the data access layer. This introduces an apparent coupling in that both the *Business* and the *Presentation* layers know about the database.

The record set acts as a *Data Transfer Object* between layers. The business layer can modify the record set on its way up to the presentation or even create one itself (that is rare). Although this form of communication is in many ways unwieldy, it has the **big advantage of allowing the presentation to use data-aware GUI controls**, even on data that's been modified by the business layer.

In this case the *domain layer* is structured in the form of *Table Modules* and *data source layer* uses *Table Data Gateways*.

## Marinescu Layers

Marinescu has five layers.

* **Presentation**: Presentation
* **Application**: Presentation (*Application Controller*)
* **Services**: Domain (*Service Layer*)
* **Domain**: Domain (*Domain Model*)
* **Persistence**: Data Source

The *presentation* is split into two layers, reflecting the separatio nof an *Application Controller*.

The domain is also splited, with a *Service Layer* built on a *Domain Model*, reflecting the common idea of splitting the *domain layer* into two parts. This is a common approach, reinforced by the limitations of EJB as a *Domain Model*.

The idea of splitting a *services layer* fro ma *domain layer* is based on a **separation of workflow logic from pure domain logic**. The *services layer* typically includes logic that's particular to a **single use case and also some communication** with other infrastructures, such as messaging.

## Nilsson Layers

Nilsson uses one of the more complex layering schemes:

* **Consumer**: Presentation
* **Consumer helper**: Presentation (*Application Controller*)
* **Application**: Domain (*Service Layer*)
* **Domain**: Domain (*Domain Model*)
* **Persistence Access**: Data Source
* **Public stored procedures**: Data Source that may include some domain
* **Private stored procedures**: Data source that may include some domain

Nilsson encourages **domain logic in stored procedures for performance reasons**, but this can make an application much harder to maintain. On ocassion, however, it's a valuable optimization technique.
