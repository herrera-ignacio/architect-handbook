# Own their own data

Ideally, microservices *should not* share databases. If one service wants to access data held by another service, then it should go and ask that service for the data it needs.

This allows the service to map from internal implementation details to a more stable public *contract*, ensuring stable service interfaces. Having stable interfaces between services is essential if we want *independent deployability*.

