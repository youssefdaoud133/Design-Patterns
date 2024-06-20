# Flyweight Design Pattern

<p align="center">
  <img src="../photos/flyweight.png" alt="Alt text" />
</p>

### Problem

The Flyweight design pattern addresses the problem of high memory usage in applications where a large number of similar objects are created. This pattern is useful when many objects share common data, leading to inefficient memory utilization.

### Solution

The Flyweight design pattern proposes sharing common parts of objects to reduce memory usage. This involves creating a Flyweight object to store shared data and using it across multiple objects. The pattern involves:

- **Flyweight**: An interface or abstract class that defines methods for intrinsic state (shared data).
- **ConcreteFlyweight**: A class that implements the Flyweight interface and stores intrinsic state.
- **FlyweightFactory**: A class that manages Flyweight objects and ensures that they are shared properly.
- **Client**: A class that uses Flyweight objects and provides extrinsic state (context-specific data).

### When to Use

Use the Flyweight design pattern when:

- An application uses a large number of objects.
- Most object states can be made extrinsic.
- Objects can be shared to reduce memory usage.
- The identity of objects does not matter.

### Example Code

```java
import java.util.HashMap;
import java.util.Map;

// Flyweight
interface CharacterInterface {
    void display(int fontSize, String color);
}

// ConcreteFlyweight
class ConcreteCharacter implements CharacterInterface {
    private final char symbol;

    public ConcreteCharacter(char symbol) {
        this.symbol = symbol;
    }

    @Override
    public void display(int fontSize, String color) {
        System.out.println("Character: " + symbol + ", FontSize: " + fontSize + ", Color: " + color);
    }
}

// FlyweightFactory
class CharacterFactory {
    private final Map<Character, ConcreteCharacter> characterMap = new HashMap<>();

    public CharacterInterface getCharacter(char symbol) {
        ConcreteCharacter character = characterMap.get(symbol);
        if (character == null) {
            character = new ConcreteCharacter(symbol);
            characterMap.put(symbol, character);
        }
        return character;
    }
}

// Client
class TextEditor {
    private final CharacterFactory characterFactory;
    private final Map<Integer, CharacterWithStyle> text;

    public TextEditor(CharacterFactory characterFactory) {
        this.characterFactory = characterFactory;
        this.text = new HashMap<>();
    }

    public void addCharacter(int position, char symbol, int fontSize, String color) {
        CharacterInterface character = characterFactory.getCharacter(symbol);
        text.put(position, new CharacterWithStyle(character, fontSize, color));
    }

    public void display() {
        for (Map.Entry<Integer, CharacterWithStyle> entry : text.entrySet()) {
            System.out.print("Position: " + entry.getKey() + " -> ");
            entry.getValue().display();
        }
    }

    private static class CharacterWithStyle {
        private final CharacterInterface character;
        private final int fontSize;
        private final String color;

        public CharacterWithStyle(CharacterInterface character, int fontSize, String color) {
            this.character = character;
            this.fontSize = fontSize;
            this.color = color;
        }

        public void display() {
            character.display(fontSize, color);
        }
    }
}

// Main
public class Main {
    public static void main(String[] args) {
        CharacterFactory factory = new CharacterFactory();
        TextEditor editor = new TextEditor(factory);

        editor.addCharacter(0, 'H', 12, "Black");
        editor.addCharacter(1, 'e', 12, "Black");
        editor.addCharacter(2, 'l', 12, "Black");
        editor.addCharacter(3, 'l', 12, "Black");
        editor.addCharacter(4, 'o', 12, "Black");
        editor.addCharacter(5, ' ', 12, "Black");
        editor.addCharacter(6, 'W', 12, "Black");
        editor.addCharacter(7, 'o', 12, "Black");
        editor.addCharacter(8, 'r', 12, "Black");
        editor.addCharacter(9, 'l', 12, "Black");
        editor.addCharacter(10, 'd', 12, "Black");

        editor.display();
    }
}

```

### Cons

- **Complexity**: The Flyweight pattern can introduce complexity in managing shared states and ensuring thread safety.
- **Inflexibility**: It might be challenging to make changes to the shared part of the objects as they are widely used.
- **Overhead**: There is additional complexity in managing the factory and ensuring that objects are correctly shared and reused.
- **Context Handling**: The client must manage the extrinsic state, which can complicate the code and lead to potential errors if not handled correctly.