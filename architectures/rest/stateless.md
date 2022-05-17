# Stateless protocol

## Definition

A __stateless__ protocol is a communication protocol in which the receiver must not retain _session state_ from previous requests.

The sender transfers relevant session state to the receiver in such a way that __every request can be understood in isolation__, that is without reference to session state from previous requests retained by the receiver.

> Examples include _Internet Protocol_ (IP), _Hypertext Transfer Protocol_ (HTTP), UDP.

Another way to define this is that __the client is responsible for storing and handling the session__ related information on its own side, as well as sending any state information to the server whenever it is needed.

There should not be any __session affinity__ or __sticky session__ between the client and the server.

## Tradeoffs

### Advantages

Stateless protocols improve:

* __Visibility__: monitoring systems don't have to look beyond a single request in order to determine its full nature.
* __Reliability__: eases the task of recovering from partial failures.
* __Scalability__: allows the server to quickly free resources and further simplifies implementation.

### Disadvantages

They may __decrease network performance__ by increasing the repetitive data sent in a series of requests, since the data cannot be left on the server and reused.

## Vs Stateful

In contrast, a __stateful__ protocol is a communication protocol in which the receiver _may_ retain session state from previous requests.

> Examples include _Transmission Control Protocol_ (TCP) and the _File Transfer Protocol_ (FTP).

## Stacking protocol layers

There can be complex interactions between stateful and stateless protocols among different protocol layers.

> For example, HTTP (stateless) is layered on top of TCP (stateful), which is layered on top of IP (stateless), and so on.

### HTTP & Session Management

The stacking of layers continues even above HTTP. As a workaround for the lack of a retained session state, HTTP servers implement various _session management methods_.

Typically, utilizing a session identifier in an _HTTP cookie_ referencing session state stored on the server, effectively creating a stateful protocol on top of HTTP.

> HTTP cookies may be considered to violate REST architectural style because even without referencing a session state stored on the server, they are independent of session state (they affect previous pages of the same website in the browser history) and they have no defined semantics.

