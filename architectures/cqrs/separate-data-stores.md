# Separate data stores

For greater isolation, you can physically separate the read data from the write data. In that case, the read database can use its own data schema that is optimized for queries.

For example, it can store a _materialized view_ of the data, in order to avoid complex joins or complex ORM mappings. It might even use a different type of data store. For example, the write database might be relational, while the read database is a document database.

If separate read and write databases are used, __they must be kept in sync__. Typically this is accomplished by having the write model publish an event whenever it updates the database. This __must occur in a single transaction__.

> See [Event-driven architecture style](https://docs.microsoft.com/en-us/azure/architecture/guide/architecture-styles/event-driven).

![](2022-08-08-14-51-52.png)
