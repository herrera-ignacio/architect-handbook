# Layering

* Overview
* Benefits
* Downsides
* Some history background

## Overview

When thinking of a system in terms of layers, you imagine the principal sub systems in the software arranged in some form of layer cake, where each layer rests on a lower layer. In this scheme, **the higher layer uses various services defined by the lower layer**, but the lower layer is unaware of the higher layer.

Furthermore, **each layer usually hides its lower layers from the layers above**. 

> You can see Layerin in machine architectures, where layers descend from a programming language with operating system calls into device drivers and CPU instructions sets, and into logic gates inside chips. Networking has FTP layered on top of TCP, which is on top of IP, which is on top of ethernet.

The hardest part of a layered architecture is deciding what layers to have and what the responsibility of each layer should be.

## Benefits

* **A single layer is a coherent whole without knowing much about the other layers**. You can understand how to build an FTP service on top of TCP without knowing the details of how ethernet works.

* You can **substitute layers with alternative implementations.** An FTP service can run without change over ethernet, PPP, or whatever a cable company uses.

* You **minimize dependencies between layers**. If the cable company changes its physical transmission system, providing they make IP work, we don't have to alter our FTP service.

* Layers make good places for **standardization**. TCP and IP are standards because they define how a specific layer should operate.

* Once you have a layer built, you can **use it for many higher-level services**. Higher-level protocols can reuse a lower-level one without having to write their own.

## Downsides

* Layers **encapsulate some, but not all, things well**. As a result you sometime get cascading changes. The classic example of this is in a layered enterprise application is adding a field that needs to display on the UI, must be in the database, and thus must be added to every layer in between.

* **Extra layers can harm performance**. At every layer things typically need to be transformed from one representation to another. However, the encapsulation of an underlying function often gives you efficiency gains that more than compensate. A layer that controls transactions can be optimized and will then make everything faster.

## Some history background

### The problem

The notion of layers became more apparent in the '90s with the rise of **client-server** systems. These were two-layer systems: The client held the user interface and other application code, and the server was usually a relational database.

If the application was all about display and simple update of relational data, then these client-server systems worked very well. The problem came with *domain logic*: business rules, validations, calculations, and the like. Usually people would write these on the client, but this was awkward and usually done by embedding the logic directly into the UI screens. As the domain logic got more complex, the code **became very difficult to work with**.

Furthermore, embedding logic in screens made it **easy to duplicate code**, which meant that **simple changes resulted in hunting down similar code in many screens**.

An alternative was to put the domain logic in the database as stored procedures. However, this gave limited structuring mechanisms, which again led to awkward code. Also, many people liked relational databases because SQL was a standard that would allow them to change their database vendor without too high a porting cost. But because stored procedures were all proprietary, they limited this.

### The proposal: Three-layer system

At the same time that client-server was gaining popularity, the **OOP** was rising. The object community proposed a **three-layer system**: In this approach you have a presentation layer for your UI, a domain layer for your domain logic, and a data source.

Despite this, it made little headway. The truth was that many systems were simple, or at least started that way. And although the three-layer approach had many benefits, the tooling for client-server **was compelling if your problem was too simple**. The client-server tools also were difficult, or even impossible, to use in a three-layer configuration.

### The Web

Suddenly people wanted to deploy client server applications with a Web browser. However, if all your business logic was buried in a rich client, then **all your business logic needed to be redone to have a Web interface**.

A well-designed three-layer system could just add a new presentation layer and be done with it. Furthermore, with Java, OOP became mainstream. The tools that appeared to build Web pages were much less tied to SQL and thus more amenable to a third layer.

> Often *layer* and *tier* concepts are used as synonyms, but most people see *tier* as implying a physical separation. Client-server systems are often described as two-tier system as their separation is physical, but *layers* don't have tu run on different machines.
