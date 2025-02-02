## 🗑️ **What is Garbage Collection (GC)?**

- Garbage Collection (GC) is the automatic process of reclaiming memory occupied by unreachable objects in Java.
- It ensures efficient memory usage and helps prevent memory leaks.

---

## 🔑 **Key Concepts**

- **Heap Memory:** Divided into Young Generation, Old Generation, and sometimes Metaspace.
- **GC Roots:** References that are always accessible, including:
    - Static fields
    - Local variables on active threads
    - JVM internal references

---

## 📚 **The `finalize()` Method**

- The `finalize()` method is defined in the `Object` class and is called by the Garbage Collector before an object is collected.
- Typically used to clean up system resources.

### **Important Notes:**

- **Not Guaranteed:** The JVM does not guarantee that `finalize()` will ever be called.
- **Performance Issues:** Overusing `finalize()` can lead to performance bottlenecks.
- **Deprecated:** As of JDK 9, `finalize()` is deprecated due to unpredictability and better alternatives.

### **Example (Not Recommended):**

```java
@Override
protected void finalize() throws Throwable {
    try {
        System.out.println("Cleaning up resources...");
    } finally {
        super.finalize();
    }
}
```

### **Best Practice:**

- Use `try-with-resources` and explicit resource management instead of relying on `finalize()`.

---

## ⚙️ **How GC Works in Java (General Process)**

1. **Mark:** Identify all live objects.
2. **Sweep:** Remove unused objects and reclaim memory.
3. **Compact (Optional):** Rearrange memory to avoid fragmentation.

---

## 🚀 **Common GC Algorithms**

### **1. Serial GC**

- Single-threaded collection.
- Best for single-threaded applications.

### **2. Parallel GC**

- Multi-threaded collection.
- Suitable for high-throughput applications.

### **3. G1 GC**

- Balances pause time and throughput.
- Divides heap into regions for efficient collection.

### **4. Z Garbage Collector (ZGC)**

- Ultra-low pause times.
- Suitable for large heaps and low-latency applications.

---

## 🛠️ **Basic JVM GC Options**

```bash
-XX:+UseSerialGC         # Use Serial GC
-XX:+UseParallelGC       # Use Parallel GC
-XX:+UseG1GC             # Use G1 GC
-XX:+UseZGC              # Use Z Garbage Collector
```

---

## 🔍 **Key Takeaways**

- Garbage collection is essential for automatic memory management.
- Avoid using `finalize()`; prefer explicit resource handling.
- Choose the right GC algorithm based on application requirements.
- Monitor and tune GC performance using JVM options and profiling tools.