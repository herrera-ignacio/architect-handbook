# Architecture

* Definition
* Software Architect
* Impact
  * Development
  * Deployment
  * Use cases & Operation
  * Maintenance

## Definition

> The primary purpose of architecture is to support the life cycle of the system. The ultimate goal is to minimize the lifetime cost of the system and to maximize programmer productivity.

The architecture of a software system is the *shape* given to that system by those who build it. The form of that shape is in the division into components, the arrangement of those components, and the ways of which those components communicate with each other.

The purpose of that shape is to facilitate the development, deployment, operation, and maintenance of the software system contained within it.

> The strategy behind that facilitation is to **leave as many options open as possible for as long as possible**.

A good architecture makes the system easy to understand, easy to develop, easy to maintain, and easy to deploy.

## Software Architect

First of all, a software architect is a programmer, and continues to be a programmer. Never fall for the lie that suggests that software architects pull back from code to focus on higher-level issues.

Software architects are the best programmers, and they continue to take programming tasks, while they also guide the rest of the team toward a design that maximizes productivity. They may not write as much code as other programmers do, but they continue to engage in programming tasks, because otherwise they cannot do their jobs properly if they are not experiencing the problems that they are creating for the rest of the programmers.

## Impact

### Development

A software system that is hard to develop is not likely to have a long healthy lifetime.

So the architecture of a system should make that system easy to develop, for the team(s) who develop it. Different team structures imply different architectural decisions.

> **Conway's law**: Any organization that designs a system will produce a design whose structure is a copy of the organization's communication structure.

When components are **strongly decoupled**, the interference between teams is mitigated. If the business rules don't know about the UI, then a team that focuses on the UI cannot much affect a team that focuses on the business rules.

> As long as the layers and use cases are decoupled, the architecture of the system will support the organization of the teams, irrespective of whether they are organized as feature teams, component teams, layer teams, or some other variation.

### Deployment

The higher the cost of deployment, the less useful the system is.

A goal of a software architecture should be to make a system that can be easily and *immediately* deployed *with a single action* after build.

> Decoupling of use cases and layers affords a high degree of flexibility in deployment. There should be possible to hot-swap layers and use cases in running systems.

### Use Cases & Operation

The impact of architecture on system operation tends to be less dramatic than other areas. Almost any operational difficulty can be resolved by throwing more hardware at the system without drastically impacting the software architecture.

> The fact that hardware is cheap and people are expensive means that architectures that impide operation are not as costly as architectures that impede development, deployment, and maintenance.

A good software architecture **communicates the operational needs of the system**. It makes the operation of the system readily apparent to the developers.

> The architecture of the system should elevate the use cases, the features, and the required behaviors of the system to first-class entities that are visible landmarks for the developers. A good architecture clarify and expose the behavior so that the intent of the system is visible at the architectural level.

### Maintenance

> Of all aspects of a software system, maintenance is the most costly.

The primary cost of maintenance is in *spelunking* and risk. Spelunking is the cost of digging through the existing software, trying to determine the best place and the best strategy to add a new feature or to repair a defect. While making such changes, the likelihood of creating inadvertent defects is always there, adding to the cost of risk.

A carefully thought-through architecture vastly mitigates these costs. By separating the system into components, and isolating those components through stable interfaces, it is possible to illuminate the pathways for future features and greatly reduce the rsik of inadvertent breakage.
