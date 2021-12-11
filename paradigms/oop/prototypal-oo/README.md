# Prototypal vs Classical Inheritance 

## Overview

In **class-based** languages the _classes_ are defined beforehand and the _objects_ are instantiated based on the classes. If two objects _apple_ and _orange_ are instantiated from the class _Fruit_, they are inherently fruits and it is guaranteed that you may handle them in the same way.

In **prototype-based** languages the _objects_ are the primarty entities. No _classes_ even exist. The _prototype_ of an object is just another object to which the object is linked. Every object has one prototype link (and only one). New objects can be created based on already existing objects chosen as their prototype. You may call two different objects _apple_ and _orange_ a fruit, if the object _fruit_ exists, both apple and orange may have fruit as their prototype. The idea of the fruit class doesn't exist explicitly, but as the equivalence class of the object's sharing the same prototype. The attributes and methods of the prototype are delegated to all the objects of the equivalence class defined by this prototype. The key difference is that the attributes and methods _owned individually_ by the object may not be shared by others of the same equivalence class, thus it is not guaranteed that two objets linked to the same prototype may be handled the same way.

Only single inheritance can be implemented through the prototype.

## Classical Inheritance Drawbacks

> Resources:
> * https://www.youtube.com/watch?v=lKCCZTUx0sI&t=1s
