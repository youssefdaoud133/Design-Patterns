# Proxy Design Pattern

<p align="center">
  <img src="../photos/Proxy.png" alt="Alt text" />
</p>

### Problem

The Proxy design pattern addresses the problem of controlling access to an object, either for security reasons, to reduce the cost of accessing it, or to add additional functionality. Sometimes, the object might be resource-intensive to create or may need to perform specific actions before or after access.

### Solution

The Proxy design pattern involves creating a proxy object that controls access to the original object. The proxy object implements the same interface as the original object, thus making it a substitute for the original object. The proxy can handle various tasks such as lazy initialization, access control, logging, and more.

### When to Use

Use the Proxy design pattern when:

- You need to control access to an object.
- You want to add a layer of security or access control.
- You need to add functionality before or after accessing the object.
- The object is resource-intensive to create and you want to use lazy initialization.

### Example Code

```java
// Subject
interface Image {
    void display();
}

// RealSubject
class RealImage implements Image {
    private final String filename;

    public RealImage(String filename) {
        this.filename = filename;
        loadFromDisk();
    }

    private void loadFromDisk() {
        System.out.println("Loading " + filename);
    }

    @Override
    public void display() {
        System.out.println("Displaying " + filename);
    }
}

// Proxy
class ProxyImage implements Image {
    private final String filename;
    private RealImage realImage;

    public ProxyImage(String filename) {
        this.filename = filename;
    }

    @Override
    public void display() {
        if (realImage == null) {
            realImage = new RealImage(filename);
        }
        realImage.display();
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        Image image = new ProxyImage("test_image.jpg");

        // Image will be loaded from disk
        image.display();

        // Image will not be loaded from disk, will use the already created RealImage
        image.display();
    }
}
```

### Cons

- **Overhead**: The proxy can introduce additional overhead, particularly if the operations it performs are not trivial.
- **Complexity**: Adding a proxy layer can increase the complexity of the system, making it harder to understand and maintain.
- **Latency**: In some cases, the proxy might introduce latency, particularly if it performs remote calls or adds significant processing.
- **Consistency**: If the proxy does not properly synchronize access to the real object, it can lead to inconsistent states or data races in multithreaded environments.

### Variants of Proxy

1. **Virtual Proxy**: Controls access to a resource that is expensive to create. It creates the resource on demand (lazy initialization).
2. **Protection Proxy**: Controls access to a resource based on access rights.
3. **Remote Proxy**: Represents an object located in a different address space (e.g., in a different machine).
4. **Smart Proxy**: Adds additional behavior when an object is accessed (e.g., reference counting, logging).

Using proxies helps manage the complexity and efficiency of object interactions in a system, providing control over how and when certain operations are performed.