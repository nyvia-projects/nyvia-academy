# Design Patterns - TypeScript

Solutions that approach to address recurring problems in software.

_"Elements of Reusable Object-Oriented Software"_ by GoF (Gang of Four)

---

### Let's recap some concepts

**Coupling** - dependency between classes

**Interface** - Contract specifying capabilities that a class should provide (construct)

- interfaces solve coupling (but not only)

**Abstraction** - Unnecessary details of classes should be hidden

- access modifier(private) provide abstraction

- abstract classes provide polymorphism (construct)

**Abstract classes** should be used when common code needs to be provided for child classes

**Interfaces** should be used when above mentioned is wrong and requirements is simply abstraction

## Categories

23 design patters in 3 categories

- **Creational** -- how objects are created
- **Structural** -- how objects relate
- **Behavioral** -- how objects interact

## Creational Patterns

### Singleton

Type of object that can be instantiated once = single existing instance

```
class Computer {
  readonly cpu?: string;
  readonly ram?: string;
  readonly storage?: string;
  readonly gpu?: string;

  constructor(builder: Computer.Builder) {
    this.cpu = builder.cpu;
    this.ram = builder.ram;
    this.storage = builder.storage;
    this.gpu = builder.gpu;
  }
  printSpecs(): void {
    let specs = `CPU: ${this.cpu}\nRAM: ${this.ram}\nStorage: ${this.storage}\nGPU: ${this.gpu}`;
    console.log(specs);
  }
}

namespace Computer {
  export class Builder {
    cpu?: string;
    ram?: string;
    storage?: string;
    gpu?: string;

    setCpu(cpu: string): this {
      this.cpu = cpu;
      return this;
    }

    setRam(ram: string): this {
      this.ram = ram;
      return this;
    }

    setStorage(storage: string): this {
      this.storage = storage;
      return this;
    }

    setGPU(gpu: string): this {
      this.gpu = gpu;
      return this;
    }

    build(): Computer {
      // Here, we can add validations if needed.
      if (!this.cpu || !this.ram) {
        throw new Error("CPU and RAM are required!");
      }
      return new Computer(this);
    }
  }
}
```

```
const computer = new Computer.Builder()
  .setCpu("Intel i7")
  .setRam("16GB")
  .setStorage("2TB SSD")
  .setGPU("NVIDIA RTX 3080")
  .build();

computer.printSpecs();
```

### Prototype

Cloning

Alternative way to implement inheritance, where you inherit from a created object

```
const button = {
  click() {
    return "clicked!";
  },
};

const redButton = Object.create(button, { color: { value: "red" } });

console.log(`${redButton.color} button: ${redButton.click()}`);

console.log(Object.getPrototypeOf(redButton));
```

### Factory

Provides interface for creating objects in a super class but allows subclasses to alter the type.

<!-- \*memento pattern
used to add 'undo' mechanisms
Originator - Memento - Caretaker = classes

\*state pattern (Open/Closed principle in sOlid)
allows an object to behave differently when the state changes
Context - State - ConcreteStates
 -->
