# MVC: Model-View-Controller

> MVC is commonly used for developing UIs that divides the related program logic into three interconnected elements. This is done to separate internal representations of information from the ways information is presented to and accepted from the user.

## Problem

Decoupling objects so that changes to one can affect any number of others without requiring the changed object to know details of the others. Particularly, allow for multiple representations by decoupling views from application logic.

## Solution

MVC consists of three kinds of objects:

* __Model__: Application object. It directly manages the data, logic and rules of the application.

* __View__: Any representation of information.

* __Controller__: Defines the way the user interface reacts to user input (it accepts input and converts it to commands for the model or view).

In addition to dividing the application into these three components, MVC defines the interactions between them:

* _Model_ is responsbile for managing the data of the application. It receives user input from the _Controller_.

* _View_ renders presentation of the _Model_ in a particular format.

* _Controller_ responds to the user input and performs interactions on the data model objects. The controller receives input, optionally validates it, and then passes the input to the _Model_.

## Consequences

* Increase flexibility and reuse by decoupling models, controllers, and views, from each other.

* Views can be nested. This allows to create a class hierarchy in which some subclasses define primitive objects (e.g, Button) and other classes define composite objects that assemble the primitives into more complex objects.

* Lets you change the way a view responds to user input without changing its visual presentation.
  * MVC encapsulates the response mechanism in a _Controller_ object.
  * There is a class hierarchy of controllers, making it easy to create a new controller as a variantion on an existing one.
  * A view uses an instance of a Controller subclass to implement a partcular response strategy, you can simply replace it.
  * It's even possible to change a view's controller at run-time.

## Related patterns

Main relationships in MVC are given by the _Observer_, _Composite_, and _Strategy_ design patterns, but it uses others such as _Factory Method_ to specify the default controller class for a view and _Decorator_ to add scrolling to a view.
