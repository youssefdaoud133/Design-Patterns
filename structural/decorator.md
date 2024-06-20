# Decorator Design Pattern

<p align="center">
  <img src="../photos/decorator-comic-1.png" alt="Alt text" />
</p>

### Problem

The Decorator design pattern addresses the problem of adding functionality to objects dynamically without affecting the behavior of other objects from the same class. This pattern is particularly useful when subclassing is impractical due to a large number of independent extensions.

### Solution

The Decorator pattern involves a set of decorator classes that are used to wrap concrete components. Decorators mirror the type of the components they decorate. Each decorator implements the same interface or abstract class as the component it wraps, adding its own behavior before or after delegating to the wrapped component.

### When to Use

Use the Decorator design pattern when:

- You need to add responsibilities to individual objects dynamically and transparently without affecting other objects.
- You need to extend functionality by composing behaviors rather than using inheritance.
- You want to add responsibilities to an object that you might want to change in the future.

### Example Code

```java
// Component Interface
interface Coffee {
    String getDescription();
    double getCost();
}

// Concrete Component
class SimpleCoffee implements Coffee {
    @Override
    public String getDescription() {
        return "Simple coffee";
    }

    @Override
    public double getCost() {
        return 2.0;
    }
}

// Decorator Base Class
abstract class CoffeeDecorator implements Coffee {
    protected final Coffee decoratedCoffee;

    public CoffeeDecorator(Coffee coffee) {
        this.decoratedCoffee = coffee;
    }

    @Override
    public String getDescription() {
        return decoratedCoffee.getDescription();
    }

    @Override
    public double getCost() {
        return decoratedCoffee.getCost();
    }
}

// Concrete Decorators
class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee coffee) {
        super(coffee);
    }

    @Override
    public String getDescription() {
        return decoratedCoffee.getDescription() + ", Milk";
    }

    @Override
    public double getCost() {
        return decoratedCoffee.getCost() + 0.5;
    }
}

class SugarDecorator extends CoffeeDecorator {
    public SugarDecorator(Coffee coffee) {
        super(coffee);
    }

    @Override
    public String getDescription() {
        return decoratedCoffee.getDescription() + ", Sugar";
    }

    @Override
    public double getCost() {
        return decoratedCoffee.getCost() + 0.2;
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        Coffee coffee = new SimpleCoffee();
        System.out.println(coffee.getDescription() + " $" + coffee.getCost());

        coffee = new MilkDecorator(coffee);
        System.out.println(coffee.getDescription() + " $" + coffee.getCost());

        coffee = new SugarDecorator(coffee);
        System.out.println(coffee.getDescription() + " $" + coffee.getCost());
    }
}
```

### Cons

- **Complexity**: The use of multiple small classes can lead to increased complexity and make the system harder to understand and maintain.
- **Performance**: The pattern may introduce performance overhead due to the addition of many layers of decoration, especially if there are many decorators.
- **Debugging**: The stack of decorators can make debugging more difficult, as the flow of control involves multiple levels of delegation.
- **Memory Usage**: Every layer of decoration adds a new object, which may increase memory usage.

### Summary

The Decorator pattern provides a flexible alternative to subclassing for extending functionality. It allows responsibilities to be added to an object dynamically, and decorators can be composed together in various combinations. However, this flexibility comes at the cost of added complexity and potential performance overhead.