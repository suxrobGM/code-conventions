# TypeScript Best Practices

This document outlines best practices for writing code in TypeScript projects. Following these practices ensures our codebase is maintainable, efficient, and aligns with industry standards.

# Code Structure and Organization

## Modularize Code

- Organize code into modules to encapsulate functionality and promote reuse. Use ES6 module syntax (`import`/`export`) for modularization.

## Type Safety

### 1. Use TypeScript's Type System

- Take full advantage of TypeScript's static typing. Always specify types or interfaces for variables, function parameters, and return values to catch errors at compile time.

### 2. Avoid `any`

- Avoid using the `any` type unless absolutely necessary. The use of `any` bypasses the compiler's type checking, negating the benefits of TypeScript.

## Code Quality

### 1. Linting and Formatting

- Use tools like ESLint and Prettier to enforce code quality and consistent formatting. Configure these tools according to the team's agreed-upon rules.

### 2. Write Clean, Readable Code

- Write self-documenting code: choose clear and descriptive names for variables, functions, and classes.
- Keep functions and methods short and focused on a single task.

## Follow SOLID Principles

SOLID is an acronym that represents five principles of object-oriented programming and design. These principles, when combined together, make it easier for developers to develop applications that are easy to maintain and extend. They also make it easier for other developers to understand and work with the code.

### S - Single Responsibility Principle (SRP)

**Principle**: A class should have only one reason to change, meaning that a class should only have one job or responsibility.

**Example**:
```typescript
// Violation of SRP
class UserSettings {
  user: User;

  constructor(user: User) {
    this.user = user;
  }

  changeUserName(name: string) {
    this.user.name = name;
  }

  persistSettings() {
    localStorage.setItem('userSettings', JSON.stringify(this.user));
  }
}

// Adherence to SRP
class User {
  name: string;
  // other properties
}

class UserNameChanger {
  changeUserName(user: User, name: string) {
    user.name = name;
  }
}

class UserSettingsPersister {
  persistSettings(user: User) {
    localStorage.setItem('userSettings', JSON.stringify(user));
  }
}
```

### O - Open/Closed Principle (OCP)
**Principle**: Objects or entities should be open for extension but closed for modification. This means that a class should be extendable without modifying the class itself.

**Example**:
```typescript
// Open/Closed Principle
abstract class Shape {
  abstract draw(): void;
}

class Circle extends Shape {
  draw() {
    console.log('Drawing a circle');
  }
}

class Square extends Shape {
  draw() {
    console.log('Drawing a square');
  }
}

const shapes = [new Circle(), new Square()];
shapes.forEach(shape => shape.draw());
```

### L - Liskov Substitution Principle (LSP)
**Principle**: Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.

**Example**:
```typescript
class Bird {
  fly(): void {
    console.log('I can fly');
  }
}

class Duck extends Bird { }

class Ostrich extends Bird {
  fly(): void {
    throw new Error("I can't fly");
  }
}

function makeBirdFly(bird: Bird) {
  bird.fly();
}

const duck = new Duck();
const ostrich = new Ostrich();

makeBirdFly(duck); // works fine
makeBirdFly(ostrich); // will throw an error
```

In the above example, Ostrich is not substitutable for Bird because it can't fly, violating the Liskov Substitution Principle.

## I - Interface Segregation Principle (ISP)
**Principle**: A client should not be forced to depend on interfaces it does not use.

**Example**:
```typescript
// Violation of ISP
interface IWorker {
  work(): void;
  eat(): void;
}

class HumanWorker implements IWorker {
  work() {
    // ...working
  }

  eat() {
    // ...eating during break
  }
}

class RobotWorker implements IWorker {
  work() {
    // ...processing
  }

  eat() {
    // Robots don't eat, but have to implement the method
  }
}

// Adherence to ISP
interface IWorkable {
  work(): void;
}

interface IEatable {
  eat(): void;
}

class HumanWorker implements IWorkable, IEatable {
  work() {
    // ...working
  }

  eat() {
    // ...eating during break
  }
}

class RobotWorker implements IWorkable {
  work() {
    // ...processing
  }
}
```

### D - Dependency Inversion Principle (DIP)
**Principle**: High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions.

**Example**:
```typescript
// Violation of DIP
class LightBulb {
  turnOn() {
    // ...turn on the light
  }

  turnOff() {
    // ...turn off the light
  }
}

class Switch {
  private bulb: LightBulb;

  constructor(bulb: LightBulb) {
    this.bulb = bulb;
  }

  operate() {
    this.bulb.turnOn();
    // ...other operations
    this.bulb.turnOff();
  }
}

// Adherence to DIP
interface ISwitchableDevice {
  turnOn(): void;
  turnOff(): void;
}

class LightBulb implements ISwitchableDevice {
  turnOn() {
    // ...turn on the light
  }

  turnOff() {
    // ...turn off the light
  }
}

class Switch {
  private device: ISwitchableDevice;

  constructor(device: ISwitchableDevice) {
    this.device = device;
  }

  operate() {
    this.device.turnOn();
    // ...other operations
    this.device.turnOff();
  }
}
```


## Asynchronous Programming and Performance Optimization

### 1. Use Promises for I/O Operations

- Leverage promises to handle asynchronous I/O operations. This approach provides a cleaner and more manageable way to deal with asynchronous code compared to traditional callbacks.

Example:
```typescript
// Reading a file asynchronously with Promises
import {promises as fsPromises} from 'fs';

function readFileAsync(path: string): Promise<string> {
  return fsPromises.readFile(path, { encoding: 'utf8' });
}

readFileAsync('example.txt')
  .then((content) => console.log(content))
  .catch((error) => console.error('Error reading file:', error));
```

### 2. Use Workers for CPU-Intensive Operations
- Offload CPU-intensive tasks to background threads using Web Workers in the browser or Worker Threads in Node.js. This prevents blocking the main thread and keeps the application responsive.

Browser Worker Example:
```typescript
// main.ts - Main thread
const worker = new Worker('worker.js');

worker.postMessage('Start processing');

worker.onmessage = (event) => {
  console.log('Received from worker:', event.data);
};

// worker.js - Web Worker
onmessage = (event) => {
  console.log('Message from main thread:', event.data);
  const result = performHeavyComputation(); // Replace with actual computation
  postMessage(result);
};
```

Node Worker Example:
```typescript
// main.ts - Main thread
import {Worker} from 'worker_threads';

const worker = new Worker('./worker.js');
worker.postMessage('Start processing');

worker.on('message', (message) => {
  console.log('Received from worker:', message);
});

// worker.js - Worker thread
import {parentPort} from 'worker_threads';

parentPort.on('message', (message) => {
  console.log('Message from main thread:', message);
  const result = performHeavyComputation(); // Replace with actual computation
  parentPort.postMessage(result);
});
```

## Testing

### 1. Write Tests

- Write unit tests for your code to ensure functionality and prevent regressions.
- Aim for high test coverage but focus on testing the critical paths of the application.

