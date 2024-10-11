# Testable Architectures

If your system architecture is all about the use cases, and if you have kept your framework at arm's length, then you should be able to unit-test all those use cases without any of the frameworks in place.

You shouldn't need the web server running to run your tests. You shouldn't need the database connected to run your tests.

Your _Entity_ objects should be plain old objects that have no dependencies on frameworks or databases or other complications. Your use cases objects should coordinate your Entity objects.
