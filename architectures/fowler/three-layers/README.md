# Martin Fowler: The Three Principal Layers

* **Presentation**: Handle interaction between user and software. It's responsible of provisioning services and displaying information (e.g., in Windows or HTML, handling user requests like mouse clicks or keyboard hits, HTTP requests, command-line invocations, batch API).

* **Domain**: Also referred to as *business logic*. It involves calculations based on inputs and stored data, validation of any data that comes in from the presentation, and figuring out exactly what data source logic to dispatch, depending on commands received from the presentation.

* **Data Source**: Communication with databases, messaging systems, transaction managers, other packages. This is primarily responsible for storing persistent data.

> A single application can often have multiple packages of each of these three subject areas.

Sometimes the layers are **arranged so that the domain layer completely hides the data source from the presentation**. More often, however, the presentation access the data store directly. While this is less pure, it tends to work better in practice. The presentation may interpret a command from the user, use the data source to upull the relevant data out of the database, and then let the domain logic manipulate that data before presenting it.

**The domain and data source should never be dependent on the presentation**. That is, there should be no subroutine call from the domain or data source code into the presentation code. This rule makes it easier to substitute different presentations on the same foundation and makes it easier to modify the presentation without serios ramifications deeper down.

> Presentation is an external interface for a service your system offers to someone else, whether it be a complex human or a simple remot program. Data source is the interface to things that are providing a service to you.

Although we can identify the three common responsiblity layers of presentation, domain, and data source for every enterprise application, **how you separate them depend depends on how complex the application is**. A simple script to pull data from a database and display it in a Web page may all be one procedure, or the behavior of each layer may be placed in separate subroutines. As the system gets more complex, the three layers can be break into separate classes, and as complexity increases, into separate packages.

> Choose the most appropriate form of separation for your problem but make sure you do some kind of separation, at least at the subroutine level.

## Case study: Hexagonal Architecture

There is a lot of similarity between the presentation and data source layers in that they both are about connection to the outside world. This is the logic behind *Alistar Cockburn's Hexagonal Architecture* pattern, which visualizes any system as a **core surrounded by interfaces to external system**.

Everything external is fundamentally an outside interface, and thus it's a symmetrical view rather than an asymmetric layering scheme as the three-layer system.
