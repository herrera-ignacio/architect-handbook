# Use Cases

List of actions or event steps typically defining the interactions between a role/actor and a system to achieve a goal.

An Use Case doesn't describe nothing about data structure, validation mechanisms, etc.

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
