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
* Optimistic and Pessimistic Concurrency Control
  * Preventing Inconsistent Reads
  * Deadlocks

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

## Optimistic and Pessimistic Concurrency Control

What happens when we have **mutable data that we can't isolate**?

Let's suppose that Martin and David both want to edit the Customer file at the same time. With **optimistic locking** both of them can make a copy of the file and edit it freely. If David is the first to finish, he can check in his work without trouble. The concurrency control kicks in when Martin tries to commit his changes. At this point the source code control system detects a conflict between Martin's changes and David's changes. Martin's commit is rejected and it's up to him to figure out how to deal  with the situation.

With **pessimistic locking** whoever checks out the file first prevents anyone else from editing it. So if Martin is first to check out, David can't work with the file until Martin is finished with it and commits his changes.

> "Optimistic lock is about conflict detection while a pessimistic lock is about conflict prevention." - Martin Fowler & David Rice

The essence of the choice between optimistic and pessimistic locks is the frequency and severity of conflicts. If conflicts are sufficiently rare, or if the consequences are no big deal, you should usually pick optimistic locks because they give you better concurrency and are usually easier to implement. However, if the results of a conflict are painful for users, you'll need to use a pessimistic technique instead.

### Preventing Inconsistent Reads

Consider this situation. Martin edits the Customer class and adds some calls to the Order class. Meanwhile David edits the Order class and changes the interface. David compiles and checks in; Martin then compiles and checks in. Now the shared code is broken because Martin didn't realize that the Order class was altered underneath him.

> Some source code control systems will spot this inconsistent read, but others require some kind of manual discipline to enforce consistency, such as updating your files from the trunk before you check in.

**Pessimistic locks** have a well-worn way of dealing with this problem through read and write locks. To read data you need a read (or shared) lock; to write data you need a write (or exclusive) lock. Many people can have read locks on the data at one time, but if anyone has a read lock nobody can get a write lock. Conversely, once somebody has a write lock, then nobody else can have any lock.

**Optimistic locks** usually base their conflict detection on some kind of version marker on the data. This can be a timestamp or a sequential counter. To detect lost updates the system checks the version marker of your update with the version marker of the shared data. If they're the same, the system allows the update and updates the version marker.

Detecting an inconsistent read with optimistic locks is similar: In this case every bit of data that was read also needs to have its version marker compared with the shared data. Any differences indicate a conflict.

> controlling access to every bit of data that's read often causes unnecessary problems due to conflicts or waits on data thaat doesn't actually matter that much. You can reduce this burden by separating out data you've *used* from data you've merely read.

Another way is using **Temporal Reads**. These prefix each read of data with some kind of timestamp or immutable label, and the database returns the data as it was according to that time or label. The problem is that the data source needs to provide a full temporal history of changes, which takes time and space to process. You may need to provide this capability for specific areas of your domain logic.

### Deadlocks

A particular problem with **pessimistic techniques** is **deadlock**.

Say Martin starts editing the Customer file and David starts editing the Order file. David realizes that to complete his task he needs to edit the Customer file too, but Martin has a lock on it so he has to wait. Then Martin realizes he has to edit the Order file, which David has locked. They are now deadlocked, **neither can make progress until the other completes**.

It's very easy to think you have a deadlock-proof scheme and then fine some chain of events you didn't consider.

> "We prefer very simple and conservative schemes for enterprise application development. They may cause unecessary victims, but that's usually much better than the consequences of missing a deadlock scenario." - Martin Fowler and David Rice

#### Deal with deadlocks

There are various techniques to deal with deadlocks.

One is to have software that can detect a deadlock when it occurs. In this case you pick a **victim**, who has to throw away his work and his locks so the others can make progress. **Deadlock detection** is very difficult and causes pain for victims.

A similar approach is to **give every lock a time limit**. Once you hit that limit you lose your locks and your work, essentially becoming a victim. **Timeouts** are easier to implement than a deadlock detection mechanism, but if anyone holds locks for a while some people will be victimized when there actually is no deadlock present.

#### Prevent deadlocks

Other approaches try to stop deadlocks occurring at all. Deadlocks essentially occur when people who already have locks try to get more (or to upgrade from read to write locks). Thus, one way of preventing them is to **force people to acquire all their locks at once** at the beginning of their work and then **prevent them gaining more**.

You can **force an order on how everybody gets locks**. An example might be to always get locks on files in alphabetical order. This way, once David had a lock on the Order file, he can't try to get a lock on the Customer file because it's earlier in the sequence. At that point he essentially becomes a victim.

You can also make it so that, if Martin tries to acquire a lock and David already has one, Martin automatically becomes a victim. It's a drastic technique, but it's simple to implement.

> You can use multiple schemes. For example, you force everyone to get all their locks at the beginning, but add a timeout in case something goes wrong.
