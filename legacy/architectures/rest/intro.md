# REST: Representational State Transfer

__Representational state transfer (REST)__ is a _de-facto standard_ for software architectures for interactive applications (accepts and responds to input) typically used in web services.

In order to be used in a REST-based application, or to be considered _RESTful_, a web service needs to meet certain constraints.

RESTful web services provide an application access to its web resources in a textual representation and support reading/modification of them with a stateless protocol through a predefined set of operations. Thus, provide interoperability.

> "Web resources" were first defined on the World Wide Web as documents or files identified by their URLs. However, today they have a much more generic and abstract definition that encompasses every thing, entity, or action that can be identified, named, addressed, handled, or performed, in any way whatsoever, on the Web.

In a RESTful Web service, requests made to a resource's URI will elicit a response with a payload formatted in HTML, XML, JSON or some other format. The response can confirm that some alteration has been made to the resource state, and provide hypertext links to other related resources.

By using a stateless protocol and standard operations, RESTful systems aim for fast performance, reliabiltiy and the ability to grow by reusing components that can be managed and updated without affecting the system as a whole.

> RESTful Web Services allow requesting systems to access and manipulate textual representations of Web Resources by using a uniform and predefined set of stateless operations.

## Key principles

* Everything is a resource.
* Each resource is identifiable by a __unique identifier__ (URI).
* Resources are manipulated via standard methods.
* Resources can have multiple representations.
* Communicate with resources in a stateless manner.

This means __resource manipulation operations through HTTP requests should always be considered atomic__. All modifications of a resource should be carried out within an HTTP request in an isolated manner. After request execution, resource is left in a final state, this implictly means that partial resource updates are not supported.

## REST vs SOAP

Unlike SOAP-based Web services, there is no 'official' standard for RESTful Web APIs. This is because REST is an architectural style, while SOAP is a protocol.

REST is not a standard in itself. Many developers also describe their APIs as being RESTful, even though these APIs actually don't fulfill all the architectural constraints described above (especially the Uniform Interface constraint).
