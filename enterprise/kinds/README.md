# Kinds of Enterprise Applications

> It's important to realize that EAPPs are all different and that different problems lead to different ways of doing things.

## Case study 1

Consider a *B2C (business to customer) online retailer*: People browse and buy. For such a system we need to be able to handle a very high volume of users, so our solution needs to be not only reasonably efficient in terms of resources used but also scalable so that you can increase the load by adding more hardware.

The domain logic for such an application can be pretty straightforward: order capturing, some relatively simple pricing and shipping calculations, and shipment notification. We want anyone to be able to access the system easily, so that implies a pretty generic Web presentation that can be used with the widest possible range of browsers. Data source includes a database for holding orders and perhaps some communication with an inventory system to help with availability and delivery information.

## Case study 2

Contrast first case with a *system that automates the processing of leasing agreements*. In some ways this is a much simpler system than the B2C retailer's because there are many fewer users, but its business logic is more complicated.

Calculating monthly bills on a lease, handling events such as early returns and late payments, and validating data as a lease is booked are all complicated tasks, since much of the leasing industry's competition comes in the form of little variations over deals done in the past. A complex business domain such as this is challenging because the rules are so arbitrary.

Such a system also has more complexity in the UI. At the least this means a much more involved HTML interface with more, and more complex, screens. Often these systems have UI demands that lead users to want a more sophisticated presentation than a simple frontend allows, so a more conventional rich-client interface is needed.

This also leads to more complicated transaction behavior: Booking a lease may take an hour or two, during which time the user is in a logical transaction. We also see a complex database schema with perhaps two hundred tables and connections to packages for asset valuation and pricing.

## Case study 3

Consider a simple *expense-tracking system for a small company*.

Such a system has few users and simple logic and can easily be made accessible across the company with a simple HTML presentation. The only data source is a few tables in a database. As simple as it is, a system like this is not devoid of challenge.

You have to build it very quickly and you have to bear in mind that it may grow as people want to calculate reimbursement checks, feed them into the payroll system, understand tax implications, provide reports for the CFO, tie into airline reservation web services, and so on.

Trying to use the architecture for either of the other two example systems will slown down the development of this one. If a system has business benefits (as all EAPPs should), delaying those benefits costs money. However, you don't want to make decisions now that will hamper future growth. But if you add flexibility now and get it wrong, the complexity added for flexibility's sake may actually make it harder to evolve in the future and may delay deployment and thus delay the benefit.

> Although such systems may be small, most enterprise have a lot of them so the **cummulative effect** of an inappropriate architecture can be significant.

## Conclusion

Each enterprise application has different difficulties. As a result, **you can't come up with a single architecture that will be right for all three**.

Choosing an architecture means that you have to understand the particular problems of your system and choose an appropriate design based on that understanding. Many of the **patterns are about choices and alternatives**, all they can do is **give you more information to base your decisions on**.