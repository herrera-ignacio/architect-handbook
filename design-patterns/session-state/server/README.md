# Server Session State

> Keeps the session state on a server system in a serialized form.

* Overview
* How It Works
* When to Use It

## Overview

In the simplest form of this pattern, **a session object is held in memory on an application server**.

## How It Works

* Store session objects keyed by a session ID so it can be retrieved when processing a request.

* You store the objects in memory or serialize all the session state to a *Memento* (Gang of Four).

* Storing in a database or a shared server is needed for supporting efficient clustering and failover.

* Storing a serialized *Server Session State* in the database would require a table indexed by session ID that stores *Serialized LOB*. There are other approaches such as using *JSON Web Tokens (JWT)*.

* If you are storing *Server Session State* in a database, you'll have to worry about handling sessions going away, especially in a consumer application.
  * One route is to have a daemon that looks for aged sessions and deletes them.
  * Another approach is to partition the session table into twelve database segmenets and every two hours rotating the segments, deleting everything in the oldest segment and then directing all inserts to it (dumping sessions that were active for twenty-four hours).

## When to Use It

* The great appeal of *Server Session State* is its simplicity.

* The effort of using *Server Session State* depends on if you can get away with the in-memory implementation and, if not, how much help your application server platform gives you.

* The programming effort comes into play in **session maintenance**, particularly if you have to roll your own support to enable clustering and failover. It may work out to be more trouble than your other options, especially if you don't have much session data to deal with or if your session data is easily converted to tabular form.
