# Interface Adapters

![](../../CleanArchitecture.jpg)

The software in the interface adapters layers is a set of adapters that *convert data from the format most convenient for the use cases and entities, to the data format most convenient for some external agency* such as the database or the web.

> In this layer, for example, that will wholly contain the MVC architecture of a GUI. The presenters, views, and controllers all belong in the interface adapters layer. The models are likely just data structures that are passed from the controllers to the use cases, and then back from the use cases to the presenters and views.

No code inward of this circle should know anything at all about external circles (i.e, the database).
