# Leaky Abstraction

Abstraction that leaks details that is supposed to abstract away.

## Law of Leaky Abstractions

As coined by Joel Spolsky:

> All non-trivial abstractions, to some degree, are leaky.

This statement highlights a particularly problematic cause of software defects: _the reliance of the software developer on an abstraction's infallibility_.

As systems become more complex, software developers must rely upon more abstractions. Each abstraction tries to hide complexity. However, this law claims that developers of _reliable_ software must learn the abstraction's underlying details anyway.

## Examples from Spolsky's [article](https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/)

The following are examples of leaky abstractions that create problems for software development.

### TCP/IP

TCP tries to provide reliable delivery of information, running on top of IP, which provides only "_best-effort_" service. When IP loses a packet TCP has to retransmit it, which takes additional time.

Thus TCP provides the abstraction of a reliable connection, but the implementation details leak through in the form of potentially variable performance (throughput and latency both suffer when data has to be retransmitted).

### Iteration over a large 2D array

Iteration over a large two-dimensional array can have radically different performance if done horizontally rather than vertically, depending on the order in which elements are stored in memory. One direction may vastly increase _cache misses_ and _page faults_, both of which really delay access to memory.

### SQL

SQL abstracts away the procedural steps for querying a database, allowing one to merely define what one wants. But certain SQL queries are thousands of time slower than other logically equivalent queries. On an even higher level of abstraction, ORM systems, which isolate object-oriented code from the implementation of object persistence using a relational database, still force the programmer to think in terms of databases, tables, and native SQL queries as soon as performance of ORM-generated queries becomes a concern.

### ASP.NET web forms

ASP.net web forms programming platform, not to be confused with ASP.NET MVC, abstracts away the difference between HTML code to handle clicking on a hyperlink (`<a>`) and code to handle clicking on a button. However, ASP.NET needs to hide the fact that in HTML there is no way to submit a form from a hyperlink. It does this by generating a few lines of JavaScript and attaching an `onclick` handler to the hyperlink. However, if the end user has JavaScript disabled, the ASP.NET application malfunctions. Furthermore, one cannot naively think of event handlers in ASP.NET in the same way as in a desktop GUI framework such as Windows Forms; due to the asynchronous nature of the Web, processing event handlers in ASP.NET requires exchanging data with the server and reloading the form.
