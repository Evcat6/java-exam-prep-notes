## 📦 **Import Required Package**

```java
import java.lang.reflect.*;
```

---

## 🏷️ **Get Class Object**

- From an Object:
    
    ```java
    Class<?> clazz = obj.getClass();
    ```
    
- From Class Name:
    
    ```java
    Class<?> clazz = Class.forName("com.example.MyClass");
    ```
    
- From Type:
    
    ```java
    Class<MyClass> clazz = MyClass.class;
    ```
    

---

## 🔍 **Inspect Class Details**

- **Get Class Name:**
    
    ```java
    String name = clazz.getName(); // Full class name
    String simpleName = clazz.getSimpleName(); // Class name only
    ```
    
- **Get Modifiers:**
    
    ```java
    int modifiers = clazz.getModifiers();
    boolean isPublic = Modifier.isPublic(modifiers);
    ```
    
- **Get Superclass:**
    
    ```java
    Class<?> superclass = clazz.getSuperclass();
    ```
    
- **Get Interfaces:**
    
    ```java
    Class<?>[] interfaces = clazz.getInterfaces();
    ```
    

---

## 📋 **Inspect Fields**

- **Get All Fields:**
    
    ```java
    Field[] fields = clazz.getDeclaredFields(); // All fields
    Field[] publicFields = clazz.getFields(); // Only public fields
    ```
    
- **Access a Specific Field:**
    
    ```java
    Field field = clazz.getDeclaredField("fieldName");
    ```
    
- **Modify Field Value:**
    
    ```java
    field.setAccessible(true); // For private fields
    field.set(obj, newValue); // Set value
    Object value = field.get(obj); // Get value
    ```
    

---

## 🔧 **Inspect Methods**

- **Get All Methods:**
    
    ```java
    Method[] methods = clazz.getDeclaredMethods(); // All methods
    Method[] publicMethods = clazz.getMethods(); // Only public methods
    ```
    
- **Access a Specific Method:**
    
    ```java
    Method method = clazz.getDeclaredMethod("methodName", paramType1, paramType2);
    ```
    
- **Invoke a Method:**
    
    ```java
    method.setAccessible(true); // For private methods
    Object result = method.invoke(obj, arg1, arg2);
    ```
    

---

## 🏗️ **Inspect Constructors**

- **Get All Constructors:**
    
    ```java
    Constructor<?>[] constructors = clazz.getDeclaredConstructors();
    ```
    
- **Access a Specific Constructor:**
    
    ```java
    Constructor<MyClass> constructor = clazz.getDeclaredConstructor(paramType1, paramType2);
    ```
    
- **Create a New Instance:**
    
    ```java
    constructor.setAccessible(true);
    MyClass instance = constructor.newInstance(arg1, arg2);
    ```
    

---

## ⚠️ **Handling Exceptions**

Always handle exceptions when using reflection:

```java
try {
    // Reflection operations
} catch (NoSuchFieldException | NoSuchMethodException |
         IllegalAccessException | InvocationTargetException |
         InstantiationException e) {
    e.printStackTrace();
}
```