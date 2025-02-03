### 1. Decorator Pattern

The **Decorator Pattern** is used to dynamically extend the behavior of objects without modifying their structure.

#### Key Features:

- Promotes flexible and reusable code.
- Avoids subclass explosion.
- Uses composition instead of inheritance.

#### Implementation:

```java
interface Coffee {
    String getDescription();
    double getCost();
}

class SimpleCoffee implements Coffee {
    public String getDescription() { return "Simple Coffee"; }
    public double getCost() { return 5.0; }
}

class MilkDecorator implements Coffee {
    private Coffee coffee;
    MilkDecorator(Coffee coffee) { this.coffee = coffee; }
    public String getDescription() { return coffee.getDescription() + ", Milk"; }
    public double getCost() { return coffee.getCost() + 1.5; }
}

public class DecoratorDemo {
    public static void main(String[] args) {
        Coffee coffee = new MilkDecorator(new SimpleCoffee());
        System.out.println(coffee.getDescription() + " = $" + coffee.getCost());
    }
}
```

### 2. Observer Pattern

The **Observer Pattern** is used for a one-to-many dependency between objects, where a change in one object triggers updates in its dependents.

#### Key Features:

- Loosely coupled architecture.
- Supports dynamic relationships.
- Used in event-driven systems (e.g., GUI, notifications).

#### Implementation:

```java
import java.util.*;

interface Observer {
    void update(String message);
}

class User implements Observer {
    private String name;
    User(String name) { this.name = name; }
    public void update(String message) {
        System.out.println(name + " received update: " + message);
    }
}

class NewsAgency {
    private List<Observer> observers = new ArrayList<>();
    void addObserver(Observer o) { observers.add(o); }
    void removeObserver(Observer o) { observers.remove(o); }
    void notifyObservers(String news) {
        for (Observer o : observers) {
            o.update(news);
        }
    }
}

public class ObserverDemo {
    public static void main(String[] args) {
        NewsAgency agency = new NewsAgency();
        Observer user1 = new User("Alice");
        Observer user2 = new User("Bob");
        
        agency.addObserver(user1);
        agency.addObserver(user2);
        
        agency.notifyObservers("Breaking News!");
    }
}
```

### 3. When to Use

- **Decorator Pattern** is useful when adding responsibilities dynamically without affecting other instances.
- **Observer Pattern** is ideal for event-driven systems where multiple objects need updates when a subject changes.

By using these patterns, you can design more maintainable and scalable applications.