# REST: Representational State Transfer

Back in 1999, Roy Fielding defined a set of principles built around the HTTP and URI standards that gave birth to REST.

REST is a software arhitectural style that defines a set of constraints to be used for creating Web Services (APIs).

> RESTful Web Services allow requesting systems to access and manipulate textual representations of Web Resources by using a uniform and predefined set of stateless operations.

## Key principles

* Everything is a resource.
* Each resource is identifiable by a __unique identifier__ (URI).
* Resources are manipulated via standard HTTP methods.
* Resources can have multiple representations.
* Communicate with resources in a stateless manner.

This means __resource manipulation operations through HTTP requests should always be considered atomic__. All modifications of a resource should be carried out within an HTTP request in an isolated manner. After request execution, resource is left in a final state, this implictly means that partial resource updates are not supported.

## Goals

* Separation of concerns
	* Resource and multiple representations
* Visibilitity & Simplicity
	* Uniform interfaces
* Reliability
	* Resistence to failure at the system level in the presence of failures within components, connectors or data
* Scalability
	* Stateless & Layering are crucial here, separation of concerns simplifies component implementation and complexity of connector semantics.
* Performance

## Architectural Constraints

Six guiding constraints define a RESTful system. These constraints restrict the way the server can process and respond to client requests so that, by operating within these contraints, the system gains desirable _non-functional properties_ (goals).

### 1. Client-Server Architecture

Principle behind this is the __separation of concerns__. Separating the user interface concerns from the data storage concerns, improves portability of the user interfaces across multiple plataforms. It also improves scalability by simplifying server components, also, allowing components to evolve independently.

### 2. Statelessness

Client-server communication is constrained by __no client context being stored on the server between requests__. Each request from any client contains all the information necessary to service the request, and the session state is held in the client.

Session state can be transferred by the server to another service such as a database to persist state for a period and allow authentication.

### 3. Cacheability

Responses must, implictly or explicitly, define themselves as either cacheable or non-cacheable to prevent clients from providing stale or inappropriate data in response to further requests.

Well-managed caching partially or completely eliminates some client-server interations, further improving scalability and performance.

### 4. Layered System

A client cannot ordinarily tell whether it is connected directly to the end server, or to an intermediary along the way.

If a proxy or load balancer is placed between the client and server, it won't affect their communications and there won't be a need to update the client or server code.

Intermediary servers can improve systems scalability by enabling load balancing and by providing shared caches. Also, security can be added as a layer on top of the web services, and then clearly separate business logic from security logic.

Finally, it also means that a server can call multiple other servers to generate a response to the client.

### 5. Code on demand / Client-side scripting (optional)

Servers can temporarily extend or customize the functionality of a client by transferring executable code, for example, compiled components such as Java applets, or client-side scripts such as JavaScript.

### 6. Uniform Interface

The uniform interface constraint is __fundamental__ to the design of any RESTful system. It simplifies and decouples the architecture, which enables parts to evolve independently. 

There are four constraints for this uniform interface:

#### A. Resource identification in requests

Individual resources are identified in requests. Resources themsleves are conceptually separate from fthe representations that are returned to the client. For example, server could send data from its databas as HTML, XML, or as JSON, none of which are the server's internal representation.

#### B. Resource manipulation through representations

When a client holds a representation of a resource, including any metadata attached, it has enough information to modify or delete the resource's state.

#### C. Self-descriptive messages

Each message includes enough information to describe how to process the message.

#### D. Hypermedia as the Engine of Application State (HATEOAS)

Having accessed an initial URI for the REST application, a REST client should then be able to use server-provided links dynamically to disver all the available resources it needs.

As access proceeds, server responds with text that includes hyperlinks to other resources that are currently available. There is no need for the client to be hard-coded with information gathered about the structure or dynamics of the application.

This is analogous to a human web user accessing the home page of a website.


## Native HTTP Actions

* GET (Safe & Idempotent)
* POST 
* PUT (Idempotent)
* DELETE (Idempotent)
* HEAD
* OPTIONS
* TRACE
* CONNECT

Safe means that, when requested, it does not modify or cause any side effects on the state of the resource.

Idempotent means that, response stays the same, regardless of the number of times it is requested.

## REST vs SOAP

Unlike SOAP-based Web services, there is no 'official' standard for RESTful Web APIs. This is because REST is an architectural style, while SOAP is a protocol.

REST is not a standard in itself. Many developers also describe their APIs as being RESTful, even though these APIs actually don't fulfill all the architectural constraints described above (especially the Uniform Interface constraint).
