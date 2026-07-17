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
