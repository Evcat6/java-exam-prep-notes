## Nested and Inner Classes in Java

### 1. Inner Classes (Non-Static Nested Classes)

Inner classes are defined within another class and have direct access to all fields and methods of the enclosing (outer) class.

#### Key Characteristics:

- Can access all fields and methods of the outer class directly.
- Members of the inner class can be accessed using `refToInnerClassObject.{property|methodName()}`.
- An inner class can only be instantiated when an instance of the outer class exists, using:
    
    ```java
    OuterClassName outer = new OuterClassName();
    OuterClassName.InnerClassName inner = outer.new InnerClassName();
    ```
    

#### 1.1 Qualified `this` & `super`

- An inner class retains a reference to the instance of the outer class that created it.
- You can access the outer class reference using `OuterClassName.this`.
- If the outer class extends another class, you can access its superclass using `OuterClassName.super`.

#### 1.2 Inner Classes Inside Inner Classes

If class `A` contains an inner class `B`, and `B` contains another inner class `C`, references to `A`'s members within `C` would look like this:

```java
A.this.someMethod();
```

> **Note:** While Java allows deep nesting of inner classes, excessive nesting can reduce code readability and should be used with caution.

### 2. Inheritance of Inner Classes

Inner classes can be inherited similarly to normal classes:

```java
class Outer {
    class Inner {}
}
class SubOuter extends Outer {
    class SubInner extends Inner {}
}
```

However, inner class inheritance is rare and should be used judiciously to maintain clarity.

### 3. Redefining Outer Class Properties in Inner Classes

If an inner class defines a method or variable with the same name as one in the outer class, the outer class's version is hidden within the inner class scope.

```java
class Outer {
    int value = 10;
    void display() { System.out.println("Outer display"); }
    class Inner {
        int value = 20;
        void display() { System.out.println("Inner display"); }
    }
}
```

> **Note:** The inner class introduces a new type and does not necessarily adhere to the contract of the outer class.

### 4. Local Classes (Method-Scoped Inner Classes)

Local classes are defined within a method, constructor, or non-static initialization block.

#### Key Characteristics:

- They behave like local variables and are only accessible within the enclosing block.
- They cannot have access modifiers (e.g., `public`, `private`).
- They cannot be `static`.
- References to them can be passed as arguments to methods.

```java
class Outer {
    void someMethod() {
        class LocalClass {
            void display() { System.out.println("Inside Local Class"); }
        }
        LocalClass local = new LocalClass();
        local.display();
    }
}
```

### 5. Anonymous Classes

Anonymous classes are unnamed classes that are declared and instantiated simultaneously, often for implementing interfaces or extending classes on the fly.

#### Key Characteristics:

- Created using `new` followed by a class or interface name.
- Commonly used for event handling and functional-style programming.
- Can initialize fields, even using non-static initialization blocks.

```java
abstract class Greeting {
    abstract void sayHello();
}
public class Test {
    public static void main(String[] args) {
        Greeting greeting = new Greeting() {
            void sayHello() { System.out.println("Hello from Anonymous Class!"); }
        };
        greeting.sayHello();
    }
}
```

### 6. Nested Types and Interfaces

- A Java interface can contain other interfaces and classes.
- Classes and interfaces defined within an interface are implicitly `public` and `static`.
- A nested class within an interface can serve as its default implementation.
- Nested types help enforce strong relationships between related types.

```java
interface OuterInterface {
    interface InnerInterface {
        void display();
    }
    class InnerClass implements InnerInterface {
        public void display() {
            System.out.println("InnerClass implementing InnerInterface");
        }
    }
}
```

By understanding and properly utilizing inner and nested classes, developers can write more maintainable and structured Java programs.