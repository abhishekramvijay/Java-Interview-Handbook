# Core Java

> Core Java forms the foundation of almost every Java backend interview.

---

# Must Revise (★★★★★)

- OOP
- Strings
- Collections
- Exception Handling
- Multithreading
- JVM
- Serialization
- Java Memory Model

---

# Contents

1. Java Fundamentals
2. OOP
3. Strings
4. Collections
5. Exception Handling
6. Multithreading
7. JVM
8. Serialization
9. Java Memory Model
10. Reflection
11. Interview Coding Questions

---

# Java Fundamentals

(To be added)

---

# OOP

(To be added)

---

# Strings

(To be added)

---

# Collections

(To be added)

---

# Exception Handling

(To be added)

---

# Multithreading

(To be added)

---

# JVM

(To be added)

---

# Serialization

(To be added)

---

# Java Memory Model

(To be added)

---

# Reflection

(To be added)

---

# Interview Coding Questions

(To be added)









# Java Fundamentals

---

# JVM vs JRE vs JDK ★★★★★

## Interview Answer

- **JDK (Java Development Kit)** is used to develop Java applications. It contains the JRE along with development tools like `javac`, `javadoc`, and `jar`.
- **JRE (Java Runtime Environment)** is used to run Java applications. It contains the JVM and required libraries.
- **JVM (Java Virtual Machine)** is responsible for executing Java bytecode. It provides platform independence by converting bytecode into machine-specific instructions.

**Relationship**

```
JDK
 ├── JRE
 │    ├── JVM
 │    └── Java Libraries
 └── Development Tools
```

### Follow-up Questions

**Q. Why is Java platform independent?**

Because Java source code is compiled into platform-independent **bytecode**, which is executed by the JVM available for that operating system.

**Q. Does JVM make Java platform independent?**

Yes. Different operating systems have different JVM implementations, but all of them understand the same bytecode.

---

# Class vs Object ★★★★★

## Interview Answer

A **class** is a blueprint that defines the properties and behavior of an object.

An **object** is a runtime instance of a class.

Example

```java
class Employee {
    int id;
}

Employee e = new Employee();
```

Here,

- `Employee` → Class
- `e` → Object

---

# == vs equals() ★★★★★

## Interview Answer

- `==` compares references (or primitive values).
- `equals()` compares object contents. By default it behaves like `==`, but many classes such as `String` override it to compare values.

Example

```java
String s1 = new String("Java");
String s2 = new String("Java");

System.out.println(s1 == s2);      // false
System.out.println(s1.equals(s2)); // true
```

### Follow-up Questions

**Why should equals() and hashCode() be overridden together?**

If two objects are equal according to `equals()`, they must return the same hash code. Otherwise collections like `HashMap` and `HashSet` will behave incorrectly.

---

# Java is Pass by Value ★★★★★

## Interview Answer

Java is always **pass by value**.

- Primitive variables → value is copied.
- Object variables → the reference is copied (not the object).

Therefore, a method can modify the object's state but cannot make the caller's reference point to another object.

Example

```java
public void change(Employee e) {
    e.name = "John";      // Visible outside

    e = new Employee();   // Only local reference changes
}
```

---

# final vs finally vs finalize() ★★★★★

| final | finally | finalize() |
|--------|----------|------------|
| Keyword | Block | Method |
| Prevents inheritance, overriding or reassignment | Executes after try-catch | Invoked by GC before object collection (deprecated) |

### Interview Tip

`finalize()` is **deprecated** and should not be used for resource cleanup. Use **try-with-resources** or explicit cleanup methods instead.

---

# static ★★★★☆

## Interview Answer

`static` belongs to the class rather than an object.

- Static variable → shared by all objects.
- Static method → can be called without creating an object.
- Static block → executed once when the class is loaded.

Example

```java
class Employee {

    static int count = 0;

    Employee() {
        count++;
    }
}
```

---

# Access Modifiers ★★★★☆

| Modifier | Same Class | Same Package | Subclass | Other Package |
|-----------|------------|--------------|-----------|---------------|
| private | ✅ | ❌ | ❌ | ❌ |
| default | ✅ | ✅ | ❌ | ❌ |
| protected | ✅ | ✅ | ✅ | ❌* |
| public | ✅ | ✅ | ✅ | ✅ |

\* Accessible in another package only through inheritance.

---

# Wrapper Classes & Autoboxing ★★★★☆

## Interview Answer

Wrapper classes convert primitive types into objects.

Example

- `int → Integer`
- `char → Character`

Autoboxing

```java
Integer x = 10;
```

Unboxing

```java
int y = x;
```

Useful because Java Collections can store only objects.

---

# Frequently Asked Questions

1. JVM vs JRE vs JDK
2. Why is Java platform independent?
3. Does Java support pass by reference?
4. Difference between == and equals()?
5. Why override equals() and hashCode() together?
6. final vs finally vs finalize()
7. Can a constructor be final?
8. Can a static method be overridden?
9. Why are wrapper classes needed?
10. What is autoboxing and unboxing?


# OOP

---

# OOP Pillars ★★★★★

The four pillars of Object-Oriented Programming are:

- Encapsulation
- Abstraction
- Inheritance
- Polymorphism

---

# Encapsulation ★★★★★

## Interview Answer

Encapsulation is the process of bundling data and methods together while restricting direct access to the data using access modifiers. It helps achieve data hiding and protects object integrity.

Example

```java
class Employee {

    private int salary;

    public int getSalary() {
        return salary;
    }

    public void setSalary(int salary) {
        this.salary = salary;
    }
}
```

### Interview Tip

> Encapsulation answers **"How do we protect data?"**

---

# Abstraction ★★★★★

## Interview Answer

Abstraction hides implementation details and exposes only the required functionality to the user. It reduces complexity by showing **what** an object does rather than **how** it does it.

Example

```java
interface PaymentService {
    void pay();
}
```

### Real-world Example

ATM Machine

You know how to withdraw money.

You don't know how the bank processes it internally.

### Interview Tip

> Abstraction answers **"What does the object do?"**

---

# Encapsulation vs Abstraction ★★★★★

| Encapsulation | Abstraction |
|---------------|-------------|
| Hides data | Hides implementation |
| Achieved using private members | Achieved using interfaces & abstract classes |
| Focuses on security | Focuses on simplicity |

---

# Inheritance ★★★★★

## Interview Answer

Inheritance allows one class to acquire the properties and methods of another class, enabling code reuse and polymorphism.

Example

```java
class Animal {

    void eat() {}
}

class Dog extends Animal {

    void bark() {}
}
```

Relationship

```
Dog IS-A Animal
```

### Advantages

- Code reuse
- Extensibility
- Runtime polymorphism

### Disadvantages

- Tight coupling
- Fragile hierarchy if overused

---

# Polymorphism ★★★★★

## Interview Answer

Polymorphism means "one interface, many implementations."

It allows the same method call to behave differently based on the object.

There are two types:

- Compile-time (Method Overloading)
- Runtime (Method Overriding)

---

# Method Overloading ★★★★★

## Interview Answer

Methods have the same name but different parameter lists.

Resolved at compile time.

```java
class Calculator {

    int add(int a, int b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

---

# Method Overriding ★★★★★

## Interview Answer

A subclass provides its own implementation of a superclass method.

Resolved at runtime.

```java
class Animal {

    void sound() {
        System.out.println("Animal");
    }
}

class Dog extends Animal {

    @Override
    void sound() {
        System.out.println("Bark");
    }
}
```

---

# Overloading vs Overriding ★★★★★

| Overloading | Overriding |
|--------------|------------|
| Same class | Parent & Child |
| Different parameters | Same parameters |
| Compile-time | Runtime |
| Increases readability | Enables runtime polymorphism |

---

# Composition vs Inheritance ★★★★★

## Interview Answer

Inheritance represents an **IS-A** relationship.

Composition represents a **HAS-A** relationship.

Modern applications prefer **composition over inheritance** because it reduces coupling and improves flexibility.

Example

```java
class Engine {}

class Car {

    private Engine engine;
}
```

Relationship

```
Car HAS-A Engine
```

### Interview Tip

> Prefer Composition over Inheritance.

---

# Interface vs Abstract Class ★★★★★

| Interface | Abstract Class |
|------------|----------------|
| Defines contract | Defines partial implementation |
| Multiple inheritance supported | Single inheritance |
| No instance variables (except constants) | Can have instance variables |
| Used for capabilities | Used for common base implementation |

### When to use?

Interface

- Multiple implementations
- Loose coupling
- Strategy Pattern

Abstract Class

- Common code reuse
- Shared state
- Partial implementation

---

# this vs super ★★★★☆

| this | super |
|------|-------|
| Refers to current object | Refers to parent object |
| Access current members | Access parent members |
| Call current constructor | Call parent constructor |

---

# Object Class ★★★★☆

Frequently overridden methods

- equals()
- hashCode()
- toString()

Frequently used methods

- getClass()
- clone()
- wait()
- notify()
- notifyAll()

---

# SOLID Principles ★★★★☆

> Learn the definition and one example of each principle.

- S - Single Responsibility Principle
- O - Open Closed Principle
- L - Liskov Substitution Principle
- I - Interface Segregation Principle
- D - Dependency Inversion Principle

(Detailed explanation in LLD chapter.)

---

# Frequently Asked Questions

1. Difference between abstraction and encapsulation.
2. Difference between interface and abstract class.
3. Why is Java not purely object oriented?
4. Difference between overloading and overriding.
5. Can constructors be overridden?
6. Can constructors be final?
7. Why do we prefer composition over inheritance?
8. Difference between IS-A and HAS-A relationship.
9. What are SOLID principles?
10. Explain runtime polymorphism with an example.
