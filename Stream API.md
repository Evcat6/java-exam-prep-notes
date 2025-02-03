### 1. Introduction to Streams

Java Streams provide a functional approach to processing collections of data.

#### Key Features:

- **Declarative**: Focus on what to achieve rather than how.
- **Lazy Execution**: Operations are performed only when necessary.
- **Parallel Processing**: Enables efficient multi-threaded execution.

### 2. Creating Streams

Streams can be created from various sources:

#### From Collections:

```java
List<String> list = List.of("apple", "banana", "cherry");
Stream<String> stream = list.stream();
```

#### From Arrays:

```java
String[] array = {"a", "b", "c"};
Stream<String> stream = Arrays.stream(array);
```

#### From Values:

```java
Stream<String> stream = Stream.of("one", "two", "three");
```

#### From Files:

```java
Stream<String> lines = Files.lines(Paths.get("file.txt"));
```

### 3. Stream Operations

Stream operations are classified into **intermediate** and **terminal** operations.

#### **Intermediate Operations** (Lazy, return a Stream):

- `filter(Predicate<T>)` – Filters elements based on a condition.
- `map(Function<T, R>)` – Transforms elements.
- `flatMap(Function<T, Stream<R>>)` – Flattens nested structures.
- `distinct()` – Removes duplicate elements.
- `sorted()` – Sorts elements.
- `peek(Consumer<T>)` – Performs an action without modifying elements.

Example:

```java
list.stream()
    .filter(s -> s.startsWith("a"))
    .map(String::toUpperCase)
    .sorted()
    .forEach(System.out::println);
```

#### **Terminal Operations** (Trigger execution, return non-stream values):

- `collect(Collectors.toList())` – Collects results into a list.
- `forEach(Consumer<T>)` – Performs an action for each element.
- `count()` – Returns the count of elements.
- `reduce(BinaryOperator<T>)` – Reduces elements to a single result.
- `anyMatch(Predicate<T>)`, `allMatch(Predicate<T>)`, `noneMatch(Predicate<T>)` – Evaluate conditions.

Example:

```java
long count = list.stream().filter(s -> s.length() > 3).count();
```

### 4. Collecting Results

Streams can be collected into different structures using `Collectors`.

```java
List<String> collected = list.stream()
    .map(String::toUpperCase)
    .collect(Collectors.toList());
```

Using `groupingBy`:

```java
Map<Integer, List<String>> groupedByLength = list.stream()
    .collect(Collectors.groupingBy(String::length));
```

### 5. Parallel Streams

For large datasets, parallel streams can improve performance.

```java
list.parallelStream().forEach(System.out::println);
```

> **Note:** Parallel streams may not preserve order and should be used with caution for mutable data structures.

### 6. Handling Primitive Streams

Java provides specialized stream types for primitives: `IntStream`, `LongStream`, `DoubleStream`.

#### Generating a range of numbers:

```java
IntStream.range(1, 10).forEach(System.out::println);
```

#### Converting between streams:

```java
Stream<Integer> boxed = IntStream.range(1, 10).boxed();
```

### 7. Stream Short-Circuiting

Some operations can stop execution early:

- `limit(n)` – Limits the number of elements.
- `findFirst()`, `findAny()` – Retrieve an element early.

Example:

```java
Optional<String> first = list.stream().findFirst();
```

### 8. Common Stream Pitfalls

- **Streams are not reusable** – A stream is consumed once.
- **Avoid using stateful operations in parallel streams** – May lead to unexpected behavior.
- **Lazy execution may defer errors** – Debugging can be tricky.

By leveraging streams effectively, Java developers can write cleaner, more efficient, and more readable code!