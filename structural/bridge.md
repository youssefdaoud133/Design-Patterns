# Bridge Design Pattern

<p align="center">
  <img src="../photos/bridge_pattern_uml_diagram.jpg" alt="Alt text" />
</p>

The Bridge pattern is a structural design pattern that separates the abstraction from its implementation, allowing them to vary independently. It decouples the abstraction and implementation by providing an interface (abstraction) for clients to interact with, while allowing multiple implementations (implementor) to be used interchangeably. This promotes flexibility, maintainability, and extensibility by enabling changes in either the abstraction or implementation without affecting each other.

## Problem

In software development, there are scenarios where a class or component has multiple variants or implementations, and clients need to interact with them without being tightly coupled to specific implementations. However, directly coupling the abstraction to its implementations may lead to several issues, including:

- Tight coupling: Abstraction and implementation are tightly coupled, making it difficult to change or extend them independently.
- Limited extensibility: Adding new variants or implementations requires modifying existing code, violating the principle of open/closed principle.
- Poor maintainability: Changes to one variant may require modifications to other variants, leading to maintenance issues and code duplication.

## Solution

The Bridge pattern addresses these issues by decoupling the abstraction from its implementations. It defines separate hierarchies for the abstraction and implementation, allowing them to vary independently. Abstraction delegates implementation-specific tasks to the implementor, promoting loose coupling and enhancing flexibility, maintainability, and extensibility.

## Implementation

### Structure

The Bridge pattern typically consists of the following components:

- **Abstraction**: Defines the interface for the abstraction and maintains a reference to an implementor object.
- **Refined Abstraction**: Extends the abstraction interface and provides additional functionality or variations.
- **Implementor**: Defines the interface for the implementor and provides concrete implementations.
- **Concrete Implementor**: Implements the implementor interface and provides specific implementations for the abstraction.

### Example

Consider a scenario where we need to implement a drawing application that supports multiple rendering engines (e.g., OpenGL, DirectX) using the Bridge pattern:

```java
// Implementor
interface Renderer {
    void renderCircle(int radius);
}

// Concrete Implementor
class OpenGLRenderer implements Renderer {
    @Override
    public void renderCircle(int radius) {
        System.out.println("Rendering circle using OpenGL with radius " + radius);
    }
}

class DirectXRenderer implements Renderer {
    @Override
    public void renderCircle(int radius) {
        System.out.println("Rendering circle using DirectX with radius " + radius);
    }
}

// Abstraction
abstract class Shape {
    protected Renderer renderer;

    public Shape(Renderer renderer) {
        this.renderer = renderer;
    }

    abstract void draw();
}

// Refined Abstraction
class Circle extends Shape {
    private final int radius;

    public Circle(int radius, Renderer renderer) {
        super(renderer);
        this.radius = radius;
    }

    @Override
    void draw() {
        renderer.renderCircle(radius);
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        Renderer openglRenderer = new OpenGLRenderer();
        Renderer directXRenderer = new DirectXRenderer();

        Shape circle1 = new Circle(5, openglRenderer);
        circle1.draw(); // Output: Rendering circle using OpenGL with radius 5

        Shape circle2 = new Circle(8, directXRenderer);
        circle2.draw(); // Output: Rendering circle using DirectX with radius 8
    }
}

```
## Benefits
Promotes loose coupling between abstraction and implementation, making the code easier to maintain and extend.

Enables changes in either the abstraction or implementation without affecting each other, enhancing flexibility and maintainability.

Facilitates the creation of complex hierarchies and variations by separating the concerns of abstraction and implementation.

## Considerations
Care should be taken to properly design the abstraction and implementor interfaces to ensure compatibility and flexibility.

Bridge pattern may introduce additional complexity, so it should be used judiciously based on the specific requirements and design constraints.