# Web Presentation

> Web-browser-based user interfaces bring with them a lot of advantages: no client software to instsall, a common UI approach, and easy universal access.

* Web Server
  * As a Script
  * As a Server Page
* MVC: Model View Controller
  * Overview
  * Why
  * Application Controller

## Web Server

Preparing a Web app **begins with the server software itself**. Usually this indicates which URLs are to be handled by which programs.

Often a single Web server can handle many kinds of programs. These programs may be dynamic and can be added to a server by placing them in an appropriate directory.

> The Web server's job is to interpreter the URL of a request and hand over control to a Web server program.

There are two main forms of structuring a program in a Web server: as **a script** or as **a server page**.

> *Script style* works best for interpreting the request and the *Server Page style* works best for formatting a response.

There's the obvious option to use a script for request interpretation and a server page for response formatting. This separation is in fact an old idea that first surfaced in user interfaces with MVC.

### As a Script

The script form is a program, usually with functions or methods to handle the HTTP call.

> Examples include CGI scripts and Java servlets.

The script can be broken down into subroutines, and can create and use other services. It gets data from the Web page by examining *the HTTP request object*, which is a string.

> Some platforms, such as Java servlets, do this parsing for the programmer, which allows the programmer to access the information from the request through a keyword interface.

The output of the Web server is another string, *the response*, which the script can write to using the usual write stream operations in the language.

### As a Server Page 

In *server pages*, the program is structured around the returning text page. You write the return page in HTML and insert into the HTML scriptlets of code to execute at certain points.

> Examples of this approach include PHP, ASP, and JSP.

The server page approachs **works well when there's little processing of the response**, such as "*Show me details of album #1234*". 

## MVC: Model View Controller

> "MVC is a widely referenced pattern but one that's often misunderstood. A main reason for the confusion was the use of the word '*controller*'. [...] Controller is used in a number of different contexts, and I've usually found it used in a different way to that described in MVC. As a result I prefer to use the term **input controller** for the controller in MVC." - Fowler

### Overview

A *request* comes in to an **input controller** which pulls information off the *request*. It then forwards the bussiness logic to an appropriate model object. The **model object** talks to the **data source** and does everything indicated by the *request* as well as gather information for the *response*. When it's done it returns control to the **input controller**, which looks at the results and decides which **view** is needed to display the *response*. It then passes control, together with the *response data*, to the **view**.

The **input controller**'s handoff to the **view** often isn't always a straight call but often involves forwarding with the data placed in an agreed place on some form of HTTP session object that's shared between the **input controller** and the **view**.

![](2021-06-19-16-02-10.png)

> A broad picture of how the model, view, and input controller roles work together in a Web server. The controller handles the request, gets the model to do the domain logic, and then gets the view to create a response based on the model.

### Why

The first, and most important, reason for applying *MVC*, is to **ensure that the models are completely separated from the Web presentation**. This makes it easier to modify the presentation as well as easier to add additional presentations later.

> Putting the processing into separate *Transaction Script* or *Domain Model* objects will make it easier to test them as well. This is particularly important if you're using a server page as your view.

### Application Controller

> At this point we come to a second use of the word *"controller"*.

A lot of UI designs separate the *presentation objects* from the *domain objects* with an intermediate layer of **Application Controller** objects.

The purpose of an *Application Controller* is to handle the flow of an application, deciding which screens should appear in which order. It may appear as part of the *presentation layer*, or you can think of it as a separate layer that mediates between the *presentation* and *domain layers*.

*Application Controllers* may be written to be independent of any particular presentations, in which case they can be reused between presentations. This works well if you have different presentations with the same basic flow and navigation, although often it's best to give different presentations a different flow.

Not all systems need an *Application Controller*. They're **useful if your system has a lot of logic about the order of screens and the navigatio nbetween them.** They're also useful **if you haven't got a simple mapping between your pages and the actions on the domain**. But if someone can pretty much see any screen in any order, you'll porbably have little need for an *Application Controller*.

> "A good test is this: If the machine is in control of the screen flow, you need an *Application Controller*; if the user is in control, you don't." - Martin Fowler.
