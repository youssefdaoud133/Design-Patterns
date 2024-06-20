# Facade Design Pattern

<p align="center">
  <img src="../photos/structure.png" alt="Alt text" />
</p>

### Problem

The Facade design pattern addresses the problem of complex subsystems and intricate interactions within a software system. It aims to provide a simplified interface to these subsystems, making them easier to use and understand.

### Solution

The Facade design pattern proposes creating a single class, called the Facade, that provides a simplified interface to a complex subsystem. The Facade delegates client requests to the appropriate objects within the subsystem, managing their interactions and simplifying the client’s view of the subsystem.

### When to Use

Use the Facade design pattern when:

- You want to provide a simple interface to a complex subsystem.
- There are many dependencies between clients and the implementation classes of an abstraction.
- You want to layer your subsystems to make them easier to understand and use.
- You need to decouple a subsystem from clients and other subsystems, making the subsystem more manageable and scalable.

### Example Code

```java
// Complex Subsystem
class CPU {
    public void start() {
        System.out.println("CPU started");
    }
    public void execute() {
        System.out.println("CPU executing");
    }
    public void shutdown() {
        System.out.println("CPU shut down");
    }
}

class Memory {
    public void load(long position, byte[] data) {
        System.out.println("Memory loaded from position " + position);
    }
}

class HardDrive {
    public byte[] read(long lba, int size) {
        System.out.println("HardDrive read " + size + " bytes from LBA " + lba);
        return new byte[size];
    }
}

// Facade
class ComputerFacade {
    private final CPU cpu;
    private final Memory memory;
    private final HardDrive hardDrive;

    public ComputerFacade() {
        this.cpu = new CPU();
        this.memory = new Memory();
        this.hardDrive = new HardDrive();
    }

    public void start() {
        cpu.start();
        memory.load(0, hardDrive.read(0, 1024));
        cpu.execute();
    }

    public void shutdown() {
        cpu.shutdown();
    }
}

// Client Code
public class Main {
    public static void main(String[] args) {
        ComputerFacade computer = new ComputerFacade();
        computer.start();
        computer.shutdown();
    }
}
```

### Cons

- **Limited Flexibility**: By hiding the underlying subsystem, the Facade may limit the client’s ability to utilize the full capabilities of the subsystem.
- **Performance Overhead**: The Facade may introduce additional layers of abstraction, potentially causing a slight performance overhead.
- **Complexity**: While the Facade simplifies the interface to the subsystem, it can add to the overall complexity of the system if not designed carefully.
- **Maintenance**: Changes in the underlying subsystem might require changes in the Facade, adding to maintenance efforts.