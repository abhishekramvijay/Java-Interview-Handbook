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


