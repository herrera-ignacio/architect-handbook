# Caching

*Caching* is a technique that **stores a copy of a given resource and serves it back when requested**. 

> When a web cache has a requested resource in its store, it intercepts the request and returns its copy instead of redownloading from the originating server.

This achieves several goals: iot eases the load of the server that doesn't need to serve all clients itself, and improves performance by being closer to the client.

On the other side, it has to be configured properly as not all resources stay identical forever: it is important to cache a resource only until it changes, not longer.
