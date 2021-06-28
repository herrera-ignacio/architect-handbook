# How To Approach

> The system design interview is an open-ended conversation. You are expected to lead it.

You can use the following steps to guide the discussion. As an exercise, you can work through [system design interview questions with solutions](https://github.com/donnemartin/system-design-primer#system-design-interview-questions-with-solutions) using these steps.

1. Outline use cases, constraints, and assumptions.

2. Create a high level design.

3. Design core components.

4. Scale the design.

## 1. Outline use cases, constraints and assumptions

Gather requirements and scope the problem. Ask questions to clarify use cases and constraints. Discuss assumptions.

* Who is going to use it?
* How are they going to use it?
* How many users are there?
* What does a system do?
* What are the inputs and outputs of the system?
* How much data do we expect to handle?
* How many requests per second do we expect?
* What is the expected read to write ratio?

## 2. Create a high level design

Outline a high level design with all important components.

* Sketch the main components and connections
* Justify your ideas

## 3. Design core components

Dive into details for each core component.

For example, if you were asked to design a *url shortening service*, discuss:

* Generating and storing a hash of the full url
  * MD5 and Base62
  * Hash collisions
  * SQL or NoSQL
  * Database schema
* Translating a hashed url to the full url
  * Database lookup
* API and object-oriented design

## 4. Scale the design

Identify and address bottlenecks using *principles of scalable system design*, given the constraints.

For example, do you need the following to address scalability issues?

* Load balancer
* Horizontal scaling
* Caching
* Database sharding

Discuss potential solutions and trade-offs. Everything is a trade-off.
