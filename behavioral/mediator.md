# Mediator Design Pattern

The Mediator pattern is a behavioral design pattern that defines an object that encapsulates how objects interact with each other. It promotes loose coupling by keeping objects from referring to each other explicitly and allows for complex communication between objects without them having direct references to each other.

## Problem

In software development, there are scenarios where multiple objects need to communicate with each other, but direct communication between these objects can lead to several issues:

- Tight coupling: Direct references between objects make the code harder to maintain and extend, as changes to one object may require modifications to other objects.
- Lack of scalability: As the number of objects grows, managing direct connections between them becomes increasingly complex and error-prone.
- Code duplication: Logic for coordinating communication between objects may be duplicated across multiple objects, leading to maintenance issues and inconsistencies.

## Solution

The Mediator pattern addresses these issues by introducing a mediator object that encapsulates the communication logic between objects. Instead of objects communicating with each other directly, they communicate with the mediator, which coordinates their interactions. This promotes loose coupling, simplifies communication between objects, and improves scalability and maintainability.

## Implementation

### Structure

The Mediator pattern typically consists of the following components:

- **Mediator**: Defines an interface for communicating with colleague objects.
- **Concrete Mediator**: Implements the Mediator interface and coordinates communication between colleague objects.
- **Colleague**: Defines an interface for interacting with other colleagues through the mediator.
- **Concrete Colleague**: Implements the Colleague interface and communicates with other colleagues through the mediator.

### Example

Consider a scenario where we need to implement a chat room application where users can send messages to each other using the Mediator pattern:

```java
// Mediator interface
interface ChatMediator {
    void sendMessage(String message, User user);
    void addUser(User user);
}

// Concrete Mediator
class ChatRoom implements ChatMediator {
    private List<User> users;

    public ChatRoom() {
        this.users = new ArrayList<>();
    }

    @Override
    public void sendMessage(String message, User user) {
        for (User u : users) {
            if (u != user) {
                u.receiveMessage(message);
            }
        }
    }

    @Override
    public void addUser(User user) {
        users.add(user);
    }
}

// Colleague interface
interface User {
    void sendMessage(String message);
    void receiveMessage(String message);
}

// Concrete Colleague
class ChatUser implements User {
    private String name;
    private ChatMediator mediator;

    public ChatUser(String name, ChatMediator mediator) {
        this.name = name;
        this.mediator = mediator;
    }

    @Override
    public void sendMessage(String message) {
        System.out.println(name + " sends message: " + message);
        mediator.sendMessage(message, this);
    }

    @Override
    public void receiveMessage(String message) {
        System.out.println(name + " receives message: " + message);
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        ChatMediator chatMediator = new ChatRoom();

        User user1 = new ChatUser("User1", chatMediator);
        User user2 = new ChatUser("User2", chatMediator);
        User user3 = new ChatUser("User3", chatMediator);

        chatMediator.addUser(user1);
        chatMediator.addUser(user2);
        chatMediator.addUser(user3);

        user1.sendMessage("Hello, everyone!");
        user2.sendMessage("Hi, User1!");
    }
}
```
## Benefits
Promotes loose coupling by encapsulating communication logic between objects in a mediator.

Simplifies communication between objects, making the code easier to maintain and extend.

Improves scalability and flexibility by centralizing communication logic in a mediator object.

## Considerations
Care should be taken to design a clear and cohesive mediator interface to avoid bloating and maintainability issues.

The mediator should not become a god object, and its responsibilities should be limited to coordinating communication between objects.