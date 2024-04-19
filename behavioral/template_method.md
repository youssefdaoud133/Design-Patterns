# Template Method Design Pattern

The Template Method pattern is a behavioral design pattern that defines the skeleton of an algorithm in the superclass but allows subclasses to override specific steps of the algorithm without changing its structure. It enables code reuse, promotes consistency, and provides a way to define the invariant parts of an algorithm while allowing customization of the variable parts by subclasses.

## Problem

In software development, there are scenarios where multiple algorithms share common steps but have variations in certain steps. However, directly implementing these algorithms in subclasses can lead to several issues:

- Code duplication: Common steps of the algorithm are duplicated across multiple subclasses, leading to maintenance issues and inconsistencies.
- Inflexibility: Subclasses are tightly coupled to the structure of the algorithm, making it difficult to change or extend the algorithm without modifying the subclasses.
- Lack of consistency: Variations in the implementation of common steps may lead to inconsistent behavior across subclasses.

## Solution

The Template Method pattern addresses these issues by defining the skeleton of an algorithm in the superclass and allowing subclasses to override specific steps of the algorithm as needed. It provides a way to encapsulate the invariant parts of an algorithm in the superclass while allowing customization of the variable parts by subclasses. This promotes code reuse, consistency, and flexibility in algorithm implementation.

## Implementation

### Structure

The Template Method pattern typically consists of the following components:

- **Abstract Class**: Defines the template method that defines the algorithm's skeleton and contains one or more abstract methods that subclasses must implement.
- **Concrete Class**: Implements the abstract methods defined in the abstract class to provide concrete implementations of specific steps of the algorithm.

### Example

Consider a scenario where we need to implement a simple algorithm for making tea and coffee using the Template Method pattern:

```java
// Abstract Class
abstract class Beverage {
    // Template method
    public final void prepareBeverage() {
        boilWater();
        brew();
        pourInCup();
        addCondiments();
    }

    // Abstract methods to be implemented by subclasses
    protected abstract void brew();
    protected abstract void addCondiments();

    // Common methods
    private void boilWater() {
        System.out.println("Boiling water");
    }

    private void pourInCup() {
        System.out.println("Pouring into cup");
    }
}

// Concrete Class
class Tea extends Beverage {
    @Override
    protected void brew() {
        System.out.println("Steeping the tea");
    }

    @Override
    protected void addCondiments() {
        System.out.println("Adding lemon");
    }
}

// Concrete Class
class Coffee extends Beverage {
    @Override
    protected void brew() {
        System.out.println("Dripping coffee through filter");
    }

    @Override
    protected void addCondiments() {
        System.out.println("Adding sugar and milk");
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        Beverage tea = new Tea();
        Beverage coffee = new Coffee();

        System.out.println("Making tea:");
        tea.prepareBeverage(); // Output: Boiling water, Steeping the tea, Pouring into cup, Adding lemon

        System.out.println("\nMaking coffee:");
        coffee.prepareBeverage(); // Output: Boiling water, Dripping coffee through filter, Pouring into cup, Adding sugar and milk
    }
}
```

## Benefits

Promotes code reuse by encapsulating common steps of an algorithm in the superclass.

Provides a way to define the invariant parts of an algorithm while allowing customization of the variable parts by subclasses.

Improves consistency and maintainability by enforcing a consistent structure across subclasses.

## Considerations

Care should be taken to identify the invariant and variable parts of the algorithm to properly design the template method and abstract methods.

Subclasses should follow the Liskov Substitution Principle to ensure that they can be used interchangeably with the superclass.
