# Record Set

> An in-memory representation of tabular data.

* Overview
* How It Works
* When to Use It

## Overview

![](2021-07-28-01-08-36.png)

For a long time, the dominant way to represent data in a database has been the tabular relational form. On top of this has come a wealth of tools for building UI's quickly that rely on the fact that the underlying data is relational, and they provide UI widgets fof various kinds that make it easy to view and manipulate this data with almost no programming.

The idea of the *Record Set* is to **provide an in-memory structure that looks exactly like the result of an SQL query but can be generated and manipulated by other parts of the system**.

## How It Works

* A *Record Set* is usually something that you won't build yourself but rather is provided by the vender of the software platform you're working with.

* It looks exactly like the result of a database query, meaning you can use the classical two-tier approach of issuing a query and throwing the data directly into a data-aware UI.

* You can easily create a *Record Set* yourself or take one that has resulted from a database query and easily manipulate it with domain logic code.

* The ability to disconnect the *Record Set* from its link to the data source allows you to pass the *Record Set* around a network without having to worry about database connections. Furthermore, if you can then easily serialize the *Record Set* it can also act as a *Data Transfer Object*.

* Most implementations use an **implicit interface**, meaning that to get information out of the *Record Set* you invoke a generic method with an argument to indicate which field you want. An **explicit interface** requires a class with defined methods and properties. Implicit interfaces are flexible in that you can use a generic *Record Set* for any kind of data, and it saves you having to write a new class every time you adefine a new kind of *Record Set*. The tradeoff of implicit interfaces is that the compiler loses all type iunformation and you have to manually enter it to get the information you want.

## When to Use It

The value of *Record Set* comes from **having an environment that relies on it as a common way of manipulating data**. A lot of UI tools use *Record Set*, and that's a compelling reason to use them yourself.

If you have such an environment, you should probably use *Table Module* to organize your domain logic:

1. Get a *Record Set* from the database.
2. Pass it to a *Table Module* to calculate derived information.
3. Pass it to a UI for fisplay and editing
4. Pass it back to a *Table Module* for validation.
5. Commit the updates to the database.
