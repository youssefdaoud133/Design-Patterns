# Memento Design Pattern

<p align="center">
  <img src="../photos/memento-en.png" alt="Alt text" />
</p>

The Memento pattern is a behavioral design pattern that allows capturing and storing the internal state of an object without exposing its internal structure. It enables restoring the object to its previous state, providing undo/redo functionality and ensuring data integrity and encapsulation.

## Problem

In software development, there are scenarios where objects need to be able to revert to a previous state or restore their internal state after a series of operations. However, directly exposing the internal state of objects or using traditional data persistence mechanisms may lead to several issues:

- Violation of encapsulation: Exposing the internal state of objects can violate the principle of encapsulation, making it difficult to maintain and evolve the code.
- Lack of flexibility: Traditional data persistence mechanisms like databases or serialization may not be suitable for capturing and restoring the state of objects in memory.
- Performance overhead: Storing and retrieving the entire state of objects can be resource-intensive, especially for large or complex objects.

## Solution

The Memento pattern addresses these issues by encapsulating the internal state of objects in a memento object and providing a way to capture, store, and restore the object's state without exposing its internal structure. It allows objects to maintain multiple states and revert to a previous state as needed, providing undo/redo functionality and ensuring data integrity and encapsulation.

## Implementation

### Structure

The Memento pattern typically consists of the following components:

- **Originator**: Creates a memento object to store its internal state and uses mementos to restore its state.
- **Memento**: Stores the internal state of the originator object and provides methods for retrieving and setting the state.
- **Caretaker**: Manages the mementos created by the originator, providing a way to store and retrieve mementos without exposing their internal structure.

### Example

Consider a scenario where we need to implement a text editor application with undo/redo functionality using the Memento pattern:

```java
import java.util.Stack;

import java.util.Stack;

// Originator
class TextEditor {
    private String text ="";
    private Stack<TextMemento> history = new Stack<>();

    public void addText(String addedText) {
        history.push(new TextMemento(text.toString()));
        text += addedText;
    }

    public void undo() {
        if (!history.isEmpty()) {
            text = history.pop().getText();
        }
    }

    public void printText() {
        System.out.println("Current text: " + text);
    }
    // Memento
    public  static  class  TextMemento {
        private String text;

        public TextMemento(String text) {
            this.text = text;
        }

        public String getText() {
            return text;
        }
    }
}

// Client
public class Main {

    public static void main(String[] args) {
        TextEditor editor = new TextEditor();

        editor.addText("Hello ");
        editor.printText(); // Output: Current text: Hello

        editor.addText("World!");
        editor.printText(); // Output: Current text: Hello World!

        editor.undo();
        editor.printText(); // Output: Current text: Hello
        editor.undo();
        editor.printText(); // Output: Current text:

    }
}
```
## Benefits
Encapsulates the internal state of objects, ensuring data integrity and encapsulation.

Provides a way to capture and restore the state of objects without exposing their internal structure.

Enables undo/redo functionality and maintains multiple states of objects.

## Considerations
Care should be taken to manage the lifecycle of memento objects to avoid memory leaks or excessive memory consumption.

Memento objects should be immutable or have limited mutability to prevent unintended modifications to their state.