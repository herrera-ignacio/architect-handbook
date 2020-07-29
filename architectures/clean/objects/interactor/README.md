# Interactor

> You can turn an Use Case into an object, an Interactor.

Interactors have __Application specific business rules__, the use cases of applications, for example, the process of creating an order.

## Implementation

![example](https://cleancodejava.com/wp-content/uploads/2016/07/boundaryinteractorentitydelivery_mechanism.png)

Usually, Interactors will communicate with several Entities objects.

For example, a `CreateOrderInteractor` will probably talk to an `OrderEntity`, a `CustomerEntity`, etc.
