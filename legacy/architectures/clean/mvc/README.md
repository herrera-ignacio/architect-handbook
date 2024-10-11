# MVC Architecture Analysis

- [MVC Architecture Analysis](#mvc-architecture-analysis)
  - [Not Clean](#not-clean)
  - [Clean Architecture Proposal: Model View Presenter](#clean-architecture-proposal-model-view-presenter)

## Not Clean

![how mvc goes wrong](./wrong.jpg)

User make a requests, Controllers are responsible for processing the request, url query params, etc, and then invoke and orchestate Business Model objects. Then, controller delegates control to View, which queries resulting data from Business Model objects, and returns with a proper response to the user.

The main problem of MVC 'web architecture' is the __lack of boundaries__.

Controller-like / View-like functions end up in business objects, and easily gets closer to a big-ball-of-mud architecture without strict discipline.

> Our Model ends up knowing about our infrastructure and low-level modules, thus, depending on them.

## Clean Architecture Proposal: Model View Presenter

![clean](../mcp/mcp.gif)
