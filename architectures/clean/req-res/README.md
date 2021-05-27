# Request and Response Models

Use cases expect input data, and they produce output data. However, a well-formed use case object *should have no inkling about the way that data is communicated* to user or to any other component.

The use case accepts simple request data structures for its input and returns simple response data structures as its output. These data structures are not dependent on anything. This *lack of dependencies is critical*. If the request and response models are not independent, then the uise cases that depend on them will be indirectly bound to whatever depenedencies the models carry with them.

> You might be tempted to have these data structures contain references to Entity objects but the purpose of these two objects is very different. Over time, they will change for very different reasons, so tying them together in any way violates the *Common Closure* and *Single Responsibility* principles. The result would be lots of tramp data, and lots of conditionals in your code.
