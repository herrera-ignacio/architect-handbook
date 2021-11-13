# Decomposing the Database

Microservices work best when we practice *information hiding*, which in turn typically leads us toward microservices totally encapsulating their own data storage and retrieval mechanisms.

Splitting a database apart is far from a simple endeavor, however. We need to consider issues of:

* Data synchronization during transactions
* Logical versus physical schema decomposition
* Transactional integrity
* Joins
* Latency
* More...
