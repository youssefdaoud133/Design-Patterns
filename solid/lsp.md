# Liskov Substitution Principle (LSP)

<p align="center">
  <img src="../photos/Liskov Substitution Principle.png" alt="Alt text" />
</p>



The Liskov Substitution Principle (LSP) is a fundamental principle in object-oriented programming that states that objects of a superclass should be replaceable with objects of its subclass without affecting the correctness of the program. This principle promotes polymorphism, code reuse, and maintainability by ensuring that derived classes can be used interchangeably with their base classes.

## Problem

In software development, derived classes often inherit behavior and properties from their base classes. However, violating the Liskov Substitution Principle can lead to several issues, including:

- **Incorrect behavior**: Subclasses may introduce behavior that violates the contracts established by their base classes, leading to incorrect program behavior.
- **Unexpected side effects**: Subclasses may override methods or properties in a way that causes unexpected side effects or violates the expected behavior of the base class.
- **Violation of invariants**: Subclasses may weaken or violate the invariants established by their base classes, leading to unexpected program behavior or runtime errors.

## Solution

The Liskov Substitution Principle addresses these issues by defining a contract that derived classes must adhere to when substituting base classes. Derived classes should extend the behavior of their base classes without changing the expected behavior or invariants established by the base class. This promotes code reliability, maintainability, and robustness by ensuring that derived classes can be used interchangeably with their base classes.

## Implementation

### Example

Consider a scenario where we have a `Rectangle` class with `width` and `height` properties and a `getArea()` method:

```java
class Rectangle {
    private int width;
    private int height;

    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }

    public int getWidth() {
        return width;
    }

    public void setWidth(int width) {
        this.width = width;
    }

    public int getHeight() {
        return height;
    }

    public void setHeight(int height) {
        this.height = height;
    }

    public int getArea() {
        return width * height;
    }
}
// Now, suppose we create a Square class that extends Rectangle, where the setWidth() and setHeight() methods set both the width and height to the same value:

class Square extends Rectangle {
    public Square(int size) {
        super(size, size);
    }

    @Override
    public void setWidth(int width) {
        super.setWidth(width);
        super.setHeight(width);
    }

    @Override
    public void setHeight(int height) {
        super.setWidth(height);
        super.setHeight(height);
    }
}

//Violation of LSP
// The Square class violates the Liskov Substitution Principle because it changes the behavior of the setWidth() and setHeight() methods, which behave differently from their counterparts in the Rectangle class. For example:

Rectangle rectangle = new Square(3);
rectangle.setWidth(5);
rectangle.setHeight(4);

// The area of the rectangle is unexpectedly 12 instead of 20
System.out.println("Area: " + rectangle.getArea());

```
## Benefits
**Code reliability**: Adhering to the Liskov Substitution Principle ensures that derived classes can be used interchangeably with their base classes without affecting program correctness.


**Code reuse**: Derived classes can inherit behavior and properties from their base classes, promoting code reuse and modularity.

**Maintainability**: Derived classes can be easily added or modified without affecting the existing codebase, making the codebase easier to maintain and extend.
## Considerations

Design consistency: Consistent application of the Liskov Substitution Principle across the codebase ensures predictable behavior and promotes code reliability.

Code reviews and testing: Regular code reviews and thorough testing are essential to identify violations of the Liskov Substitution Principle and ensure program correctness.