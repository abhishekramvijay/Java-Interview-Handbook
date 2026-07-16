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
