# Design-pattern-JavaScript

Sure! Here’s a categorized list of common design patterns in JavaScript, organized into **Creational**, **Structural**, and **Behavioral** patterns.

### 1. **Creational Patterns**
These patterns focus on object creation mechanisms, trying to create objects in a manner suitable to the situation.

- **Singleton Pattern**: Ensures a class has only one instance and provides a global point of access to it.
- **Factory Pattern**: Defines an interface for creating objects but allows subclasses to alter the type of objects that will be created.
- **Abstract Factory Pattern**: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.
- **Builder Pattern**: Separates the construction of a complex object from its representation, allowing the same construction process to create different representations.
- **Prototype Pattern**: Creates new objects by copying an existing object, known as the prototype.

### 2. **Structural Patterns**
These patterns deal with object composition, creating relationships between objects to form larger structures.

- **Module Pattern**: Encapsulates private variables and functions, exposing a public API.
- **Decorator Pattern**: Adds behavior to individual objects dynamically without affecting the behavior of other objects from the same class.
- **Facade Pattern**: Provides a simplified interface to a complex subsystem.
- **Adapter Pattern**: Allows incompatible interfaces to work together by converting the interface of a class into another interface that a client expects.
- **Bridge Pattern**: Decouples an abstraction from its implementation so that the two can vary independently.
- **Composite Pattern**: Composes objects into tree structures to represent part-whole hierarchies, allowing clients to treat individual objects and compositions uniformly.

### 3. **Behavioral Patterns**
These patterns focus on communication between objects, defining how objects interact and communicate.

- **Observer Pattern**: Allows a subject to maintain a list of observers that are notified of any changes in the subject's state.
- **Strategy Pattern**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable.
- **Command Pattern**: Encapsulates a request as an object, thereby allowing for parameterization of clients with queues, requests, and operations.
- **Iterator Pattern**: Provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.
- **Mediator Pattern**: Defines an object that encapsulates how a set of objects interact, promoting loose coupling.
- **State Pattern**: Allows an object to alter its behavior when its internal state changes, appearing to change its class.
- **Template Method Pattern**: Defines the skeleton of an algorithm in a method, deferring some steps to subclasses.
- **Chain of Responsibility Pattern**: Passes a request along a chain of handlers, allowing multiple objects to handle the request without the sender needing to know which object will handle it.

### Summary
This categorization helps to understand the purpose of each design pattern and how they can be applied in JavaScript development. If you want to explore any specific pattern in detail or see examples, just let me know!

Sure! Here’s a collection of design patterns in JavaScript categorized into **Creational**, **Structural**, and **Behavioral** patterns, complete with code examples and descriptions for each.

### 1. **Creational Patterns**

#### **1.1 Singleton Pattern**
**Description**: Ensures a class has only one instance and provides a global point of access to it.

```javascript
const Singleton = (function () {
    let instance;

    function createInstance() {
        const object = new Object("I am the instance");
        return object;
    }

    return {
        getInstance: function () {
            if (!instance) {
                instance = createInstance();
            }
            return instance;
        }
    };
})();

const instance1 = Singleton.getInstance();
const instance2 = Singleton.getInstance();
console.log(instance1 === instance2); // Outputs: true
```

#### **1.2 Factory Pattern**
**Description**: Defines an interface for creating objects but allows subclasses to alter the type of objects that will be created.

```javascript
class Animal {
    speak() {}
}

class Dog extends Animal {
    speak() {
        return "Woof!";
    }
}

class Cat extends Animal {
    speak() {
        return "Meow!";
    }
}

class AnimalFactory {
    createAnimal(type) {
        switch (type) {
            case "dog":
                return new Dog();
            case "cat":
                return new Cat();
            default:
                return null;
        }
    }
}

const factory = new AnimalFactory();
const dog = factory.createAnimal("dog");
console.log(dog.speak()); // Outputs: Woof!
```

#### **1.3 Abstract Factory Pattern**
**Description**: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

```javascript
class Dog {
    speak() {
        return "Woof!";
    }
}

class Cat {
    speak() {
        return "Meow!";
    }
}

class DogFactory {
    createAnimal() {
        return new Dog();
    }
}

class CatFactory {
    createAnimal() {
        return new Cat();
    }
}

class AnimalFactory {
    static getFactory(type) {
        switch (type) {
            case "dog":
                return new DogFactory();
            case "cat":
                return new CatFactory();
            default:
                return null;
        }
    }
}

const factory = AnimalFactory.getFactory("dog");
const dog = factory.createAnimal();
console.log(dog.speak()); // Outputs: Woof!
```

#### **1.4 Builder Pattern**
**Description**: Separates the construction of a complex object from its representation, allowing the same construction process to create different representations.

```javascript
class Car {
    constructor() {
        this.make = '';
        this.model = '';
    }
}

class CarBuilder {
    constructor() {
        this.car = new Car();
    }

    setMake(make) {
        this.car.make = make;
        return this;
    }

    setModel(model) {
        this.car.model = model;
        return this;
    }

    build() {
        return this.car;
    }
}

const myCar = new CarBuilder().setMake('Toyota').setModel('Corolla').build();
console.log(myCar); // Outputs: Car { make: 'Toyota', model: 'Corolla' }
```

#### **1.5 Prototype Pattern**
**Description**: Creates new objects by copying an existing object, known as the prototype.

```javascript
const carPrototype = {
    init(make, model) {
        this.make = make;
        this.model = model;
    },
    getDetails() {
        return `${this.make} ${this.model}`;
    }
};

function createCar(make, model) {
    const car = Object.create(carPrototype);
    car.init(make, model);
    return car;
}

const myCar = createCar('Ford', 'Mustang');
console.log(myCar.getDetails()); // Outputs: Ford Mustang
```

### 2. **Structural Patterns**

#### **2.1 Module Pattern**
**Description**: Encapsulates private variables and functions, exposing a public API.

```javascript
const Module = (function () {
    let privateVariable = "I am private";

    function privateMethod() {
        console.log(privateVariable);
    }

    return {
        publicMethod: function () {
            privateMethod();
        }
    };
})();

Module.publicMethod(); // Outputs: I am private
```

#### **2.2 Decorator Pattern**
**Description**: Adds behavior to individual objects dynamically without affecting the behavior of other objects from the same class.

```javascript
function Coffee() {
    this.cost = function () {
        return 5;
    };
}

function MilkDecorator(coffee) {
    const originalCost = coffee.cost();
    coffee.cost = function () {
        return originalCost + 1;
    };
}

const myCoffee = new Coffee();
MilkDecorator(myCoffee);
console.log(myCoffee.cost()); // Outputs: 6
```

#### **2.3 Facade Pattern**
**Description**: Provides a simplified interface to a complex subsystem.

```javascript
class CPU {
    freeze() {
        console.log("Freezing CPU...");
    }
    jump(position) {
        console.log(`Jumping to ${position}...`);
    }
    execute() {
        console.log("Executing...");
    }
}

class Memory {
    load(position, data) {
        console.log(`Loading data at ${position}...`);
    }
}

class Computer {
    constructor() {
        this.cpu = new CPU();
        this.memory = new Memory();
    }

    start() {
        this.cpu.freeze();
        this.memory.load(0, "Boot data");
        this.cpu.jump(0);
        this.cpu.execute();
    }
}

const computer = new Computer();
computer.start();
// Outputs:
// Freezing CPU...
// Loading data at 0...
// Jumping to 0...
// Executing...
```

#### **2.4 Adapter Pattern**
**Description**: Allows incompatible interfaces to work together by converting the interface of a class into another interface that a client expects.

```javascript
class OldSystem {
    request() {
        return "Old system request";
    }
}

class NewSystem {
    specificRequest() {
        return "New system request";
    }
}

class Adapter {
    constructor(newSystem) {
        this.newSystem = newSystem;
    }

    request() {
        return this.newSystem.specificRequest();
    }
}

const oldSystem = new OldSystem();
const newSystem = new NewSystem();
const adapter = new Adapter(newSystem);

console.log(oldSystem.request()); // Outputs: Old system request
console.log(adapter.request()); // Outputs: New system request
```

#### **2.5 Composite Pattern**
**Description**: Composes objects into tree structures to represent part-whole hierarchies, allowing clients to treat individual objects and compositions uniformly.

```javascript
class Component {
    constructor(name) {
        this.name = name;
    }

    display() {
        console.log(this.name);
    }
}

class Composite extends Component {
    constructor(name) {
        super(name);
        this.children = [];
    }

    add(component) {
        this.children.push(component);
    }

    display() {
        console.log(this.name);
        this.children.forEach(child => child.display());
    }
}

const root = new Composite("Root");
const child1 = new Component("Child 1");
const child2 = new Composite("Child 2");
const grandchild = new Component("Grandchild");

child2.add(grandchild);
root.add(child1);
root.add(child2);
root.display();
// Outputs:
// Root
// Child 1
// Child 2
// Grandchild
```

### 3. **Behavioral Patterns**

#### **3.1 Observer Pattern**
**Description**: Allows a subject to maintain a list of observers that are notified of any changes in the subject's state.

```javascript
class Subject {
    constructor() {
        this.observers = [];
    }

    addObserver(observer) {
        this.observers.push(observer);
    }

    notifyObservers(data) {
        this.observers.forEach(observer => observer.update(data));
    }
}

class Observer {
    update(data) {
        console.log(`Observer notified with data: ${data}`);
    }
}

const subject = new Subject();
const observer1 = new Observer();
const observer2 = new Observer();

subject.addObserver(observer1);
subject.addObserver(observer2);
subject.notifyObservers("Hello Observers!");
// Outputs:
// Observer notified with data: Hello Observers!
// Observer notified with data: Hello Observers!
```

#### **3.2 Strategy Pattern**
**Description**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable.

```javascript
class Context {
    constructor(strategy) {
        this.strategy = strategy;
    }

    executeStrategy(a, b) {
        return this.strategy.execute(a, b);
    }
}

class AddStrategy {
    execute(a, b) {
        return a + b;
    }
}

class SubtractStrategy {
    execute(a, b) {
        return a - b;
    }
}

const context = new Context(new AddStrategy());
console.log(context.executeStrategy(5, 3)); // Outputs: 8
context.strategy = new SubtractStrategy();
console.log(context.executeStrategy(5, 3)); // Outputs: 2
```

#### **3.3 Command Pattern**
**Description**: Encapsulates a request as an object, thereby allowing for parameterization of clients with queues, requests, and operations.

```javascript
class Command {
    execute() {}
}

class Light {
    turnOn() {
        console.log("Light is on");
    }
    turnOff() {
        console.log("Light is off");
    }
}

class LightOnCommand extends Command {
    constructor(light) {
        super();
        this.light = light;
    }

    execute() {
        this.light.turnOn();
    }
}

class LightOffCommand extends Command {
    constructor(light) {
        super();
        this.light = light;
    }

    execute() {
        this.light.turnOff();
    }
}

const light = new Light();
const lightOn = new LightOnCommand(light);
const lightOff = new LightOffCommand(light);

lightOn.execute(); // Outputs: Light is on
lightOff.execute(); // Outputs: Light is off
```

#### **3.4 Iterator Pattern**
**Description**: Provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

```javascript
class Iterator {
    constructor(collection) {
        this.index = 0;
        this.collection = collection;
    }

    next() {
        return this.index < this.collection.length ?
            { value: this.collection[this.index++], done: false } :
            { done: true };
    }

    hasNext() {
        return this.index < this.collection.length;
    }
}

const collection = [1, 2, 3, 4, 5];
const iterator = new Iterator(collection);

while (iterator.hasNext()) {
    console.log(iterator.next().value); // Outputs: 1 2 3 4 5
}
```

#### **3.5 State Pattern**
**Description**: Allows an object to alter its behavior when its internal state changes, appearing to change its class.

```javascript
class Context {
    constructor() {
        this.state = null;
    }

    setState(state) {
        this.state = state;
        this.state.setContext(this);
    }

    request() {
        this.state.handle();
    }
}

class State {
    setContext(context) {
        this.context = context;
    }
}

class ConcreteStateA extends State {
    handle() {
        console.log("Handling request in State A");
        this.context.setState(new ConcreteStateB());
    }
}

class ConcreteStateB extends State {
    handle() {
        console.log("Handling request in State B");
        this.context.setState(new ConcreteStateA());
    }
}

const context = new Context();
context.setState(new ConcreteStateA());
context.request(); // Outputs: Handling request in State A
context.request(); // Outputs: Handling request in State B
```


Design patterns in JavaScript can be categorized into three main types: **Creational**, **Structural**, and **Behavioral**. Each category addresses different types of problems in software design. Here’s a breakdown of these categories along with examples of patterns within each:

### 1. **Creational Patterns**
Creational patterns deal with object creation mechanisms, trying to create objects in a manner suitable to the situation.

- **Singleton Pattern**: Ensures a class has only one instance and provides a global point of access.
  
  ```javascript
  const Singleton = (function () {
      let instance;

      function createInstance() {
          const object = new Object("I am the instance");
          return object;
      }

      return {
          getInstance: function () {
              if (!instance) {
                  instance = createInstance();
              }
              return instance;
          }
      };
  })();
  ```

- **Factory Pattern**: Defines an interface for creating objects but allows subclasses to alter the type of objects that will be created.
  
  ```javascript
  class Animal {
      speak() {}
  }

  class Dog extends Animal {
      speak() {
          return "Woof!";
      }
  }

  class Cat extends Animal {
      speak() {
          return "Meow!";
      }
  }

  class AnimalFactory {
      createAnimal(type) {
          switch (type) {
              case "dog":
                  return new Dog();
              case "cat":
                  return new Cat();
              default:
                  return null;
          }
      }
  }
  ```

- **Builder Pattern**: Separates the construction of a complex object from its representation, allowing the same construction process to create different representations.
  
  ```javascript
  class Car {
      constructor() {
          this.make = '';
          this.model = '';
      }
  }

  class CarBuilder {
      constructor() {
          this.car = new Car();
      }

      setMake(make) {
          this.car.make = make;
          return this;
      }

      setModel(model) {
          this.car.model = model;
          return this;
      }

      build() {
          return this.car;
      }
  }

  const myCar = new CarBuilder().setMake('Toyota').setModel('Corolla').build();
  ```

### 2. **Structural Patterns**
Structural patterns deal with object composition, creating relationships between objects to form larger structures.

- **Module Pattern**: Encapsulates private variables and functions, exposing a public API.
  
  ```javascript
  const Module = (function () {
      let privateVariable = "I am private";

      function privateMethod() {
          console.log(privateVariable);
      }

      return {
          publicMethod: function () {
              privateMethod();
          }
      };
  })();
  ```

- **Decorator Pattern**: Adds behavior to individual objects dynamically without affecting the behavior of other objects from the same class.
  
  ```javascript
  function Coffee() {
      this.cost = function () {
          return 5;
      };
  }

  function MilkDecorator(coffee) {
      const originalCost = coffee.cost();
      coffee.cost = function () {
          return originalCost + 1;
      };
  }

  const myCoffee = new Coffee();
  MilkDecorator(myCoffee);
  ```

- **Facade Pattern**: Provides a simplified interface to a complex subsystem.
  
  ```javascript
  class CPU {
      freeze() {
          console.log("Freezing CPU...");
      }
      jump(position) {
          console.log(`Jumping to ${position}...`);
      }
      execute() {
          console.log("Executing...");
      }
  }

  class Memory {
      load(position, data) {
          console.log(`Loading data at ${position}...`);
      }
  }

  class Computer {
      constructor() {
          this.cpu = new CPU();
          this.memory = new Memory();
      }

      start() {
          this.cpu.freeze();
          this.memory.load(0, "Boot data");
          this.cpu.jump(0);
          this.cpu.execute();
      }
  }

  const computer = new Computer();
  computer.start();
  ```

### 3. **Behavioral Patterns**
Behavioral patterns focus on communication between objects, defining how objects interact and communicate.

- **Observer Pattern**: Allows a subject to maintain a list of observers that are notified of any changes in the subject's state.
  
  ```javascript
  class Subject {
      constructor() {
          this.observers = [];
      }

      addObserver(observer) {
          this.observers.push(observer);
      }

      notifyObservers(data) {
          this.observers.forEach(observer => observer.update(data));
      }
  }

  class Observer {
      update(data) {
          console.log(`Observer notified with data: ${data}`);
      }
  }
  ```

- **Strategy Pattern**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable.
  
  ```javascript
  class Context {
      constructor(strategy) {
          this.strategy = strategy;
      }

      executeStrategy(a, b) {
          return this.strategy.execute(a, b);
      }
  }

  class AddStrategy {
      execute(a, b) {
          return a + b;
      }
  }

  class SubtractStrategy {
      execute(a, b) {
          return a - b;
      }
  }

  const context = new Context(new AddStrategy());
  console.log(context.executeStrategy(5, 3)); // Outputs: 8
  ```

- **Command Pattern**: Encapsulates a request as an object, thereby allowing for parameterization of clients with queues, requests, and operations.
  
  ```javascript
  class Command {
      execute() {}
  }

  class Light {
      turnOn() {
          console.log("Light is on");
      }
      turnOff() {
          console.log("Light is off");
      }
  }

  class LightOnCommand extends Command {
      constructor(light) {
          super();
          this.light = light;
      }

      execute() {
          this.light.turnOn();
      }
  }

  class LightOffCommand extends Command {
      constructor(light) {
          super();
          this.light = light;
      }

      execute() {
          this.light.turnOff();
      }
  }

  const light = new Light();
  const lightOn = new LightOnCommand(light);
  const lightOff = new LightOffCommand(light);

  lightOn.execute(); // Outputs: Light is on
  lightOff.execute(); // Outputs: Light is off
  ```

These patterns provide a structured approach to software design, making it easier to manage complexity and enhance code reusability. If you want to explore any specific pattern further, just let me know!
