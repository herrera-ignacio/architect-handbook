# Embedded Value / Aggregate Mapping

> Maps an object into several fields of another object's table.

* Overview
* How It Works
* When to Use It

## Overview

An *Embedded Value* maps the values of an object to fields in the record of the object's owner.

> Many small objects make sense in an OO system that don't make sense as tables in a database (e.g. currency-aware money objects and date ranges).

## How It Works

* When the owning object is loaded or saved, the dependent objects are loaded and saved at the same time.

* The dependent classes won't have their own persistence methods since all persistence is done by the owner.

* You can think of *Embedded Valueof* as a special case of *Dependent Mapping*, where the value is a single dependent object.

## When to Use It

* Simple *Value Objects* like money and date range.

* When storing reference to dependent objects has no relevance outside the context of the owner (e.g. you only load dependents when loading the owner).

* If mapping to an existing schema and a talbe contains data that you split into more than one object in memory.

* Can only be used for fairly simple dependents. For more complex structures, including potentially large object subgraphs, you should consider *Serialized LOB*.
