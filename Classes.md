## 📖 **Basic Structure of a Java Class**

```java
public class MyClass {
    // Fields (variables)
    private int number;
    private String text;

    // Constructor
    public MyClass(int number, String text) {
        this.number = number;
        this.text = text;
    }

    // Methods
    public int getNumber() {
        return number;
    }

    public void setNumber(int number) {
        this.number = number;
    }

    public void display() {
        System.out.println("Number: " + number + ", Text: " + text);
    }

    // Main method
    public static void main(String[] args) {
        MyClass obj = new MyClass(42, "Hello, World!");
        obj.display();
    }
}
```

---

## 🔑 **Class Components**

- **Fields:** Variables defined within a class.
- **Methods:** Functions that define behavior.
- **Constructors:** Initialize new objects.
- **Access Modifiers:** Control visibility (`public`, `private`, `protected`, package-private).
- **Static Members:** Shared across all instances of the class.
- **Inner Classes:** Nested classes inside a parent class.

---

## 🛡️ **Access Modifiers**

| Modifier    | Same Class | Same Package | Subclass | Everywhere |
| ----------- | ---------- | ------------ | -------- | ---------- |
| `public`    | ✔          | ✔            | ✔        | ✔          |
| `protected` | ✔          | ✔            | ✔        | ❌          |
| No Modifier | ✔          | ✔            | ❌        | ❌          |
| `private`   | ✔          | ❌            | ❌        | ❌          |


---

## 🔧 **Constructors**

- **Default Constructor:** Provided by Java if no constructor is defined.
- **Parameterized Constructor:** Allows setting fields during object creation.

```java
public MyClass(int number) {
    this.number = number;
}
```

- **Constructor Overloading:** Multiple constructors with different parameters.

```java
public MyClass() { }

public MyClass(int number) { this.number = number; }
```

---

## 🚀 **Static Members**

- **Static Variables:** Shared by all instances.
- **Static Methods:** Cannot access instance fields or methods.
- **Static Block:** Executes once when the class is loaded.

```java
public class StaticExample {
    static int count = 0;

    static {
        System.out.println("Static block executed");
    }

    public static void displayCount() {
        System.out.println("Count: " + count);
    }
}
```

---

## 💾 **Inheritance**

- Enables a class to inherit properties and methods from a parent class.

```java
class Parent {
    public void display() {
        System.out.println("Parent method");
    }
}

class Child extends Parent {
    public void display() {
        System.out.println("Child method");
    }
}

Parent obj = new Child(); // Polymorphism
obj.display(); 
```

### **Key Concepts:**

- `super`: Access parent class members.
- Method overriding.
- Constructors are not inherited.
- Avoid multiple inheritance (use interfaces).

---

## 📦 **Encapsulation**

- Restricts direct access to fields.
- Achieved using private fields and public getter/setter methods.

```java
class EncapsulatedClass {
    private int value;

    public int getValue() {
        return value;
    }

    public void setValue(int value) {
        this.value = value;
    }
}
```

---

## 🔄 **Polymorphism**

### **1. Compile-Time (Method Overloading)**

```java
class OverloadExample {
    void display(int number) {
        System.out.println(number);
    }

    void display(String text) {
        System.out.println(text);
    }
}
```

### **2. Runtime (Method Overriding)**

```java
class Parent {
    void show() { System.out.println("Parent class"); }
}

class Child extends Parent {
    @Override
    void show() { System.out.println("Child class"); }
}
```

---

## 🔗 **Abstraction (Abstract Classes and Interfaces)**

### **Abstract Class**

```java
abstract class Animal {
    abstract void sound();

    public void eat() {
        System.out.println("Eating...");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Bark");
    }
}
```

### **Interface**

```java
interface Animal {
    void sound();
}

class Dog implements Animal {
    @Override
    public void sound() {
        System.out.println("Bark");
    }
}
```

- Interfaces support multiple inheritance.
- Default and static methods are allowed in interfaces.

---

## ⚙️ **Inner Classes**

### **1. Member Inner Class**

```java
class OuterClass {
    class InnerClass {
        void display() {
            System.out.println("Inner Class");
        }
    }
}
```

### **2. Static Nested Class**

```java
class OuterClass {
    static class NestedStaticClass {
        void display() {
            System.out.println("Nested Static Class");
        }
    }
}
```

### **3. Anonymous Inner Class**

```java
Runnable r = new Runnable() {
    public void run() {
        System.out.println("Anonymous Inner Class");
    }
};
r.run();
```

---

## 🔍 **Object Class and Important Methods**

### **Key Methods:**

- `toString()`: Returns string representation.
- `equals(Object obj)`: Compares two objects for equality.
- `hashCode()`: Returns the hash code.
- `clone()`: Creates a copy of the object.
- `finalize()`: Called before object is garbage-collected.

### **Example:**

```java
@Override
public String toString() {
    return "MyClass: number=" + number;
}
```

---

## 🔧 **Best Practices for Java Classes**

1. **Encapsulation:** Always use private fields and public getters/setters.
2. **Immutable Classes:** Use `final` fields and no setters.
3. **Use Constructor Overloading:** Provide flexibility for object creation.
4. **Minimize Usage of `static`:** Use only when necessary.
5. **Override `toString`, `equals`, and `hashCode`:** For better object comparison and representation.
6. **Follow Naming Conventions:** Use PascalCase for classes and camelCase for methods/variables.

This cheat sheet covers all the essential and advanced topics related to Java classes. Master these, and you'll have a solid understanding of how to work efficiently with classes in Java!