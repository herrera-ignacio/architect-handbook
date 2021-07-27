# Layer Supertype

> A type that acts as the supertype for all type in its layer.

* Overview
* How It Works
* When to Use It

## Overview

It's not uncommon for all the objects in a layer to have methods you don't want to have duplicated throughout the system. You can move all of this behavior into a common *Layer Supertype*.

## How It Works

All you need is a *super class* for all the objects in a layer. If you have more than one kind of object in a layer, it's useful to have more than one *Layer Supertype*.

> For example, a Domain Object super class for all the domain objects in a *Domain Model*. Common features, such as the storage and handling of *Identity Fields*, can go there. Similarly all *Data Mappers* in the mapping layer can have a super class that relies on the fact that all domain objects have a common super class.

## When to Use It

Use *Layer Supertype* when you have a common features from all objects in a layer.
