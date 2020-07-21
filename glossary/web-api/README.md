# Web API

An API is a collection of clearly __defined methods of communication between different software components__.

More specifically, a Web API is the interface composed by a __collection of endpoints and the resources these endpoints expose__.

A Web API is defined by the types of requests that it can handle, which is determined by the routes that it defines, and the types of responses that the clients can expect to receive after hitting those routes.

One Web API can be used to provide data for different frontends. Since a Web API can provide data without really specifying how the data is viewed, multiple different HTML pages or mobile applications can be created to view the data from the Web API in different ways.

## What kind of responses can s erver send?

The data that the server sends back can come in different forms. For example, a server might serve up an HTML file, send data as JSON, or it might send back only an HTTP status code. You’ve probably seen the status code “404 - Not Found” whenever you’ve tried navigating to a URI that doesn’t exist, but there are many more status codes that indicate what happened when the server received the request.
