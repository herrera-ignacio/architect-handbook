# Concurrency

* Overview
* Essential Problems
  * Lost Updates
  * Inconsistent Reads
* Execution Contexts
  * Request
  * Session
  * Process
  * Thread
  * Transactions
* Isolation and Immutability

## Overview

Whenever you have multiple processes or threads manipulating the same data, you run into concurrency problems.

> "One of the great ironies of enterprise application development is that few branches of software development use concurrency more yet worry about it less. The reason enterprise developers can get away with a naive view of concurrency is *transaction managers*" - Martin Fowler & David Rice

Transactions provide a framework that helps avoid many of the most tricky aspects of concurrency in an enterprise application. As long as you do all your data manipulation within a transaction, nothing really bad will happen to you.

> "Sadly, this doesn't mean we can ignore concurrency problems completely, for the primary reason that many interactions with a system can't be placed within a single database transaction." - Fartin Fowler & David Rice

This forces us to manage concurrency in situations where data spans transactions. The term we use is **offline concurrency**, that is, concurrency control for data that's manipulated during multiple database transactions.

Another complicated area is **application servers**, supporting multiple threads in an application server system. For this you can use server platforms that take caare of much of it for you.

## Essential Problems

> Concurrency problems occu when more than one active agent, such as a process or thread, has access to the same piece of data.

Problems will be illustrated with examples from source code control systems used by teams to coordinate changes to a code base.

Both problems cause a failure of **correctness** (or safety), and they result in incorrect behavior that would not have occurred without two people trying to work with the same data at the same time.

The **essential problem** of any concurrent programming is that it's not enough to worry about correctness; you also have to **worry about liveness**: how much concurrent activity can go on. Often people need to sacrifice some correctness to gain more liveness, depending on the seriousness and likelihood of the failures and the need for people to work on their data concurrently.

### Lost Updates

Say Martin edits a file to make some changes to the `checkConcurrency` method, a task that takes a few minutes. While he's doing this, David alters the `updateImportantParameter` method in the same file. David starts and finishes his alteration before Martin does.

This is unfortunate. When Martin read the file it didn't include David's update, so when Martin writes the file it writes over the version that David updated and Davi's update is lost forever.

### Incosistent Reads

An *inconsistent read* occurs when you read two things that are correct pieces of information but not correct at the same time.

Say Martin wishes to know how many classes are in the concurrency package, which contains two subpackages for locking and multiphase. Martin looks in the locking package and sees seven classes. At this point he gets a phone call from Roy on some abstruse question. While Martin's answering the phone, David finishes dealing with a bug in the four-phase lock code and adds two classes on the locking package and three classes to the five that were in the multiphase package.

His phone call over, Martin looks in the multiphase package to see how many classes there are and sees eight, producing a grand total of fifteen. Sadly, fifteen classes was never the right answer. The correct answer was twelve before Davi's update and seventeen afterward. Either answer would have been correct, even if not current, but fifteen was never correct.

This problem is called an inconsistent read because the data that Martin read was inconsistent.

## Execution Contexts

> Whenever processing occurs in a system, it occurs in some context and usually in more than one.

From the perspective of interacting with the outside world, two important contexts are the *request* and the *session*.

> Server software in an enterprise application sees both requests and sessions from two angles, as the server from the client and as the client to other systems. Thus, you'll often see multiple sessions: HTTP sessions from the client and databases sessins with various databases.

### Request

A *request* corresponds to a single call from the outside world which the software works on and for which it optionally sends back a response.

During a request the processing is largely in the server's court and the client is assumed to wait for a response. Some protocols allow the client to interrupt a request before it gets a response. More often a client may issue another request that may interfere with one it just sent. So a client may ask to place an order and then issue a separate request to cancel that order.

From the client's view the two requests may be obviously connected, but depending on your protocol that may not be so obvious to the server.

### Session

A *session* is a long-running interaction between a client and a server. It may consist of a single request, but more commonly it consists of a series of requests that the user regards as a consistent logical sequence.

Commonly a session will begin with a user logging in and doing various bits of work that may involve issuing queries and one or more business transactions. At the end of the session the user logs out, or he may just go away and assume that the system interprets that as logging out.

### Process

Usuall a heavyweight execution context that provides a lot of isiolation for the internal data it works on.

### Thread

Lighter-weight active agent that's set up so that multiple threads can operate in a single process, favoring a good utilization of resources.

However, threads usually share memory, and such sharing leads to concurrency problems.

Some environments allow you to control what data a thread may access, aallowing you to have **isolated threads** that don't share memory.

### Transactions (database context)

Transactions pull together several requests that the client wants treated as if they were a single request. They can occur from the application to the database (a system transaction) or from the user to an application (a business transaction).

## Isolation and Immutability

Two common solutions for concurrency problems: *isolation* and *immutability*.

With **isolation**, you partition the data so that any piece of it can only be accessed by one active agent. With it you arrange things so that the program enters an isolated zone, within which you don't have to worry about concurrency.

> "Good concurrency design is thus to find ways of creaing such zones and to ensure that as much programming as possible is done in one of them." - Martin Fowler & David Rice

You only get concurrency problems if the data you're sharing can be modified. So one way to avoid concurrency conflicts is to recognize **immutable data**. By identifying some data as immutable, or at least immutable almost all the time, we can relax our concurrency concerns for it and share it widely.

Another option is to separate applications that are only reading data, and have them use copied data sources, from which we can then relax all concurrency controls.
