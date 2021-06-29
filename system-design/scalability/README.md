# Scalability

* Overview
* Scalability vs Performance
* Domains

## Overview

**Scalability** is the property of a system to handle a growing amount of work by adding resources to the system.

In *computing* scalability is a characteristic of computers, networks, algorithms, networking protocosl, programs and applications.

> An example is *search engine*, which must support increasing numbers of users, and the number of topics it indexes.

## Scalability vs Performance

A service is scalable if it results in **increased performance in a manner proportional to resources added**.

* If you have a performance problem, your system is slow for a single user.
* If you have a scalability problem, your system is fast for a single user but slow under heavy load.

## Domains

* A scalable **database managment system** or **online transaction processing system** is one that can be upgraded to process more transactions by adding new processors, devices and storage, and which can be upgraded easily and transparently without shutting it down.

* A **routing protocol** is considered scalable with respect to network size, if the size of the necessary *routing table* on each node grows as *O(log n)*, where *n* is the number of nodes in the network.
  * Some P2P systems like BitTorrent scale well because the demand on each peer is independent of the number of peers. Nothing is centralized, so the system can expand indefinitely without any resources other than the peer themselves.

* The distributed nature of **Domain Name System** (**DNS**) allows it to work efficiently, serving billions of hosts on the worldwide Internet.
