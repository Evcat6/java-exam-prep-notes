## 🔑 **Key Concepts**

- **Reference:** A variable that points to an object in memory.
- **Strong, Soft, Weak, and Phantom References:** Different types of references that define how the garbage collector (GC) handles objects.

---

## 💪 **1. Strong References (Default)**

- The standard reference type in Java.
- An object is not eligible for GC as long as it has strong references.

### **Example:**

```java
String strongRef = "Hello, World!";
```

- As long as `strongRef` points to the string, it won't be garbage collected.

---

## 🧹 **2. Soft References (Less Strict)**

- Used for memory-sensitive caches.
- GC may collect these objects only when memory is low.
- Defined using `SoftReference` class.

### **Example:**

```java
import java.lang.ref.SoftReference;

String data = new String("Important data");
SoftReference<String> softRef = new SoftReference<>(data);

// Clear the strong reference
data = null;
System.out.println(softRef.get()); // May still return the object
```

---

## 🐾 **3. Weak References (Weaker than Soft)**

- GC may collect these objects more aggressively.
- Useful for canonical mapping or caches that should not block GC.
- Defined using `WeakReference` class.

### **Example:**

```java
import java.lang.ref.WeakReference;

String weakData = new String("Weak data");
WeakReference<String> weakRef = new WeakReference<>(weakData);

weakData = null;
System.gc(); // Suggest garbage collection
System.out.println(weakRef.get()); // May return null after GC
```

---

## 🕳 **4. Phantom References (Post-Mortem Cleanup)**

- Used for advanced memory management (clean-up actions before GC).
- Always return `null` from `get()`.
- Defined using `PhantomReference` and requires a `ReferenceQueue`.

### **Example:**

```java
import java.lang.ref.PhantomReference;
import java.lang.ref.ReferenceQueue;

class Resource { /* Some resource */ }

Resource resource = new Resource();
ReferenceQueue<Resource> queue = new ReferenceQueue<>();
PhantomReference<Resource> phantomRef = new PhantomReference<>(resource, queue);

resource = null;
System.gc(); // Suggest garbage collection

if (queue.poll() != null) {
    System.out.println("Resource is ready for cleanup.");
}
```

---

## 🔍 **Reference Best Practices**

- **Strong References:** Default, suitable for critical business data.
- **Soft References:** Use for memory-sensitive caches.
- **Weak References:** Ideal for caching non-essential objects.
- **Phantom References:** Advanced use cases like pre-finalization cleanup.

---

## ⚠️ **Important Notes**

- Always manage references with care to avoid memory leaks.
- Test caching strategies to balance performance and memory efficiency.
- Use `ReferenceQueue` for clean-up logic when handling phantom references.