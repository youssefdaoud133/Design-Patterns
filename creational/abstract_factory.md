# Abstract Factory Pattern

<p align="center">
  <img src="../photos/abstract factorymethod.png" alt="Alt text" />
</p>

The Abstract Factory pattern is a creational design pattern that provides an interface for creating families of related or dependent objects without specifying their concrete classes. It allows clients to create objects without knowing their concrete types, promoting loose coupling and enhancing flexibility.

## Problem

In software development, there are scenarios where we need to create families of related or dependent objects. However, directly instantiating these objects in client code can lead to several issues:

- Tight coupling: Directly instantiating concrete classes in client code couples the code to those specific classes, making it difficult to switch to different implementations or extend the system.
- Lack of flexibility: Client code may need to know about the specific implementations of objects, violating the principle of abstraction and encapsulation.

## Solution

The Abstract Factory pattern addresses these issues by providing an interface for creating families of related or dependent objects. It defines a set of factory methods, each of which is responsible for creating a particular type of object. Subclasses implement these factory methods to create instances of concrete classes, thus providing different implementations of related objects.

## Implementation

### Structure

The Abstract Factory pattern typically consists of the following components:

- **Abstract Factory**: Declares a set of factory methods for creating related or dependent objects.
- **Concrete Factory**: Implements the factory methods to create instances of concrete classes.
- **Abstract Product**: Declares the interface for a type of product object.
- **Concrete Product**: Implements the interface defined by the Abstract Product.
- **Client**: Uses the interfaces declared by Abstract Factory and Abstract Product to create families of related or dependent objects.

### Example

Consider a scenario where we have a GUI toolkit that supports creating buttons and checkboxes for different operating systems (e.g., Windows and macOS) using the Abstract Factory pattern:

```java
// Abstract Product
interface Button {
    void render();
}

// Concrete Product
class WindowsButton implements Button {
    @Override
    public void render() {
        System.out.println("Rendering a Windows button");
    }
}

// Concrete Product
class MacOSButton implements Button {
    @Override
    public void render() {
        System.out.println("Rendering a macOS button");
    }
}

// Abstract Product
interface Checkbox {
    void render();
}

// Concrete Product
class WindowsCheckbox implements Checkbox {
    @Override
    public void render() {
        System.out.println("Rendering a Windows checkbox");
    }
}

// Concrete Product
class MacOSCheckbox implements Checkbox {
    @Override
    public void render() {
        System.out.println("Rendering a macOS checkbox");
    }
}

// Abstract Factory
interface GUIFactory {
    Button createButton();
    Checkbox createCheckbox();
}

// Concrete Factory for Windows
class WindowsFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new WindowsButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new WindowsCheckbox();
    }
}

// Concrete Factory for macOS
class MacOSFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new MacOSButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new MacOSCheckbox();
    }
}
```

### Usage

Client code can use the abstract factory to create families of related objects without needing to know about their concrete implementations:

```java
public class Main {
    public static void main(String[] args) {
        // Create a factory for Windows
        GUIFactory windowsFactory = new WindowsFactory();

        // Create a button and a checkbox for Windows
        Button windowsButton = windowsFactory.createButton();
        windowsButton.render(); // Output: Rendering a Windows button

        Checkbox windowsCheckbox = windowsFactory.createCheckbox();
        windowsCheckbox.render(); // Output: Rendering a Windows checkbox

        // Create a factory for macOS
        GUIFactory macOSFactory = new MacOSFactory();

        // Create a button and a checkbox for macOS
        Button macOSButton = macOSFactory.createButton();
        macOSButton.render(); // Output: Rendering a macOS button

        Checkbox macOSCheckbox = macOSFactory.createCheckbox();
        macOSCheckbox.render(); // Output: Rendering a macOS checkbox
    }
}
```

### Benefits

Encapsulates object creation logic, promoting loose coupling between client code and the created objects.

Provides a flexible way to create families of related or dependent objects, allowing subclasses to determine the type of objects to be created.

Enhances code maintainability and scalability by facilitating the addition of new products and factories without modifying existing code.

### Considerations

May lead to the proliferation of factories and products if there are many variations.

Clients may need to choose the appropriate factory, reducing flexibility.
