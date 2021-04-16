# Ports & Adapter / Hexagonal Architecture

The Hexagonal Architecture aims at creating loosely coupled application components that can be easily connected to their software environment by means of ports and adapters. This makes components exchangeable at any level and facilitates test automation.

![architecture](https://upload.wikimedia.org/wikipedia/commons/thumb/7/75/Hexagonal_Architecture.svg/313px-Hexagonal_Architecture.svg.png)

## Origin

Invented by _Alistair Cockburn_ in an attempt to avoid known structural pitfalls in object-oriented software design, such as undesired dependencies between layers and contamination of user interface code with business logic.

## Principle

Divides a system into several loosely-coupled interchangeable components, such as the application core, database, user interface, test scripts, and interfaces with other systems. This approach is an alternative to the traiditional layered architecture.

Each component is connected to the others through a number of exposed "__ports__". Communication between these ports follow a given protocol depending on their purpose. Ports and protocols define an abstract API that can be implemented by any suitable technical means.

Adapters are the glue between components and the outside world. They tailor the exchanges between the external world and the ports that represent the requirements of the inside of the application component. There can be several adapters for one port.
