### 1. Generics Overview

Generics allow you to create classes, interfaces, and methods with type parameters, making code more reusable and type-safe.

#### Key Benefits:

- **Type Safety:** Detects type mismatch at compile time.
- **Code Reusability:** Allows writing generic code applicable to multiple data types.
- **Eliminates Type Casting:** No need for explicit type casting.

```java
class Box<T> {
    private T item;
    void setItem(T item) { this.item = item; }
    T getItem() { return item; }
}
```

### 2. Generics and Nested Classes

Nested and inner classes can also use generics to create more flexible and reusable code.

#### Difference Between Nested and Inner Classes in Generics

- **Static Nested Classes** do **not** have access to the generic type of the outer class. If a nested class needs generics, it must declare its own type parameter.
- **Inner Classes** (non-static) **do** have access to the generic type of the outer class, meaning they can use the same type parameter without needing to declare it again.

#### Generic Nested Classes:

```java
class Outer<T> {
    class Inner {
        void display(T item) {
            System.out.println("Item: " + item);
        }
    }
}
```

#### Static Nested Classes with Generics:

```java
class Outer {
    static class Nested<T> {
        private T value;
        Nested(T value) { this.value = value; }
        T getValue() { return value; }
    }
}
```

### 3. Generic Methods

Generic methods allow flexibility by enabling parameterized types independent of the class.

```java
class Utility {
    public static <T> void printArray(T[] array) {
        for (T element : array) {
            System.out.print(element + " ");
        }
        System.out.println();
    }
}
```

### 4. Wildcards in Generics

Wildcards (`?`) help generalize types while maintaining type safety.

#### **Unbounded Wildcard (`?`)**

Accepts any type:

```java
void printList(List<?> list) {
    for (Object obj : list) {
        System.out.println(obj);
    }
}
```

#### **Upper-Bounded Wildcard (`? extends T`)**

Accepts `T` or subclasses of `T`. It is useful when you want to read values but not modify them.

```java
void processNumbers(List<? extends Number> list) {
    for (Number num : list) {
        System.out.println(num.doubleValue());
    }
}
```

> **Note:** You cannot add elements to a list declared as `List<? extends T>` because the exact type is unknown.

#### **Lower-Bounded Wildcard (`? super T`)**

Accepts `T` or any superclass of `T`. It is useful when you want to modify a collection.

```java
void addNumbers(List<? super Integer> list) {
    list.add(10);
}
```

> **Note:** You can add elements to a list declared as `List<? super T>`, but retrieving elements will return `Object`.

### 5. Generic Interfaces

Interfaces can be generic to define flexible contracts for multiple types.

```java
interface Container<T> {
    void add(T item);
    T get();
}
```

### 6. Bounded Type Parameters

You can restrict generic types to certain classes or interfaces.

```java
class NumberBox<T extends Number> {
    private T num;
    void setNum(T num) { this.num = num; }
    double getDoubleValue() { return num.doubleValue(); }
}
```

> **Note:** `T extends Number` means that `T` can only be `Number` or its subclasses (`Integer`, `Double`, etc.).

### 7. Multiple Bounds

A generic type can have multiple bounds using `&`.

```java
class MultiBound<T extends Number & Comparable<T>> {
    private T value;
    MultiBound(T value) { this.value = value; }
    T getValue() { return value; }
}
```

> **Note:** If multiple bounds are specified, the first must always be a class, and the rest must be interfaces.

### 8. Generics and Anonymous Classes

Generics work with anonymous classes but must be explicitly declared.

```java
abstract class Processor<T> {
    abstract T process(T input);
}
public class Main {
    public static void main(String[] args) {
        Processor<Integer> square = new Processor<>() {
            Integer process(Integer input) { return input * input; }
        };
        System.out.println(square.process(5));
    }
}
```

By leveraging generics effectively, Java developers can create more flexible, reusable, and type-safe code!