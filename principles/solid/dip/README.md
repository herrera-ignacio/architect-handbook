# Dependency Inversion Principle

- [Dependency Inversion Principle](#dependency-inversion-principle)
  - [Definition](#definition)
  - [Traditional Layers Pattern Problem](#traditional-layers-pattern-problem)
  - [Implementations](#implementations)
    - [Direct](#direct)
    - [Flexible](#flexible)
    - [Factories](#factories)
      - [Factories - Example](#factories---example)
    - [General Restrictions](#general-restrictions)

## Definition

> Most flexible systems are those in which __dependencies refer only to abstractions__, not to concretions.

In statically typed languages, this means that import/include statements should refer only to source modules containing interfaces/abstract classes.

DIP leverages [Stable Abstractions](../../architectures/clean/stable-abstractions) and [Concrete Components](../../architectures/clean/concrete-components) concepts.

In dynamically typed languages, source code dependencies should not refer to concrete modules (functions already implemented).

> It is the _volatile_ concrete elements of our system that we want to avoid depending on. Those are the modules that we are actively developing, and that are undergoing frequent change.

## Traditional Layers Pattern Problem 

In conventional application architecture, lower-level components (e.g. Utility Layer) are designed to be consumed by higher-level components (e.g. Policy Layer). In this composition, __higher-level components depend directly upon lower-level components to achieve some task__. This dependency upon lower-level components limits the reuse opportunities of the higher-level components.

![layers pattern](https://upload.wikimedia.org/wikipedia/commons/4/42/Traditional_Layers_Pattern.png)

The hoal of DIP is to avoid this highly coupled distribution with the mediation of an abstract layer, and to increase the re-usability of higher/policy layers.

## Implementations

We tend to ignore the stable background of operating system and platform facilities when it comes to DIP, because __we know we can rely on them not to change__.

### Direct

A direct implementation __packages policy classes with service abstracts classes__ in one library. In this implementation high-level components and low-level components are distributed into separate packages/libraries, where the __interfaces defining the behaviors/services required by the high-level component are owned by, and exist within the high-level component's library__.

The implementation of the high-level component's interface by the low-level component, requires that the low-level component package depend upon the high-level component for compilation, thus _inverting the conventional dependency relationship_.

![direct dip](https://upload.wikimedia.org/wikipedia/commons/9/96/Dependency_inversion.png)

In this version of DIP, re-utilization of lower layer components is difficult.

```ts
//== Layer 1 - PROGRAMMER: HIGH-LEVEL COMPONENT //==

class Programmer {
  fullName: string;
  language: string;
  computer: Computer;
  
  constructor(fullName: string, language: string, computer: Computer) {
    this.fullName = fullName;
    this.language = language;
    this.computer = computer;
  }

  startCoding() {
    this.computer.powerOn();
    console.log(`${this.fullName} is coding in ${this.language}`);
  }
}

//== Layer 1 - PROGRAMER SERVICES ==//

interface IComputer {
  powerOn(): void;
}

//== LOW LEVEL COMPONENT ==//

class Computer {
  private this._count = 0;
  constructor() {
    this.id = ++this._count;
  }
  
  powerOn() {
    console.log(`Computer #${this.id} powering...`);
  }
}

//== Orchestator ==//
const computer = new Computer();
const programmer = new Programmer('Nacho', 'JS', computer);
programmer.startCoding();
```

### Flexible

A more flexible solution extracts the abstract components into an independent set of packages/libraries.

![flexible dip](https://upload.wikimedia.org/wikipedia/commons/a/ab/DIPLayersPattern_v2.png)

The separation of each layer into its own package encourages re-utilization of any layer, providing robustness and mobility.

```js
//== Layer 1 - PROGRAMMER: HIGH-LEVEL COMPONENT //==

class Programmer {
  fullName: string;
  language: IProgrammingLanguage;
  computer: IComputer;
  
  constructor(fullName: string, language: IProgrammingLanguage, computer: IComputer) {
    this.fullName = fullName;
    this.language = language;
    this.computer = computer;
  }

  startCoding() {
    this.computer.powerOn();
    console.log(`${this.fullName} is coding in ${this.language.name}`);
    this.language.run();
  }
}

//== Layer 1 - PROGRAMER SERVICES ==//

interface IProgrammer {
  fullName: string;
  language: IProgrammingLanguage;
  computer: IComputer;
}

interface IComputer {
  powerOn(): void;
}

interface IProgrammingLanguage {
  name: string;
  run(): void;
}

//== Layer 2 - Computer: LOW LEVEL COMPONENT ==//

class Computer {
  private this._count = 0;
  constructor() {
    this.id = ++this._count;
  }
  
  powerOn() {
    console.log(`Computer #${this.id} powering...`);
  }
}

//== Layer 2 - ProgrammingLanguage: LOW LEVEL COMPONENT ==//

class ProgrammingLanguage {
  constructor(name: string): IProgrammingLanguage {
    this.name = name;
  }

  run() {
    console.log(`Running -${this.name}- code`);
  }
}

//== Orchestator ==//
const computer = new Computer();
const javascript = new ProgrammingLanguage('Javascript');
const programmer = new Programmer('Nacho', javascript, computer);
programmer.startCoding();
```

### Factories

The creation of volatile concrete objects requires special handling (_
Abstract Factories_).

![factories dip](./dip-1.png)

The curved line is an architectural boundary, it divides the system into two components, abstract and concrete.

Abstract components contain all the high-level business rules of the application.

Concrete components contain all the implementation details that those business rules manipulate.

#### Factories - Example

```ts
//== Layer 1 - PROGRAMMER: HIGH-LEVEL COMPONENT //==

class Programmer {
  fullName: string;
  computer: IComputer;;
  monitor: IMonitor;

  constructor(fullName: string, computer: IComputer, monitor: IMonitor): IProgrammer {
    this.fullName = fullName;
    this.computer = computer;
    this.monitor = monitor;
  }

  startCoding() {
    this.computer.powerOn();
    this.monitor.powerOn();
    console.log(`${this.fullName} is coding.`);
  }
}

//== Layer 1 - PROGRAMER SERVICES ==//

interface IProgrammer {
  fullName: string;
  computer: IComputer;
  monitor: IMonitor;
}

interface IComputer {
  brand: string;
  powerOn(): void;
}

interface IMonitor {
  brand: string;
  powerOn(): void;
}

interface IToolsFactory {
  buildComputer(): IComputer;
  buildMonitor(): IMonitor;
}

//== Layer 2 - Computer: LOW LEVEL COMPONENT ==//

class Computer {
  brand: string;

  private this._count = 0;

  constructor(brand: string): IComputer {
    this.id = ++this._count;
    this.brand = brand;
  }
  
  powerOn() {
    console.log(`Computer #${this.id}-${this.brand} powering...`);
  }
}

//== Layer 2 - Monitor: LOW LEVEL COMPONENT ==//

class Monitor {
  brand: string;

  private this._count = 0;

  constructor(brand: string): IMonitor {
    this.id = ++this._count;
    this.brand = brand;
  }
  
  powerOn() {
    console.log(`Monitor #${this.id}-${this.brand} powering...`);
  }
}

//== Layer 2 - ToolFactory: LOW LEVEL COMPONENT ==//

class AppleToolFactory {
  buildComputer(): IComputer {
    console.log('Building Macbook');
    return new Computer('Apple');
  }

  buildMonitor(): IMonitor {
    console.log('Building AppleTV');
    return new Monitor('Apple');
  }
}

//== Orchestator ==//
const appleFactory = new AppleToolFactory();
const programmer = new Programmer(
  'Nacho',
  appleFactory.buildComputer(),
  appleFactory.buildMonitor(),
);
programmer.startCoding();
```

### General Restrictions

The use of interfaces to accomplish DIP has design implications in object-oriented software:

* All member variables in a class must be interfaces or abstracts.
* All concrete class packages must connect only through interface or abstract class packages.
* No class should derive from a concrete class.
* No method should override an implemented method.
* All variable instantiation requires the implementation of a _Creational Pattern_ such as the _Factory Method_ or the _Factory_ pattern, or the use of a _Dependency-Injection_ framework.
