# Narratives Summary

> This is a summary of the narratives/general architectural concerns explained by Martin Fowler n *Patterns of Enterprise Application Architecture*.

* Making a Decision
* Starting with the Domain Layer
* Down to the Data Source Layer
  * Data Source for *Table Module*
  * Data Source for *Domain Model*
* The Presentation Layer
* Web Services

## Making a Decision

In the end, you have to make, and live with, the decisions yourself. Architectural refactoring is hard, and we're still ignorant of its full costs, but it isn't impossible.

Even if you dislike the full story of **extreme programming (Beck XP)**, you should still onsider seriously three technical practices:

* Continuous Integration
* Test-Driven-Development (TDD)
* Refactoring

They'll make it much easier for you to change your mind when you discover you need to, and you will most likely need to.

## Starting with the Domain Layer

The start of the process is deciding which domain logic approach to go with. The three main contenders are **Transaction Script**, **Table Module**, and **Domain Model**.

The strongest force that drives you through this trio is the complexity of the domain logic, something currently impossible to quantify, or even qualify, with any degree of precision. But other factors also play in the decision, in particular, the difficulty of the connection with a database.

The simplest is *Transaction Script*, it fits with a precedural model and nicely encapsulates the logic of each system transaction in a comprehensible script. Its great failing is that it doesn't deal well with complex business logic, being particularly susceptible to duplicate code.

At the other end of the scale is the *Domain Model*, which is the way to go for complex domain logic. Yet it has its faults. High on the list is the difficulty of learning how to use a domain model, because done poorly it's a disaster. The second big difficulty is its connection to a relational database. The complexity of many O/R mapping patterns is the result.

*Table Module* represents an attractivce middle groud between these poles. It can handle domain logic better than *Transaction Scripts*, and it fits really well with a relational database. If you have an environment such as .NET, where many tools orbit around the *Record Set*, then *Table Module* works nicely.

> Tools you have also affect your architecture. Sometimes you're able to choose the tools based on the architecture, and in theory that's the way you should go. In practice, however, you often have to match your architecture to your tools.

From here we go downward to the database layer, but now the **decisions are shaped by the context of your domain layer choice**.

## Down to the Data Source Layer

The simplest *Transaction Scripts* contain their own database logic, but we want to avoid that even in the simplest cases. **Separating the database** delimits two parts that make sense as separate.

The database patterns to choose from here are **Row Data Gateway** and **Table Data Gateway**.

The choice between the two depends much on the facilities of your implementation platform and on where you expect the application to go in the future. With a *Row Data Gateway* each record is read into an object with a clear and explicit interface. With *Table Data Gateway* you may have less code to write sicne you don't ned all the accessor code to get at the data, but you end up with a much more implicit interface that relies on accessing a record set structure that's a little more than a glorified map.

The key decision, however, lies in the rest of your platform. Having a platform that provides a lot of tools that work well with *Record Set*, particularly UI tools or transactional disconnected record sets, tilts you decisively in the direction of a *Table Data Gateway*.

You usually don't need any of the other O/R mapping patterns in this context. The **structural mapping issues** are pretty much absent since the in-memory structure maps to the database structure so well. You might consider a *Unit of Work*. You neither have to worry about most **concurrency issues** because the script often corresponds almost exactly to a system transaction. The common exception is where one request pulls data back for editing and the next request tries to save the changes. In this case *Optimistic Offline Lock* is almost always the best choice. Not only is it easier to implement, it also usually fits users' expectations and avoids the problem of a hanging session leaving all sorts of things locked.

### Data Source for *Table Module*

The main reason to choose *Table Module* is the presence of a good *Record Set* framework. In this case, you'll want a database mapping pattern that works well with *Record Sets*, and that leads you inexorably toward *Table Data Gateway*.

In the best cases, the *Record Set* has some kind of concurrency contro lmechanism built in, which effectively turns it into a *Unit of Work*.

### Data Source for *Domain Model*

> In many ways the big weakness of *Domain Model* is that the **conection to the database is complicated**.

If your *Domain Model* is fairly simple, say a couple of dozen classes that are pretty close to the database, then an *Active Record* makes sense.

If you want to decouple things a bit, you can use either *Table Data Gateway* or *Row Data Gateway* to do that. Whether you separate or not isn't a huge deal either way.

As things get more complicated, you'll need to consider *Data Mapper*. This is the approach that delivers on the promise of keeping your *Domain Model* as independent as possible of all the other layers. But *Data Mapper* is also the most complicated one to implement.

> Unless you either have a strong team or you can find some simplifications that make the mapping easier to do, it's recommended getting a mapping tool.

Once you choose *Data Mapper* most of the patterns in O/R mapping come into play. In particularly, *Unit of Work* acts as a focal point for **concurrency control**.

## The Presentation Layer

In many ways the presentation is **relatively independent of the choice of the lower layers**.

It's preferable to pick an HTML browser if you can get away with it and a rich client if that's not posible.

> A rich client will give you a nicer UI, but then you need a certain amount of control and deployment of your clients. They will usually take more effort to program because they tend to be more sophisticated.

If you go the HTML route, you have to decidehow to structure your application. **Model View Controller** is recommended as the underpinning for your design. That done, you're left with two decisions, one for the *controller* and one for the *view*.

You can go with **Page Controller** and **Template View** (for example, Visual Studio would do this for you in the case of .NET). If you use Java, you have a choice of Web frameworks to consider (Struts for example will lead you to a **Front Controller** and a *Template View*).

Given a freer choice, Fowler recommends *Page Controller* if your site is more document oriented, particularly if you have a mix of static and dynamic pages. More complex navigation and UI lead you toward a *Front Controller*.

On the view front the choice depends on whether your team uses server pages or XSLT in programming. *Template View* has the edge at the moment, although Fowler says to like the added testability of **Transform View**. If you have the need to dispalay a common site with multiple looks and feels, you should consider **Two Step View**.

How you communicate with the lower layer depends on what kind of layers they are and whether they're always going to be in the same process, which is preferable so you don't have to worry about slow inter-process calls. If you can't do that, you should wrap your domain layer with **Remote Facade** and use **Data Transfer Object** to communicate to the Web server.

## Web Services

Web services are more about application integration rather than application construction. **You shouldn't try to break uup a single application into Web services that talk to each other unless you really need to**. Rather, build your application and expose various parts of it as Web services, treating those Web services as **Remote Facades**. Above all, don't let all the buzz about how easy it is to build Web services make you forget about the **First Law of Distributed Object Design** (*Don't distribute your objects*).
