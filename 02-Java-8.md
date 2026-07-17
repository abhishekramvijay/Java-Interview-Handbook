# Java 8

> Java 8 is one of the biggest releases in Java history. It introduced functional programming concepts, Streams API, Lambda Expressions, Optional, and the modern Date-Time API.

---

# Must Revise (★★★★★)

- Lambda Expressions
- Functional Interfaces
- Method References
- Streams
- Intermediate vs Terminal Operations
- map() vs flatMap()
- Optional
- Collectors
- Parallel Streams
- Date & Time API

---

# Contents

1. Lambda Expressions
2. Functional Interfaces
3. Method References
4. Streams
5. Collectors
6. Optional
7. Parallel Streams
8. Date & Time API
9. Interface Enhancements
10. Frequently Asked Programs


# Lambda Expressions ★★★★★

## Interview Answer

Lambda Expression is a concise way to represent an anonymous function.

It allows passing behavior as a parameter and reduces boilerplate code.

Syntax

```java
(parameters) -> expression
```

Example

Before Java 8

```java
Runnable r = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello");
    }
};
```

Java 8

```java
Runnable r = () -> System.out.println("Hello");
```

---

## Advantages

- Less code
- Better readability
- Functional programming support
- Easy Stream operations

---

## Limitations

- Can access only final or effectively final local variables.
- Cannot modify captured local variables.

---

## Frequently Asked Questions

1. What is Lambda Expression?
2. Why local variables must be effectively final?
3. Can Lambda access instance variables?
4. Lambda vs Anonymous Class?


# Functional Interface ★★★★★

## Interview Answer

A Functional Interface contains exactly one abstract method.

It can have multiple default and static methods.

Annotated using

```java
@FunctionalInterface
```

Example

```java
@FunctionalInterface
interface Calculator {

    int add(int a, int b);
}
```

---

## Common Functional Interfaces

| Interface | Method | Purpose |
|------------|--------|----------|
| Predicate | test() | Returns boolean |
| Function | apply() | Converts one type to another |
| Consumer | accept() | Consumes input |
| Supplier | get() | Produces output |

---

## Frequently Asked Questions

1. What is Functional Interface?
2. Can it have default methods?
3. Why @FunctionalInterface?
4. Name common Functional Interfaces.


# Lambda vs Anonymous Class ★★★★☆

| Lambda | Anonymous Class |
|----------|-----------------|
| Less code | More boilerplate |
| No separate class | Creates anonymous class |
| this refers to enclosing class | this refers to anonymous object |
| Better performance | Slightly heavier |


# Method Reference ★★★★☆

## Interview Answer

Method Reference is a shorthand for Lambda Expression when an existing method can be reused.

Syntax

```java
ClassName::methodName
```

Example

Instead of

```java
list.forEach(s -> System.out.println(s));
```

Write

```java
list.forEach(System.out::println);
```

Types

- Static Method
- Instance Method
- Constructor Reference


# Interface Enhancements ★★★★☆

Java 8 introduced **default** and **static** methods in interfaces, allowing interfaces to evolve without breaking existing implementations.

---

# Default Methods ★★★★★

## Interview Answer

A default method provides a method implementation inside an interface.

It allows adding new methods to existing interfaces without breaking classes that already implement the interface.

Example

```java
interface Vehicle {

    default void start() {
        System.out.println("Vehicle Started");
    }
}
```

---

## Advantages

- Backward compatibility
- Code reuse
- Interface evolution

---

## Frequently Asked Questions

### Can default methods be overridden?

Yes.

### Can interfaces contain multiple default methods?

Yes.

### Can default methods access instance variables?

No. Interfaces cannot have instance variables.

---

# Diamond Problem ★★★★★

Suppose two interfaces contain the same default method.

```java
interface A {

    default void show() {
        System.out.println("A");
    }
}

interface B {

    default void show() {
        System.out.println("B");
    }
}

class Test implements A, B {

}
```

Compilation fails because Java cannot decide which implementation to use.

The implementing class must override the method.

```java
@Override
public void show() {

    A.super.show();
}
```

---

# Static Methods in Interface ★★★★☆

## Interview Answer

Java 8 allows static methods inside interfaces.

They belong to the interface and cannot be overridden.

Example

```java
interface MathUtil {

    static int add(int a, int b) {
        return a + b;
    }
}

MathUtil.add(10,20);
```

---

# Default vs Static Method ★★★★☆

| Default | Static |
|----------|---------|
| Can be overridden | Cannot be overridden |
| Called using object | Called using interface name |
| Supports polymorphism | Does not support polymorphism |

---

# Streams ★★★★★

## Interview Answer

A Stream is a sequence of elements supporting functional operations on data.

Streams do **not** store data.

They process data obtained from collections, arrays or other sources.

Example

```java
list.stream()
    .filter(s -> s.length() > 3)
    .forEach(System.out::println);
```

---

# Stream Pipeline ★★★★★

Every stream consists of three stages.

```
Source

↓

Intermediate Operations

↓

Terminal Operation
```

Example

```java
list.stream()
    .filter(...)
    .map(...)
    .collect(...);
```

---

# Creating Streams ★★★★★

From Collection

```java
list.stream();
```

From Array

```java
Arrays.stream(arr);
```

From Values

```java
Stream.of("A","B","C");
```

Infinite Stream

```java
Stream.iterate(1, n -> n + 1);
```

---

# Intermediate Operations ★★★★★

Intermediate operations are **lazy**.

They return another Stream.

Common operations

- filter()
- map()
- flatMap()
- sorted()
- distinct()
- limit()
- skip()
- peek()

---

# Terminal Operations ★★★★★

Terminal operations produce the final result.

Examples

- collect()
- forEach()
- count()
- reduce()
- findFirst()
- findAny()
- anyMatch()
- allMatch()
- noneMatch()
- min()
- max()

After a terminal operation, the stream cannot be reused.

```java
stream.forEach(System.out::println);

stream.count();      // IllegalStateException
```

---

# Lazy Evaluation ★★★★★

## Interview Answer

Intermediate operations are not executed immediately.

Execution begins only when a terminal operation is called.

Example

```java
list.stream()
    .filter(s -> s.length() > 3)
    .map(String::toUpperCase);
```

Nothing executes.

Only after

```java
.collect(...)
```

or

```java
.forEach(...)
```

does processing begin.

Advantages

- Better performance
- Pipeline optimization
- Short-circuit evaluation

---

# map() vs flatMap() ★★★★★

## map()

One input produces one output.

```java
List<String>

↓

List<Integer>
```

Example

```java
names.stream()
     .map(String::length)
```

---

## flatMap()

One input produces multiple outputs which are flattened into a single stream.

Example

```java
List<List<String>>

↓

List<String>
```

---

# filter() ★★★★★

Filters elements based on a condition.

```java
list.stream()
    .filter(x -> x > 10);
```

---

# distinct() ★★★★☆

Removes duplicate elements.

```java
list.stream()
    .distinct();
```

---

# sorted() ★★★★☆

Sorts stream elements.

```java
.sorted()
```

Custom sorting

```java
.sorted((a,b) -> b.compareTo(a))
```

---

# limit() vs skip() ★★★★☆

limit()

Returns first N elements.

skip()

Skips first N elements.

---

# peek() ★★★☆☆

Used mainly for debugging.

```java
.peek(System.out::println)
```

Should not be used for modifying data.

---

# findFirst() vs findAny() ★★★★☆

| findFirst() | findAny() |
|--------------|-----------|
| Returns first element | Returns any matching element |
| Ordered streams | Better for parallel streams |

---

# forEach() vs forEachOrdered() ★★★★☆

forEach()

Order not guaranteed in parallel streams.

forEachOrdered()

Maintains encounter order.

---

# reduce() ★★★★☆

Used to combine stream elements into a single result.

Example

```java
int sum = list.stream()
              .reduce(0, Integer::sum);
```

---

# Common Interview Questions

1. What is Stream?
2. Why are Streams lazy?
3. Intermediate vs Terminal Operations.
4. Why can't a stream be reused?
5. map() vs flatMap().
6. filter() vs map().
7. findFirst() vs findAny().
8. limit() vs skip().
9. forEach() vs forEachOrdered().
10. What is reduce()?
11. What is peek()?
12. Why are Streams better than loops?
13. Are Streams thread-safe?
14. Difference between Collection and Stream?
15. Can Streams modify the original collection?


# Collectors ★★★★★

## Interview Answer

Collectors are utility methods used with the `collect()` terminal operation to accumulate stream elements into collections, maps, strings, or summary results.

Example

```java
List<String> result = list.stream()
                          .filter(s -> s.length() > 3)
                          .collect(Collectors.toList());
```

---

# Common Collectors ★★★★★

## toList()

```java
List<String> list = stream.collect(Collectors.toList());
```

---

## toSet()

```java
Set<String> set = stream.collect(Collectors.toSet());
```

---

## toMap()

```java
Map<Integer, String> map = employees.stream()
        .collect(Collectors.toMap(Employee::getId,
                                  Employee::getName));
```

---

## joining()

```java
String result = names.stream()
        .collect(Collectors.joining(", "));
```

Output

```
Java, Spring, SQL
```

---

## counting()

```java
long count = list.stream()
        .collect(Collectors.counting());
```

---

## groupingBy() ★★★★★

Groups elements based on a key.

```java
Map<String, List<Employee>> map =
employees.stream()
.collect(Collectors.groupingBy(Employee::getDepartment));
```

One of the most frequently asked collectors.

---

## partitioningBy()

Groups into exactly two categories.

```java
Map<Boolean, List<Integer>> map =
numbers.stream()
.collect(Collectors.partitioningBy(n -> n % 2 == 0));
```

---

## mapping()

Applies transformation while grouping.

```java
Collectors.mapping(...)
```

---

## summarizingInt()

Returns

- Count
- Sum
- Average
- Min
- Max

```java
IntSummaryStatistics stats =
employees.stream()
.collect(Collectors.summarizingInt(Employee::getSalary));
```

---

# groupingBy() vs partitioningBy() ★★★★☆

| groupingBy() | partitioningBy() |
|--------------|------------------|
| Multiple groups | Only two groups |
| Any key | Boolean key |

---

# Optional ★★★★★

## Interview Answer

Optional is a container object that may or may not contain a value.

It helps avoid NullPointerException and encourages explicit handling of missing values.

---

## Creating Optional

```java
Optional<String> name =
Optional.of("Java");
```

```java
Optional<String> name =
Optional.ofNullable(value);
```

```java
Optional<String> empty =
Optional.empty();
```

---

# Common Methods

## isPresent()

```java
optional.isPresent();
```

---

## ifPresent()

```java
optional.ifPresent(System.out::println);
```

---

## get()

Returns value.

Throws exception if empty.

Avoid using directly.

---

## orElse() ★★★★★

```java
String name =
optional.orElse("Unknown");
```

Always evaluates the default value.

---

## orElseGet() ★★★★★

```java
String name =
optional.orElseGet(() -> fetchDefault());
```

Default supplier executes only when Optional is empty.

Preferred for expensive operations.

---

## orElseThrow()

```java
optional.orElseThrow(
        IllegalArgumentException::new);
```

---

# orElse() vs orElseGet() ★★★★★

| orElse() | orElseGet() |
|-----------|-------------|
| Always evaluates | Lazy evaluation |
| Suitable for simple values | Suitable for expensive computation |

One of the most frequently asked Java 8 interview questions.

---

# Parallel Streams ★★★★★

## Interview Answer

Parallel Streams process elements using multiple threads from the ForkJoinPool.

Enable by calling

```java
parallelStream()
```

or

```java
stream.parallel()
```

---

## Advantages

- Better CPU utilization
- Faster for large datasets
- Easy parallel programming

---

## Disadvantages

- Thread overhead
- Not suitable for small collections
- Order not guaranteed
- Shared mutable state causes issues

---

## When to Use?

Use

- Large datasets
- CPU intensive operations
- Independent computations

Avoid

- Database calls
- Network calls
- Small collections
- Ordered processing

---

# Sequential vs Parallel Stream ★★★★☆

| Sequential | Parallel |
|-------------|----------|
| Single thread | Multiple threads |
| Predictable order | Order not guaranteed |
| Lower overhead | Better for large datasets |

---

# Date & Time API ★★★★☆

Java 8 introduced the `java.time` package to replace the old `Date` and `Calendar` APIs.

Common Classes

- LocalDate
- LocalTime
- LocalDateTime
- Instant
- Duration
- Period

---

## LocalDate

```java
LocalDate.now();
```

---

## LocalTime

```java
LocalTime.now();
```

---

## LocalDateTime

```java
LocalDateTime.now();
```

---

## Duration

Difference between two times.

---

## Period

Difference between two dates.

---

# Common Java 8 Interview Programs

- Print odd numbers using Streams
- Find duplicate elements
- Count frequency of characters
- Find first non-repeating character
- Find second highest salary
- Group employees by department
- Convert List<List<T>> to List<T>
- Remove duplicates
- Sort using Streams
- Find max/min
- Sum using reduce()
- Join Strings
- Partition even/odd numbers

---

# Frequently Asked Questions

1. What are Collectors?
2. Explain groupingBy().
3. groupingBy() vs partitioningBy().
4. What is Optional?
5. Why Optional?
6. orElse() vs orElseGet().
7. Optional.of() vs ofNullable().
8. What are Parallel Streams?
9. When should Parallel Streams be avoided?
10. Sequential vs Parallel Streams.
11. What thread pool do Parallel Streams use?
12. What is ForkJoinPool?
13. What is the new Date & Time API?
14. Why was the old Date API replaced?

---

# Java 8 Quick Revision

### Lambda
- Anonymous function
- Functional programming
- Less boilerplate
- Effectively final variables

### Functional Interface
- One abstract method
- @FunctionalInterface
- Predicate
- Function
- Consumer
- Supplier

### Method Reference
- Class::method
- Cleaner than Lambda

### Streams
- Lazy evaluation
- Source → Intermediate → Terminal
- Cannot be reused
- Do not modify source

### Intermediate Operations
- filter()
- map()
- flatMap()
- sorted()
- distinct()
- limit()
- skip()
- peek()

### Terminal Operations
- collect()
- forEach()
- reduce()
- count()
- min()
- max()
- findFirst()
- findAny()

### Collectors
- toList()
- toSet()
- toMap()
- joining()
- groupingBy()
- partitioningBy()
- summarizingInt()

### Optional
- Avoid NullPointerException
- of()
- ofNullable()
- empty()
- orElse()
- orElseGet()
- orElseThrow()

### Parallel Streams
- ForkJoinPool
- Multiple threads
- Large datasets
- Avoid shared mutable state

### Date API
- LocalDate
- LocalTime
- LocalDateTime
- Duration
- Period

### Most Asked Interview Questions
- map() vs flatMap()
- Intermediate vs Terminal
- Lazy Evaluation
- Optional
- orElse() vs orElseGet()
- Parallel Streams
- groupingBy()
- findFirst() vs findAny()
- forEach() vs forEachOrdered()
- Functional Interfaces
