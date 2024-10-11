# Components

> Components are the units of deployment. They are the smallest entities that can be deployed as part of a system.

They can be linked together into a single executable, or aggregated together into a single archive. Or they can be independently deployed as separate dynamically loadad plugins.

> For example, In Java they are `.jar` files. In Ruby, they are `.gem` files. In .Net they are `.dll`. In compiled languages, they are aggregations of binary files. In interpreted languages, they are aggregation of source files.

Well-designed components always retain the ability to be independently deployable and, therefore, independently developable.

With the improvements on storage devices, that got cheaper and faster, we could link several shared libraries in a matter of seconds, and execute resulting program. And so, the **component blugin architecture was born**.

> "A component is a grouping of related functionality behind a nice clean interface, which resides inside an execution environment like an application. (...) A software system is made up of one or more containers (e.g. web applications, mobile apps, stand-alone applications, databases, file systems), each of which contains one or more components, which in turn are implemented by one or more classes (or code). Whether each component resides in a separate jar file is an orthogonal concern." - Simon Brown
