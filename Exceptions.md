![[chrome_uZo0coxg9x.png]]
## 🚫 **Common Exception Types**

- **Checked Exceptions:** Must be declared or handled
    - `IOException`
    - `SQLException`
    - `ClassNotFoundException`
- **Unchecked Exceptions:** Runtime errors
    - `NullPointerException`
    - `ArrayIndexOutOfBoundsException`
    - `IllegalArgumentException`
- **Errors:** Serious issues
    - `OutOfMemoryError`
    - `StackOverflowError`

---

## ⚠️ **Handling Exceptions**

### **Basic Try-Catch Block**

```java
try {
    // Code that might throw an exception
} catch (ExceptionType e) {
    e.printStackTrace();
}
```

### **Multiple Catch Blocks**

```java
try {
    // Code that might throw multiple exceptions
} catch (IOException e) {
    e.printStackTrace();
} catch (SQLException e) {
    e.printStackTrace();
}
```

### **Finally Block**

```java
try {
    // Code that might throw an exception
} catch (Exception e) {
    e.printStackTrace();
} finally {
    // Cleanup code (executed regardless of exception)
}
```

---

## 👀 **Throwing Exceptions**

### **Throwing Custom Exceptions**

```java
throw new IllegalArgumentException("Invalid argument");
```

### **Method Declaration with Throws Clause**

```java
public void myMethod() throws IOException, SQLException {
    // Code that might throw exceptions
}
```

---

## 🔄 **Creating Custom Exceptions**

```java
class MyCustomException extends Exception {
    public MyCustomException(String message) {
        super(message);
    }
}
```

---

## 🔍 **Best Practices**

- Catch specific exceptions first.
- Use meaningful exception messages.
- Avoid catching `Exception` or `Throwable` unless necessary.
- Always clean up resources in the `finally` block or use try-with-resources.
- Create custom exceptions for domain-specific errors.