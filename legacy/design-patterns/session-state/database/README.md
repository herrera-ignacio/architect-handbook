# Database Session State

> Stores session data as comitted data in the database.

* Overview
* How It Works
* When to Use It

## Overview

When a call goes out from the client to the server, the server object first pulls the data required for the request from the database. **In order to pull information** from the database, **the server object will need some information about the session**, which requires at least a session ID number to be stored on the client.

The data involved is typically a **mix of session data that's only local to the current interaction and committed data that's relevant to all interactions**.

## How It Works

* Session data is usually considered local to the session and shouldn't affect other parts of the system until the session as a whole is comitted.
  * Adding a field to each database row that may have session data is one route (`isPending`).
  * Store a session ID as a pending field, makes it much easier to find all the data for a particular session.
  * Separate set of pending tables.

* You'll need a mechanism to clean out the session data if a session is canceled or abandoned.
  * Using a session ID you can find all data with it and delete it.
  * If a user abandon the session without telling you, you'll need some kind of timeout mechanism (e.g., a daemon that runs every few minutes).

## When To Use It

* You'll gain by using stateless objects on the server, thus **enabling pooling and easy clustering**. This is usually more straightforward than with *Server Session State*.

* You'll pay with the time needed to pull the data in and out of the database with each request. You can reduce this cost by caching the server object.

* Programming effort, especially around **handling session state**, is considerable.
