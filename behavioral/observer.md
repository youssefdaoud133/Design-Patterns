# Observer Design Pattern
<p align="center">
  <img src="../photos/Copy of 8-1 SubjectObserverAnalogy.jpg" alt="Alt text" />
</p>


The Observer pattern is a behavioral design pattern that defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically. It enables objects to maintain consistency and synchronization without tight coupling, promoting loose coupling and scalability.

## Problem

In software development, there are scenarios where multiple objects need to be notified and updated when the state of another object changes. However, directly coupling the observer objects to the subject object can lead to several issues:

- Tight coupling: Observer objects are directly dependent on the subject object, making the code harder to maintain and extend.
- Lack of flexibility: Changing the subject object or adding new observers may require modifications to existing code, violating the principle of open/closed principle.
- Inefficient polling: Polling for state changes can be inefficient and resource-intensive, especially for objects with frequent state changes.

## Solution

The Observer pattern addresses these issues by defining a one-to-many dependency between objects, where the subject object maintains a list of its dependents (observers) and notifies them automatically when its state changes. This decouples the subject object from its observers, enabling objects to maintain consistency and synchronization without tight coupling. 

## Implementation

### Structure

The Observer pattern typically consists of the following components:

- **Subject**: Maintains a list of observers and provides methods for attaching, detaching, and notifying observers.
- **Observer**: Defines an interface for receiving update notifications from the subject.
- **Concrete Subject**: Implements the Subject interface and notifies observers of state changes.
- **Concrete Observer**: Implements the Observer interface and receives update notifications from the subject.

### Example

Consider a scenario where we need to implement a weather station application where multiple display devices need to be updated with weather data using the Observer pattern:

```java
import java.util.ArrayList;
import java.util.List;

// Subject
interface Subject {
    void attach(Observer observer);
    void detach(Observer observer);
    void notifyObservers();
}

// Observer
interface Observer {
    void update(String weatherData);
}

// Concrete Subject
class WeatherStation implements Subject {
    private List<Observer> observers = new ArrayList<>();
    private String weatherData;

    public void setWeatherData(String weatherData) {
        this.weatherData = weatherData;
        notifyObservers();
    }

    @Override
    public void attach(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void detach(Observer observer) {
        observers.remove(observer);
    }

    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(weatherData);
        }
    }
}

// Concrete Observer
class DisplayDevice implements Observer {
    private String name;

    public DisplayDevice(String name) {
        this.name = name;
    }

    @Override
    public void update(String weatherData) {
        System.out.println(name + " received weather update: " + weatherData);
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        WeatherStation weatherStation = new WeatherStation();

        DisplayDevice displayDevice1 = new DisplayDevice("Display 1");
        DisplayDevice displayDevice2 = new DisplayDevice("Display 2");

        weatherStation.attach(displayDevice1);
        weatherStation.attach(displayDevice2);

        weatherStation.setWeatherData("Sunny");
        weatherStation.setWeatherData("Rainy");

        weatherStation.detach(displayDevice2);

        weatherStation.setWeatherData("Cloudy");
    }
}
```
## Benefits
Promotes loose coupling between objects, making the code easier to maintain and extend.

Enables objects to maintain consistency and synchronization without tight coupling.

Supports one-to-many relationships between objects, allowing multiple observers to listen to a single subject.

## Considerations
Care should be taken to manage the lifecycle of observer objects to avoid memory leaks or excessive memory consumption.

Observer objects should avoid performing heavy processing in their update methods to prevent blocking the subject's notification mechanism.