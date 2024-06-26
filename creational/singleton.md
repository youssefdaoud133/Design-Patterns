# Singleton Pattern

<p align="center">
  <img src="../photos/Singleton pattern java example.jpg" alt="Alt text" />
</p>

The Singleton pattern ensures that a class has only one instance and provides a global point of access to that instance.

## Problem

In some scenarios, it's necessary to have only one instance of a class available throughout the application. However, traditional object creation methods like creating a new instance every time may lead to multiple instances of the class, causing issues such as:

- Resource wastage.
- Inconsistent behavior due to multiple instances.
- Difficulty in maintaining and managing shared resources.

## Solution

The Singleton pattern addresses these problems by providing a mechanism to ensure that a class has only one instance and providing global access to that instance.

## Implementation

### Classic Singleton Implementation

```java
public class Singleton {
    private static Singleton instance;

    // Private constructor to prevent instantiation from outside
    private Singleton() {}

    // Public static method to get the instance
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

## Thread-Safe Singleton Implementation (Double-Checked Locking)

```java
public class Singleton {
    private static volatile Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}

```

## In this implementation:

The `volatile` keyword ensures that any thread that reads the instance variable will see the most recent write. Without volatile, there is a chance that a thread may see a stale value of instance and incorrectly assume that the Singleton has been instantiated when it hasn't.

The `synchronized` block ensures that only one thread can execute the instantiation logic at a time. This prevents multiple threads from creating multiple instances of the Singleton class in a concurrent environment. The synchronization block is used only when instance is null, which optimizes performance once the Singleton is instantiated.

## Applications of Singleton Pattern

- **Logger Classes**: Ensure that all parts of the application share the same logger instance, facilitating consistent logging throughout.

- **Database Connection**: Manage resources efficiently by ensuring that only one instance of the database connection is created and shared across the application.

- **Configuration Management**: Simplify access and modification of configuration settings by having a single configuration instance throughout the application.

- **Caching**: Optimize performance by using a singleton cache manager to manage caching mechanisms, ensuring consistent caching across the application.

- **Thread Pool**: Efficiently manage and reuse threads in multi-threaded applications by creating and sharing a single instance of a thread pool.

- **GUI Components**: Manage global resources such as main windows or application settings dialogs, ensuring there is only one instance of these components throughout the application.
