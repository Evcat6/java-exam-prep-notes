## 📝 **What Are Assertions?**

- Assertions are statements used to test assumptions in code.
- They help detect logic errors by verifying conditions during runtime.
- Available via the `assert` keyword in Java.

---

## 🔧 **Enabling Assertions**

- Assertions are disabled by default.
- To enable assertions, run the JVM with the `-ea` or `-enableassertions` flag:
    
    ```bash
    java -ea MyApp
    ```
    
- To selectively enable assertions for specific packages or classes:
    
    ```bash
    java -ea:com.example... -ea:MyClass
    ```
    
- Disable assertions using `-da` or `-disableassertions`.

---

## 🛠 **Basic Usage**

### **Syntax:**

```java
assert condition;
```

If `condition` evaluates to `false`, an `AssertionError` is thrown.

### **With an Error Message:**

```java
assert condition : "Error message";
```

The error message is passed to the `AssertionError` if the condition fails.

### **Example:**

```java
public class AssertionExample {
    public static void main(String[] args) {
        int age = -1;
        assert age >= 0 : "Age must be non-negative";
        System.out.println("Age: " + age);
    }
}
```

---

## ⚠️ **When to Use Assertions**

- **Preconditions:** Validate assumptions about method arguments (only for internal checks).
- **Postconditions:** Ensure expected outcomes after method execution.
- **Invariant Checks:** Validate the consistency of an object's state.
- **Unreachable Code:** Assert that certain code paths should never be executed.

### **Example:**

```java
switch (direction) {
    case "UP":
    case "DOWN":
    case "LEFT":
    case "RIGHT":
        // Valid cases
        break;
    default:
        assert false : "Unknown direction";
}
```

---

## ❌ **What Not to Use Assertions For**

- **Argument Validation:** Use exceptions (`IllegalArgumentException`, `NullPointerException`, etc.) for validating public method arguments.
- **Critical Runtime Conditions:** Don't use assertions for conditions that must always be checked, even in production.

---

## 💡 **Best Practices**

- Enable assertions during testing and development.
- Write meaningful error messages to help debug issues.
- Avoid using assertions for side-effect operations.
- Document assumptions verified by assertions.

---

## 🧪 **Testing Assertions**

- Ensure your test environment always enables assertions.
- Use automated tests to verify that assertions catch invalid conditions.