## 🔑 **Key Concepts and Terminology**

- **Thread:** A separate path of execution within a program.
- **Concurrency:** Multiple threads executing simultaneously within a program.
- **Parallelism:** True simultaneous execution on multiple processors.
- **Thread Safety:** Ensures that shared data is accessed consistently across threads.
- **Critical Section:** A part of the program that should not be executed by more than one thread simultaneously.

---

## 🔧 **Thread Creation Methods**

### **1. Extending `Thread` Class**

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running...");
    }
}
MyThread thread = new MyThread();
thread.start();
```

### **2. Implementing `Runnable` Interface**

```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Thread is running...");
    }
}
Thread thread = new Thread(new MyRunnable());
thread.start();
```

### **3. Using `Callable` and `Future` (with Result Return)**

```java
ExecutorService executor = Executors.newSingleThreadExecutor();
Future<Integer> result = executor.submit(() -> 42);

try {
    System.out.println("Result: " + result.get());
} catch (Exception e) {
    e.printStackTrace();
}
executor.shutdown();
```

---

## 🔑 **Thread Synchronization**

### **1. `synchronized` Keyword**

- Ensures only one thread can access a synchronized block or method.

#### **Synchronized Method**

```java
public synchronized void synchronizedMethod() {
    // critical section
}
```

#### **Synchronized Block**

```java
public void method() {
    synchronized(this) {
        // critical section
    }
}
```

#### **Class-Level Synchronization**

```java
synchronized (MyClass.class) {
    // synchronized block on class level
}
```

### **What to Avoid:**

- Avoid synchronizing on mutable objects.
- Minimize the scope of synchronization to improve performance.

---

## 📞 **Thread Communication (`wait`, `notify`, `notifyAll`)**

### **Concepts:**

- **`wait()`**: Puts the current thread into a waiting state until notified.
- **`notify()`**: Wakes up one waiting thread.
- **`notifyAll()`**: Wakes up all waiting threads.

### **Usage Guidelines:**

- Always call `wait`, `notify`, and `notifyAll` within synchronized blocks.
- Threads waiting on a condition must hold the monitor lock.

### **Example:**

```java
class SharedResource {
    private boolean available = false;

    synchronized void produce() throws InterruptedException {
        while (available) {
            wait();
        }
        available = true;
        System.out.println("Produced item");
        notifyAll();
    }

    synchronized void consume() throws InterruptedException {
        while (!available) {
            wait();
        }
        available = false;
        System.out.println("Consumed item");
        notifyAll();
    }
}
```

---

## ❌ **Thread Interruption**

### **How It Works:**

- **Interrupting a Thread:**

```java
thread.interrupt();
```

- **Handling Interruption:**

```java
try {
    Thread.sleep(1000);
} catch (InterruptedException e) {
    System.out.println("Thread interrupted");
}
```

- **Best Practices:**
    
    - Always restore the interrupt status if catching `InterruptedException` in library code.
    
    ```java
    Thread.currentThread().interrupt();
    ```
    

---

## 🔒 **Advanced Locks (`Lock`, `Condition`)**

### **1. `ReentrantLock`**

```java
Lock lock = new ReentrantLock();
lock.lock();
try {
    // critical section
} finally {
    lock.unlock();
}
```

### **2. `Condition` for Thread Communication**

```java
Condition condition = lock.newCondition();
lock.lock();
try {
    condition.await(); // wait
    condition.signal(); // wake up
} finally {
    lock.unlock();
}
```

---

## 📋 **Blocking Queues (`BlockingQueue`)**

### **Concept:**

- Thread-safe queues that block when attempting to add or retrieve elements under certain conditions.
- Used for producer-consumer patterns.

### **Example:**

```java
BlockingQueue<String> queue = new ArrayBlockingQueue<>(10);
queue.put("Item"); // Blocking operation
String item = queue.take(); // Blocking retrieval
```

---

## 🚧 **Synchronization Utilities**

### **1. CyclicBarrier**

- Synchronizes multiple threads at a common barrier point.

```java
CyclicBarrier barrier = new CyclicBarrier(3, () -> System.out.println("All threads reached the barrier"));

Runnable task = () -> {
    try {
        System.out.println(Thread.currentThread().getName() + " is waiting");
        barrier.await();
    } catch (Exception e) {
        e.printStackTrace();
    }
};
```

### **2. ReadWriteLock**

- Allows multiple readers or one writer at a time.

```java
ReadWriteLock lock = new ReentrantReadWriteLock();
lock.readLock().lock();
try {
    // Read operation
} finally {
    lock.readLock().unlock();
}

lock.writeLock().lock();
try {
    // Write operation
} finally {
    lock.writeLock().unlock();
}
```

---

## 🔑 **Volatile Keyword**

### **Concept:**

- The `volatile` keyword ensures visibility of changes to variables across threads.
- Prevents compiler optimizations that might reorder instructions involving the variable.

### **Usage Example:**

```java
class SharedResource {
    private volatile boolean flag = false;

    public void setFlag() {
        flag = true;
    }

    public void checkFlag() {
        while (!flag) {
            // Spin-wait until flag becomes true
        }
        System.out.println("Flag set!");
    }
}
```

### **When to Use:**

- Use for simple flags and state indicators that are read and written by multiple threads.

---

## 🔑 **Atomic Classes (`AtomicReference`)**

### **Concept:**

- Provides lock-free thread-safe operations on single variables.
- Available in `java.util.concurrent.atomic` package.

### **Example:**

```java
import java.util.concurrent.atomic.AtomicReference;

class AtomicExample {
    private AtomicReference<String> message = new AtomicReference<>("Initial");

    public void updateMessage(String newMessage) {
        message.set(newMessage);
    }

    public String getMessage() {
        return message.get();
    }
}
```

### **When to Use:**

- Use `AtomicReference` when multiple threads need to safely read and write to an object reference without locking.


---

## 👿 Daemon Threads

### Key Characteristics:

- **Background Execution:** Daemon threads run in the background and perform auxiliary tasks.
- **Application Termination:** The JVM automatically exits when all user threads have completed, even if daemon threads are still running.
- **Low Priority:** These threads generally have lower priority compared to user threads.

### Important Methods:

- `setDaemon(boolean on)`: Marks a thread as daemon or user before starting it.
- `isDaemon()`: Checks whether a thread is a daemon thread.

### Key Notes:

- If you don't explicitly set a thread as daemon, it is a **user thread** by default.
- Always set `setDaemon(true)` **before starting** the thread; setting it afterward will throw an `IllegalThreadStateException`.

---

## 🔍 **Best Practices for Multithreading**

- **Minimize Synchronization:** Keep synchronized sections as small as possible.
- **Thread-safe Collections:** Prefer `ConcurrentHashMap`, `CopyOnWriteArrayList`, etc.
- **Avoid Deadlocks:** Be mindful of lock ordering.
- **Use Executors:** Instead of manually managing thread creation.
- **Interrupt-Friendly Code:** Ensure threads handle interruptions gracefully.
- **Use Higher-Level Concurrency Tools:** Utilize classes from `java.util.concurrent` package for better abstraction.
- **Leverage Atomic Variables:** Use `AtomicInteger`, `AtomicReference`, etc., for efficient lock-free thread-safe operations.
- **Apply `volatile` Judiciously:** Only for cases where atomicity is not a concern but visibility is essential.