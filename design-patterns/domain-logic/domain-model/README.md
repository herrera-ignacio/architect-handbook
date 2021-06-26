# Domain Model

> *"An object model of the domain that incorporates both behavior and data."* - Martin Fowler

* Overview
* How It Works
* When to Use It
* Case Study: The Revenue Recognition Problem

## Overview

![](2021-06-25-21-55-26.png)

A *Domain Model* creates a web of interconnected objects, where each object represents some meaningful individual, whether as large as a corporation or as small as single line or an order form.

## How It Works

Putting a *Domain Model* in an application involves inserting a whole layer of objects that model the business area you're working in.

A simple *Domain Model* looks very much like the database design with mostly one domain object for each database table, so it can use *Active Record*.

A rich *Domain Model* can look different from the database design, with inheritance, strategies, and other Gang o Four patterns, and complex webs of small interconnected objects. This is better for more complex logic, but is harder to map to the database, so you should consider *Data Mapper*. This will help keep your *Domain Model* **indepenent from the database** and is the best approach to handle cases where the *Domain Model* and database schema diverge.

Since the behavior of the business is subject to a lot of change, it's important to be able to modify, build, and test this layer easily.

A common concern with domain logic is **bloated domain objects**. This concern leads people to consider whether some responsibility is general, in which case it should sit in a general purpose class, or specific, in which case it should sit in some usage-specific class, which might be a *Transaction Script* or perhaps the presentation itself

> As you build a screen to manipulate orders, you'll notice that some of the order behavior is only needed for it. If you put these responsibilities on the order, the risk is that the `Order` class will become too big because it's full of responsibilities that are only used in a single use case.

The problem **separating usage-specific behavior** is that it can lead to duplication. Duplication can quickly lead to more complexity and inconsistency.

> Behavior that's separated from the `Order` is harder to find, so people tend to not see it and duplicate it instead.

> *"I've found that bloating occurs much less frequently than predicted. If it does occur it's relatively easy to see and not difficult to fix. My advice is not to separate usage-specific behavior. Put it all in the object that's the natural fit. Fix the lboating when, and if, it becomes a problem."* - Martin Fowler

When you use *Domain Model* you may want to consider *Service Layer* to give your *Domain Model* a more distinct API.

## When to Use It

It all comes down to the complexity of the behavior in your system.

If you have complicated and everchanging business rules involving validation, calculations, and derivations, chances are that you'll want an object model to handle them.

One factor that comes into this is how comfortable the development team is with domain object. Learnin how to design and use a *Domain Model* is a significant exercise.

## Case Study: The Revenue Recognition Problem

> [The Revenue Recognition Problem](../../../problems/revenue-recognition)

### Java example

![](2021-06-25-22-02-05.png)

Each instance of product is connected to a single instance of recognition strategy, which determines which algorithm is used to calculate revenue recognition. In our case we have two subclasses of recognition strategy for the two different cases.

The great vlaue of the strategies is that they provide well-contained plug points to extend the application. Adding a new revenue recognition algorithm involves creating a new subclass and overriding the `calculateRevenueRecognitions` method. When you create products, you hook them up with the appropriate staretgy object.

> The following example will show only relevant code to our case study, lot of boilerplate code can be missing.

```java
class RevenueRecognition {
  private Money amount;
  private MfDate date;

  public RevenueRecognition(Money amount, MfDate date) {
    this.amount = amount;
    this.date = date;
  }

  public Money getAmount() {
    return amount;
  }

  boolean isRecognizableBy(MfDate asOf) {
    return asOf.after(date) || asOf.equals(date);
  }
}

class Contract {
  private Long id;
  private Product product;
  private Money revenue;
  private MfDate whenSigned;
  private List revenueRecognitions = new ArrayList();

  public Contract(Product product, Money revenue, MfDate whenSigned) {
    this.product = product;
    this.revenue = revenue;
    this.whenSigned = whenSigned;
  }

  public Money recognizedRevenue(MfDate asOf) {
    Money result = Money.dollars(0);
    Iterator it = revenueRecognitions.iterator();

    while (it.hasNext()) {
      RevenueRecognition r = (RevenueRecognition) it.next();
      if (r.isRecognizableBy(asOf))
        result = result.add(r.getAmount());
    }

    return result;
  }

  public void calculateRecognitions() {
    this.product.calculateRevenueRecognitions(this);
  }
}

class Product {
  private String name;
  private RecognitionStrategy recognitionStrategy;

  public Product(String name, RecognitionStrategy recognitionStrategy) {
    this.name = name;
    this.recognitionStrategy = recognitionStrategy;
  }

  public void calculateRevenueRecognitions(Contract contract) {
    this.recognitionStrategy.calculateRevenueRecognitions(contract);
  }

  public static Product newWordProcessor(String name) {
    return new Product(name, new CompleteRecognitionStrategy());
  }

  public static Product newSpreadsheet(String name) {
    return new Product(name, new ThreeWayRecognitionStrategy(60, 90));
  }

  public static Product newDatabase(String name) {
    return new Product(name, new ThreeWayRecognitionStrategy(30, 60));
  }
}

abstract class RecognitionStrategy {
  abstract void calculateRevenueRecognitions(Contract contract);
}

class CompleteRecognitionStrategy extends RecognitionStrategy {
  @Override
  void calculateRevenueRecognitions(Contract contract) {
    contract.addRevenueRecognition(new RevenueRecognition(contract.getRevenue(), contract.getWhenSigned()));
  }
}

class ThreeWayRecognitionStrategy {
  private int firstRecognitionOffset;
  private int secondRecognitionOffset;

  public ThreeWayRecognitionStrategy(int firstRecognitionOffset, int secondRecognitionOffset) {
    this.firstRecognitionOffset = firstRecognitionOffset;
    this.secondRecognitionOffset = secondRecognitionOffset;
  }

  void calculateRevenueRecognitions(Contract contract) {
    Money[] allocation = contract.getRevenue().allocate(3);

    contract.addRevenueRecognition(new RevenueRecognition(allocation[0], contract.getWhenSigned()));

    contract.addRevenueRecognition(new RevenueRecognition(allocation[1], contract.getWhenSigned().addDays(firstRecognitionOffset)));

    contract.addRevenueRecognition(new RevenueRecognition(allocation[2], contract.getWhenSigned().addDays(secondRecognitionOffset)));
  }
}
```

The OO habit of successive **forwarding from object to object moves the behavior to the object most qualified to handle it**, but it also resolves much of the conditional behavior.

You'll notice that there are no conditionals in this calculation. You set up the decision path when you create the products with the appropriate strategy. *Domain Models* work very well when you have similar conditionals because the similar conditionals can be factored out into the object structure itself.

This moves complexity out of the algorithms and into the relationships between objects.
