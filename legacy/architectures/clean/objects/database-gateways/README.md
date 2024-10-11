# Database Gateways

Between the use case interactors and the database are the *database gateways*. These gateways are *polymorphic interfaces that contain methods for every create, read, update, or delete operation that can be performed by the application* on the database.

For example, if the application needs to know the last names of all the users who logged in yesterday, then the `UserGateway` interface will have a method named `getLastNamesOfUsersWhoLoggedInAfter` that takes a `Date` as its argument and returns a list of last names.

Recall that we do not allow SQL in the use cases layer; instead, we use gateway interfaces that have appropriate methods. Those gateways are implemented by classes in the database layer. __The gateway implementation is the humble object__. It simply uses SQL, or whatever the interface to the database is, to access the data required by each of the methods. __The interactors, in contrast, are not humble because they encapsulate application-specific business rules__. Although they are not humble, those interactors are *testable*, because the gateways can be replaced with appropriate stubs and test-doubles.
