### 1. Introduction to Java Collections

Java provides the **Collections Framework** to manage and manipulate groups of objects efficiently.

### 2. Core Interfaces

|Interface|Description|
|---|---|
|`List<E>`|Ordered collection (allows duplicates)|
|`Set<E>`|Unordered collection (no duplicates)|
|`Queue<E>`|FIFO (First-In-First-Out) collection|
|`Deque<E>`|Double-ended queue (supports both FIFO & LIFO)|
|`Map<K,V>`|Collection of key-value pairs (no duplicate keys)|

### 3. Common Implementations

|Interface|Implementation|Features|
|---|---|---|
|`List`|`ArrayList`|Dynamic array, fast read, slow insert/remove|
|`List`|`LinkedList`|Doubly linked list, fast insert/remove|
|`Set`|`HashSet`|No duplicates, unordered, fast operations|
|`Set`|`TreeSet`|No duplicates, sorted order|
|`Queue`|`PriorityQueue`|Elements ordered by priority|
|`Deque`|`ArrayDeque`|Faster than `Stack` & `LinkedList`|
|`Map`|`HashMap`|Key-value pairs, fast lookup|
|`Map`|`TreeMap`|Sorted keys|
|`Map`|`LinkedHashMap`|Maintains insertion order|

### 4. ArrayList Example

```java
import java.util.*;

public class ArrayListExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Orange");
        
        for (String fruit : list) {
            System.out.println(fruit);
        }
    }
}
```

### 5. HashMap Example

```java
import java.util.*;

public class HashMapExample {
    public static void main(String[] args) {
        Map<Integer, String> map = new HashMap<>();
        map.put(1, "John");
        map.put(2, "Jane");
        map.put(3, "Jack");
        
        for (Map.Entry<Integer, String> entry : map.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
    }
}
```

### 6. Sorting Collections

```java
import java.util.*;

public class SortingExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(5, 2, 8, 1, 3);
        Collections.sort(numbers);
        System.out.println(numbers);
    }
}
```

### 7. Using Streams with Collections

```java
import java.util.*;
import java.util.stream.*;

public class StreamExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");
        List<String> filteredNames = names.stream()
                                          .filter(name -> name.startsWith("A"))
                                          .collect(Collectors.toList());
        System.out.println(filteredNames);
    }
}
```

### 8. Summary

|Collection Type|Best Used For|
|---|---|
|`ArrayList`|Fast read, dynamic resizing|
|`LinkedList`|Fast insert/remove operations|
|`HashSet`|Unique elements, fast access|
|`TreeSet`|Unique elements, sorted order|
|`HashMap`|Key-value storage, fast lookup|
|`TreeMap`|Sorted key-value pairs|

By mastering Java Collections, you can efficiently manage and manipulate groups of objects in your applications.