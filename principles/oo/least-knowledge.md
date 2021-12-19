# Least Knowledge

The Principle of Least Knowledge guides us to *reduce the interactions* between objects to just a few close *friends*. This means you should be careful of the number of classes an object interacts with and also how it comes to interact with those classes.

This principle prevents us from creating designs that have a large number of classes coupled together so that changes in one part of the system cascade to another parts.

Take any object, from any method in that object, the principle says we should *only* invoke methods that belong to:

* The object itself
* Objects passed in as a parameter to the method
* Any object the method creates or instantiates
* Any components of the object (HAS-A relationship)

> Notice that these guidelines tell us *not to* call methods on objects that were returned from calling other methods.
