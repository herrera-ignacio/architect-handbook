# Dynamic Dispatch / Message Passing

It is the responsibility of the object, not any external code, to select the procedural code to execute in response to a method call, typically by looking up the method at run time in a table associated with the object. This is known as _Dynamic Dispatch_ and distinguishes an object from an Abstract Data Type (or module), which has a fixed (static) implementation of the operations for all instances.

If the call variability relies on more than the single type of the object on which it is called (i.e. at least one other parameter object is involved in the method choice), one speaks of _Multiple Dispatch_ (some languages such as C++ provides with features like _Function Overloading_).

A method call is also known as _Message Passing_. It is conceptualized as a message (the name of the method and its input parameters) being passed to the object for dispatch.