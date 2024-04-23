# Adapter Design Pattern

<p align="center">
  <img src="../photos/adapter.png" alt="Alt text" />
</p>

The Adapter pattern is a structural design pattern that allows incompatible interfaces to work together. It acts as a bridge between two incompatible interfaces by providing a wrapper that converts the interface of a class into another interface that clients expect. This promotes interoperability, reusability, and maintainability by allowing objects with different interfaces to collaborate seamlessly.

## Problem

In software development, there are scenarios where clients expect objects with specific interfaces, but the available classes or components provide incompatible interfaces. However, modifying existing classes or components to conform to the expected interface may not be feasible due to various reasons, including:

- Legacy code: Modifying existing classes or components may require extensive changes to legacy code, leading to potential regressions and increased complexity.
- Third-party libraries: Modifying third-party libraries to conform to the expected interface may not be possible or practical due to licensing or maintenance issues.
- Stability concerns: Modifying stable or widely-used classes or components may introduce unnecessary risks and dependencies, affecting system stability.

## Solution

The Adapter pattern addresses these issues by providing a wrapper class that adapts the interface of one class to match the interface expected by clients. It encapsulates the complexities of interface conversion within the adapter, allowing clients to interact with the adapted class as if it were the original class. This promotes interoperability, reusability, and maintainability by enabling objects with different interfaces to collaborate seamlessly.

## Implementation

### Structure

The Adapter pattern typically consists of the following components:

- **Target**: Defines the interface expected by clients.
- **Adapter**: Implements the Target interface and adapts the interface of the Adaptee to match the Target interface.
- **Adaptee**: Defines the existing interface that needs to be adapted.
- **Client**: Interacts with objects through the Target interface without being aware of the underlying implementation details.

### Example

Consider a scenario where we need to adapt a legacy system that provides temperature data in Fahrenheit to work with a new client that expects temperature data in Celsius using the Adapter pattern:

```java
// Target
interface CelsiusTemperatureProvider {
    double getTemperatureInCelsius();
}

// Adaptee
class FahrenheitTemperatureProvider {
    double getTemperatureInFahrenheit() {
        // Logic to get temperature in Fahrenheit
        return 77.0; // Example temperature in Fahrenheit
    }
}

// Adapter
class FahrenheitToCelsiusAdapter implements CelsiusTemperatureProvider {
    private final FahrenheitTemperatureProvider fahrenheitProvider;

    public FahrenheitToCelsiusAdapter(FahrenheitTemperatureProvider fahrenheitProvider) {
        this.fahrenheitProvider = fahrenheitProvider;
    }

    @Override
    public double getTemperatureInCelsius() {
        // Convert Fahrenheit to Celsius
        double fahrenheit = fahrenheitProvider.getTemperatureInFahrenheit();
        return (fahrenheit - 32) * 5 / 9;
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        FahrenheitTemperatureProvider fahrenheitProvider = new FahrenheitTemperatureProvider();
        CelsiusTemperatureProvider adapter = new FahrenheitToCelsiusAdapter(fahrenheitProvider);

        System.out.println("Temperature in Celsius: " + adapter.getTemperatureInCelsius());
    }
}
```
## Benefits
Promotes interoperability between incompatible interfaces, allowing objects with different interfaces to collaborate seamlessly.

Encapsulates interface conversion logic within the adapter, enabling clients to interact with objects through a common interface.

Enhances reusability and maintainability by providing a reusable wrapper that adapts existing classes or components to new interfaces.

## Considerations
Care should be taken to properly design adapter interfaces to ensure compatibility with the target interface.

Adapters should be designed to handle edge cases and corner cases gracefully to prevent unexpected behavior or errors.
