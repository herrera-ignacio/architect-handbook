# Table Module

> *"A single instance that handles the business logic for all rows in a database table or view."* - Martin Fowler

* Overview
* How It Works
* When to Use It

## Overview

![](IMAGE%201.png)

One of the problems with *Domain Model* is the interface with relational databases. A *Table Module* organizes domain logic with **one class per table** in the database, and a **single instance** of a class contains the various procedures that will act on the data.

> The primary distinction with *Domain Model* is that, if you have many orders, a *Domain Model* will have one order object per order while a *Table Module* will have one object to handle all orders.

## How it Works

The strength of *Table Module* is that it allows you to package the data and behavior together and at the same time play to the strengths of a relational database.

*Table Module* doesn't have a notion of an identity for the objects it's working with. Thus, if you want to obtain the address of an employee, you use a method like `anEmployeeModule.getAddress(long employeeId)`. Every time you want to do something particular to a particular employee you have to pass in some kind of identity reference. Often this will be the *primary key* used in the database.

The tabular data is normally the result of a SQL call and is held in a *Record Set* that mimics a SQL table. The *Table Module* gives you an explicit method-based interface that acts on that data.

> Often you'll need behavior from multiple *Table Modules* in order to do some useful work. Many times you see multiple *Table Modules* operating on the same *Record Set*.

The most obvious example of *Table Module* is the use of one for each table in the database. However, if you have interesting queries and views in the database you can have *Table Modules* for them as well.

![](IMAGE%202.png)

The *Table Module* may be an **instance** or it may be a **collection of static methods**. The advantage of an instance is that it allows you to initialize the *Table Module* with an existing *Record Set*. Instances also make it possible to use inheritance.

The *Table Module* may include queries as factory methods. The alternative is a *Table Data Gateway*, but the disadvantage of this is having an extra mechanism in the design. The advantage is that you can use a single *Table Module* on data from different data sources since you use a different *Table Data Gateway* for each data source.

When you use a *Table Data Gateway* the application first uses the *Table Data Gateway* to assemble data in a *Record Set*. You then create a *Table Module* with the *Record Set* as an argument. if you need behavior from multiple *Table Modules*, you can create them with the same *Record Set*. The *Table Module* can then do business logic on the *Record Set* and pass the modified *Record Set* to the presentation for display and editing using table-aware widgets.

The presentation can't tell if the record sets came directly from the relational database or if a *Table Module* manipulated the data on the way out. After modification in the GUI, the data set goes back to the *Table Module* for validation before it's saved to the database. One of the benefits of this style is that you can test the *Table Module* by creating a *Record Set* in memory without going to the database.

> The structure of the *Table Module* doesn't really depend on the structure of tables in the database butr more on the virtual tables pereceived by the application, including views and queries.

![](IMAGE%203.png)

## When To Use It

*Table Module* is very much based on table-oriented data, so obviously using it makes sense when you're accessing tabluar data using *Recor Set*. It also puts that data structure very much in the center of your code, so you also want the way you access the data structure to be fairly straightforward.

You have to trade off *Domain Model*'s ability to handle complex logic against *Table Module*'s easier integration with the underlying table-oriented data structures.

> In Microsfot COM designs (and .NET), the *Record Set* is the primary repository of data in an application. Record sets can e passed to the UI, where data-aware widgets display information.
