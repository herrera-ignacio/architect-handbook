# Use Cases

> A use case is a description of the way that an automated system is used. It specifies the input to be provided, the output to be returned, and the processing steps involved in producing that output.

A use case describes **Application-specific Business Rules** as opposed to the *Critical Business Rules* within the Entities. Use Cases are *rules that would not be used in a manual environment*, because they make sense only as part of an automated system, they make or save money for the business by defining and constraining the way an *automated* system operates.

>  A set of use cases is used to describe software.

Use cases contain the rules that specify how and when the *Critical Business Rules* within the Entities would be invoked. It is an object that has one or more functions that implements the application-specific business rules, data elements that include the input data, output data, and the references to the appropriate Entities with which it interacts.

> Entities have no knowledge of the use cases that control them. This is because the *Dependency Inversion Principle*.

## Example

```
Create Order

Data:
    <Customer-id>
    <Customer-contact-info>
    <Shipment-destination>
    <Shipment-mechanism>
    <Payment-information>

Primary Course:
    1. Order clerk issues "Create Order" command with above data
    2. System validates all data
    3. System creates order and determines order-id
    4. System delivers order-id to clerk

Exception Course: Validation Error
    1. System delivers error message to clerk
```
