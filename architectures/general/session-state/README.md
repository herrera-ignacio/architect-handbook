# Session State

* Overview
* The Value of Statelessness
* The Problem with Statelessness
* Session State
  * Storing

## Overview

The differences between business and system transactions underlie much of the debate over stateless versus stateful sessions. The difference between them affects how to store the data that's used within a business transaction but isn't yet ready to be committed to the general database of record.

> "I think the fundamental issue is realizing that some sessions are inherently stateful and then deciding what to do about the state." - Martin Fowler

## The Value of Statelessness

When people refer to a stateless server they mean an **object that doesn't retain state between requests**. Such an object may well have fields, but when you invoke a method on a stateless server the values of the fields are undefined.

however, imagine that you want to keep track of some data requested by a particular client IP address. You can keep this in a list maintained by the server object. However, this list must persist between requests and thus you have a stateful server object.

The primary issue with stateful servers is **server resources**. Any stateful server object needs to keep all its state while waiting for a user to finish their session, thus you'd need more server objects (one per user for example) that will be sitting around doing nothing more than waiting most of the time. A stateless server object, however, can process other requests from other sessions, and you can use less objects but that are fully employed all the time.

The point is that, **if we have no state between method calls, it doesn't matter which object services the request, but if we do store state we need to always get the same object**.

Statelessness allows us to **pool our server objects so that we need fewer objects to handle more users**. The more idle users we have, the more valuable stateless servers are.

> Stateless servers are very useful on high-traffic web sites. Statelessness also fits in well with the Web since HTTP is a stateless protocol.

## The Problem with Statelessness

**Many client interactions are inherently stateful**.

> Consider the shopping cart metaphor that fuels most e-commerce applications. The user's interaction involves browsing several books and picking which ones to buy. The shopping cart needs to be remembered for the user's entire session.

Essentially we have a sateful business transaction, which implies that the session has to be stateful.

> If I only look at books and don't buy anything, my session is stateless, but if I buy, it's stateful.

The good news is that **we can use a stateless server to implement a stateful session**; the interesting news is that **we may want not want to**.

## Session State

The details of the shopping cart are **session state**, meaning that the data in the cart is **relevant only to thar particular session**.

Session state is distinch from what is called **record data**, which is the long-term persistent data held in the database and visible to all sessions.

**Session state needs to be commited to become record data**.

Since session state is **within a business transaction**, it has many properties that people usually think of with transactions, such as ACID.

One consequence is the effect on **consistency**. Session state isn't going to match the validation rules while it's being worked on; it will only when the business transaction commits.

> While the customer is editing an insurance policy, the current state of the policy may not be legal. The customer alters a value, uses a request to send this to the system, and the system replies indicating invalid values. Those values are part of the session state, but they aren't valid.

The biggest issue with session state is **dealing with isolation**.

> Many things can happen while a customer is editing a policy. The most obvious is two people editing the policy at the same time. But ddirect changes are not the only problem. Consider that there are two records, the policy itself and the customer record. The policy has a risk value that depends partially on the zip code in the customer record. The customer begins by editing the policy and after ten minutes does something that opens the customer record so he can see the zip code. However, during that time someone else has changed the zip code and the risk value, leading to an *inconsistent read*.

Not all data held by the session counts as session state. The session may cache some data that doens't really need to be stored between requests but is stored to improve performance.

### Storing

There are three **not mutually exclusive** basic choices:

* **Client Session State**: Stores the data on the client. There are several ways to do this such as encoding data in a URL, using cookies, serializing the data into some hidden field on a Web form, and holding the data in objects on a rich client.

* **Server Session State**: May be as simple as holding the data in memory between requests. Usually, however, there's a mechanism for storing the session state somewhere more durable as a serialized object. The object can be stored on the application server's local file system, or it can be placed in a shared data source. This could be a simple database table with a session ID as a key and serialized object as a value.

* **Database Session State**: This is also server-side storage, but it involves breaking up the data into tables and fields and storing it in the database much as you would store more lasting data.

Using *Client Session State* means the session data needs to be transferred across the wire with every request, even if the client doesn't need it for display. If we're talking about only a few fields, this is no big deal, otherwise you might need to worry about **bandwidth**. You also have to worry about **security** and **integrity**. Unless you encrypt the data, you have to assume that any malicious user could edit your session data.

Session data has to be **isolated**. Indeed, part of the meaning of sessio ndata is that it's unseen to anything outside the session. This becomes a tricky issue if you use *Database Session State*, because you have to work hard to isolate the session data from the record data that sits in the database.

If you have lot of users, you'll want to consider **clustering** to improve your troughput. **Session migration** allows a session to move from server to server as one server handles one request and other servers take on the others. Its opposite is **server affinity**, which forces one server to handle all requests for a particular session.

*Server migration* leads to a better balancing of your servers, particularly if your sessions are long. However, there can be awkward if you're using *Server Session State* because often only the machine that handles the session can easily find that state. There are ways around that that blur the lines between *Database Session State* and *Server Sesion State*.

In trying to guarantee *server affinity*, the clustering system can't always inspect the calls to see which session they're part of. As a result, it will increase the affinity so all calls from one client go to the same application server. Often this is done by the client's IP address. If the client is behind a proxy, that could mean that many clients are all using the same IP address and are thus tied to a particular server.

If the server is goign to use the session state, it needs to get it into a form that can be used quickly. If you use *Client Session State*, you often need to transform it into the form you want for your server. If you use *Database Session State*, you need to go to the database to get it (and maybe do some transforming as well).

> If you have a public retail system, you probably don't have that much data going into each session, but you do have a lot of mostly idle users. For that reason *Database Session State* can work nicely in performance terms. For a leasing system you run the risk of schlepping masses of data in and out of the database with each request. That's when *Server Session State* can give you better performance.

One of the big bugbears in many systems is when a user cancels a session and says forget it. *Client Session State* certainly wins here because you can forget about that user easily. In the other approaches you need to be able to clean out session state when you realize it's canceled, as well as set up a system that allows you to cancel after some timeout period.

> This is particularly awkward with B2C applications because the user usually doesn't actually say for get it, it just disappears and doesn't come back.

A system can cancel too, resulting in a client crashing and a session getting lost. *Server Session State* may or may not survive, depending on whether the session object is backed up to a nonvolatile store and where the store is kept. *Client Session State* won't survive a client crash, but should survive the rest going down.

> "My preference is for *Server Session State*, particularly if the memento is stored remotely so it can survive a server crash. I also like *Client Session State* for session IDs and for session data that's very small. I don't like *Database Session State* unless you need failover and clustering and if you can't store remote mementos or if isolation between sessions isn't an issue for you." - Martin Fowler
