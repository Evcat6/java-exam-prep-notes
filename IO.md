### 1. Introduction to Java I/O

Java provides various classes for input and output (I/O) operations using streams. Streams are used to read and write data in a continuous flow.

### 2. Types of Streams

- **Byte Streams** (`InputStream`, `OutputStream`): Used for reading/writing binary data.
- **Character Streams** (`Reader`, `Writer`): Used for reading/writing text data.
- **Buffered Streams** (`BufferedReader`, `BufferedWriter`): Improves efficiency by buffering data.
- **Data Streams** (`DataInputStream`, `DataOutputStream`): Used for reading/writing primitive data types.
- **Object Streams** (`ObjectInputStream`, `ObjectOutputStream`): Used for serializing and deserializing objects.

### 3. Byte Stream Example

```java
import java.io.*;

public class ByteStreamExample {
    public static void main(String[] args) {
        try (FileInputStream fis = new FileInputStream("input.txt");
             FileOutputStream fos = new FileOutputStream("output.txt")) {
            int data;
            while ((data = fis.read()) != -1) {
                fos.write(data);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 4. Character Stream Example

```java
import java.io.*;

public class CharacterStreamExample {
    public static void main(String[] args) {
        try (FileReader fr = new FileReader("input.txt");
             FileWriter fw = new FileWriter("output.txt")) {
            int data;
            while ((data = fr.read()) != -1) {
                fw.write(data);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 5. Buffered Streams

```java
import java.io.*;

public class BufferedStreamExample {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("input.txt"));
             BufferedWriter bw = new BufferedWriter(new FileWriter("output.txt"))) {
            String line;
            while ((line = br.readLine()) != null) {
                bw.write(line);
                bw.newLine();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 6. Object Serialization

```java
import java.io.*;

class Person implements Serializable {
    private static final long serialVersionUID = 1L;
    String name;
    int age;
    
    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

public class SerializationExample {
    public static void main(String[] args) {
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("person.ser"));
             ObjectInputStream ois = new ObjectInputStream(new FileInputStream("person.ser"))) {
            
            Person person = new Person("John", 30);
            oos.writeObject(person);
            
            Person deserializedPerson = (Person) ois.readObject();
            System.out.println("Name: " + deserializedPerson.name + ", Age: " + deserializedPerson.age);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

### 7. Summary

|Stream Type|Class Examples|Use Case|
|---|---|---|
|Byte Streams|`FileInputStream`, `FileOutputStream`|Read/write binary data|
|Character Streams|`FileReader`, `FileWriter`|Read/write text data|
|Buffered Streams|`BufferedReader`, `BufferedWriter`|Efficient text processing|
|Data Streams|`DataInputStream`, `DataOutputStream`|Read/write primitive types|
|Object Streams|`ObjectInputStream`, `ObjectOutputStream`|Serialization|

By understanding Java I/O, you can efficiently handle file operations, serialization, and data streaming in your applications.