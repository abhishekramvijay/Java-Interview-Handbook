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
---
---

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

# Strings

---

# Why String is Immutable ★★★★★

## Interview Answer

A String is immutable because once created, its value cannot be changed. Any modification creates a new String object.

Immutability provides:

- Security
- Thread safety
- String Pool
- Cached hashCode()
- Safe HashMap keys

### Follow-up Questions

**Why String is used as HashMap key?**

Because its hashCode never changes after creation.

**How is String made immutable?**

- Class is final
- Internal value is private
- No setter methods
- Modification methods return a new String

---

# String Pool ★★★★★

## Interview Answer

The String Pool is a special memory area inside the heap that stores string literals. If the same literal already exists, Java reuses the existing object instead of creating a new one.

Example

```java
String s1 = "Java";
String s2 = "Java";

System.out.println(s1 == s2);   // true
```

---

# String vs StringBuilder vs StringBuffer ★★★★★

| String | StringBuilder | StringBuffer |
|---------|---------------|--------------|
| Immutable | Mutable | Mutable |
| Thread Safe | No | Yes |
| Performance | Slow for modifications | Fast | Slower than Builder |

### When to use?

- String → Read-only data
- StringBuilder → Single-threaded modifications
- StringBuffer → Multi-threaded modifications

---

# == vs equals() ★★★★★

## Interview Answer

- `==` compares references.
- `equals()` compares object contents.

```java
String s1 = new String("Java");
String s2 = new String("Java");

System.out.println(s1 == s2);       // false
System.out.println(s1.equals(s2));  // true
```

---

# StringBuilder ★★★★★

## Interview Answer

StringBuilder is a mutable sequence of characters.

Preferred when repeatedly modifying strings because it avoids creating multiple String objects.

Example

```java
StringBuilder sb = new StringBuilder();

sb.append("Java");
sb.append("8");
```

---

# StringBuffer ★★★★☆

## Interview Answer

StringBuffer is similar to StringBuilder but all methods are synchronized, making it thread-safe.

Use it only when multiple threads modify the same object.

---

# intern() ★★★★☆

## Interview Answer

The `intern()` method moves (or returns) the String from the String Pool.

```java
String s1 = new String("Java");

String s2 = s1.intern();
```

Now

```java
s2 == "Java"
```

returns

```java
true
```

---

# Common String Interview Programs ★★★★★

- Reverse String
- Reverse Words
- Check Palindrome
- Count Vowels
- Count Frequency
- First Non-Repeating Character
- Most Frequent Character
- Anagram
- Longest Common Prefix
- Longest Common Subsequence
- Longest Repeating Substring

---

# Frequently Asked Questions

1. Why is String immutable?
2. Explain String Pool.
3. String vs StringBuilder vs StringBuffer.
4. == vs equals().
5. What is intern()?
6. Why is String final?
7. Why is String used as HashMap key?
8. Can String be mutable?
9. How does String concatenation work?
10. Which is faster: StringBuilder or StringBuffer?


# Collections Framework

> The Java Collections Framework provides data structures and algorithms to store, retrieve, and manipulate groups of objects efficiently.

---

# Collections Hierarchy ★★★★★

```
                Iterable
                    │
               Collection
          ┌────────┼────────┐
         List      Set     Queue
          │         │         │
 ArrayList     HashSet   PriorityQueue
 LinkedList    TreeSet
 Vector        LinkedHashSet

                 Map
                  │
        HashMap  TreeMap
        Hashtable
        LinkedHashMap
        ConcurrentHashMap
```

---

# ArrayList vs LinkedList ★★★★★

| ArrayList | LinkedList |
|------------|------------|
| Dynamic Array | Doubly Linked List |
| Fast Random Access O(1) | Random Access O(n) |
| Insert/Delete Middle O(n) | Insert/Delete O(1) (if node known) |
| Less Memory | More Memory |

## Interview Answer

Use **ArrayList** when reads are frequent.

Use **LinkedList** when insertions/deletions are frequent.

> In most enterprise applications, ArrayList is preferred.

---

# HashMap ★★★★★

## Interview Answer

HashMap stores key-value pairs using hashing.

Average lookup complexity is **O(1)**.

Internally it uses an array of buckets.

Collisions are handled using

- Linked List (Java 7)
- Red Black Tree (Java 8+) when bucket size exceeds threshold.

---

## Internal Working

```
put(key,value)

↓

hashCode()

↓

bucket index

↓

bucket empty?

↓

Yes → Insert

↓

No

↓

equals()

↓

Update

OR

Collision

↓

Linked List / Tree
```

---

## Important Facts

Default Capacity

```
16
```

Default Load Factor

```
0.75
```

Resize

```
16

↓

12 elements

↓

Resize to 32
```

Treeify Threshold

```
8
```

Untreeify Threshold

```
6
```

Minimum Capacity for Treeification

```
64
```

---

## Follow-up Questions

- Why override equals() and hashCode() together?
- What happens during resize?
- Why Tree after Java 8?
- Can mutable objects be used as keys?
- Why one null key?

---

# HashMap vs Hashtable vs ConcurrentHashMap ★★★★★

| HashMap | Hashtable | ConcurrentHashMap |
|-----------|-----------|-------------------|
| Not Thread Safe | Thread Safe | Thread Safe |
| Allows one null key | No null | No null |
| Allows null values | No null | No null |
| Faster | Slower | Better concurrency |
| No synchronization | Entire table synchronized | Fine-grained locking |

---

# ConcurrentHashMap ★★★★★

## Interview Answer

ConcurrentHashMap is a thread-safe implementation of Map.

It uses fine-grained synchronization to allow high concurrency.

Unlike Hashtable, it does not lock the entire map during writes.

---

## Why no null?

Because during concurrent access, a null return value becomes ambiguous.

```
map.get(key)

↓

null

↓

Does key not exist?

OR

Value is null?
```

Impossible to distinguish.

Hence null keys and values are prohibited.

---

# HashSet ★★★★★

## Interview Answer

HashSet stores unique elements.

Internally backed by HashMap.

Insertion, deletion and search are O(1).

---

# TreeSet ★★★★☆

## Interview Answer

TreeSet stores unique elements in sorted order.

Internally backed by TreeMap.

Complexity

```
O(log n)
```

---

# LinkedHashSet ★★★☆☆

Maintains insertion order.

Internally backed by LinkedHashMap.

---

# TreeMap ★★★★★

## Interview Answer

TreeMap stores key-value pairs in sorted order of keys.

Internally implemented using Red Black Tree.

Complexity

```
O(log n)
```

---

# TreeMap vs HashMap ★★★★★

| HashMap | TreeMap |
|-----------|---------|
| Unordered | Sorted |
| O(1) | O(log n) |
| Hash Table | Red Black Tree |
| One null key | No null key |

---

# LinkedHashMap ★★★★☆

Maintains insertion order.

Can also maintain access order.

Useful for implementing

```
LRU Cache
```

---

# WeakHashMap ★★☆☆☆

Uses Weak References for keys.

Entries are automatically removed when keys are garbage collected.

Mostly used for caches.

---

# IdentityHashMap ★★☆☆☆

Uses

```
==
```

instead of

```
equals()
```

for key comparison.

Rarely used.

---

# PriorityQueue ★★★★★

Default implementation of Min Heap.

```
peek()

O(1)

offer()

O(log n)

poll()

O(log n)
```

Common Interview Questions

- Top K Frequent Elements
- Merge K Sorted Lists
- Kth Largest Element

---

# ConcurrentModificationException ★★★★★

Occurs when a fail-fast collection is structurally modified while iterating.

Wrong

```java
for(String s : list){
    list.remove(s);
}
```

Correct

```java
Iterator<String> itr = list.iterator();

while(itr.hasNext()){

    if(...){

        itr.remove();
    }
}
```

---

# CopyOnWriteArrayList ★★★★☆

Creates a new copy of the array on every write.

Advantages

- Safe iteration
- No ConcurrentModificationException

Disadvantages

- Expensive writes
- High memory usage

Suitable for

```
Many Reads

Few Writes
```

---

# Frequently Asked Questions

1. Explain HashMap internals.
2. Difference between HashMap and ConcurrentHashMap.
3. Why ConcurrentHashMap doesn't allow null?
4. Difference between TreeMap and HashMap.
5. Difference between HashSet and TreeSet.
6. Difference between ArrayList and LinkedList.
7. What is ConcurrentModificationException?
8. What is CopyOnWriteArrayList?
9. How does HashMap resize?
10. What is treeification?
11. Can mutable objects be used as HashMap keys?
12. Why override equals() and hashCode() together?
13. Which collection would you use for LRU Cache?
14. Which collection maintains insertion order?
15. Which collection maintains sorted order?


# Exception Handling

---

# Exception Hierarchy ★★★★★

```
                 Throwable
                /         \
           Error       Exception
                           |
                 RuntimeException
```

- **Error** → Serious JVM issues (OutOfMemoryError, StackOverflowError).
- **Checked Exception** → Checked at compile time.
- **Unchecked Exception** → Occur at runtime.

---

# Checked vs Unchecked Exception ★★★★★

| Checked Exception | Unchecked Exception |
|-------------------|---------------------|
| Checked at compile time | Occurs at runtime |
| Must be handled or declared | Handling is optional |
| Extends Exception | Extends RuntimeException |

Examples

Checked

```java
IOException
SQLException
FileNotFoundException
```

Unchecked

```java
NullPointerException
ArithmeticException
ArrayIndexOutOfBoundsException
IllegalArgumentException
```

---

# throw vs throws ★★★★★

| throw | throws |
|--------|---------|
| Used to explicitly throw an exception | Declares exceptions that a method may throw |
| Inside method | In method signature |

Example

```java
public void validate(int age) {

    if(age < 18)
        throw new IllegalArgumentException();
}
```

```java
public void readFile() throws IOException {

}
```

---

# try-catch-finally ★★★★★

## Interview Answer

- **try** → Contains code that may throw an exception.
- **catch** → Handles the exception.
- **finally** → Executes regardless of whether an exception occurs.

Example

```java
try {

}
catch(Exception e){

}
finally{

}
```

---

# Can finally not execute? ★★★★☆

Yes.

Cases:

- JVM crashes
- System.exit()
- Power failure

---

# try-with-resources ★★★★★

## Interview Answer

Introduced in Java 7.

Automatically closes resources implementing **AutoCloseable**.

Example

```java
try(BufferedReader br =
        new BufferedReader(new FileReader("a.txt"))) {

}
```

Preferred over manually closing resources.

---

# Custom Exception ★★★★☆

Create by extending

Checked

```java
Exception
```

Unchecked

```java
RuntimeException
```

Example

```java
class InvalidAgeException
        extends RuntimeException {

    public InvalidAgeException(String message) {
        super(message);
    }
}
```

---

# Multiple catch blocks ★★★★☆

Always write

Specific

↓

Generic

Example

```java
catch(FileNotFoundException e){

}
catch(IOException e){

}
catch(Exception e){

}
```

---

# Exception Propagation ★★★★☆

Unchecked exceptions automatically propagate up the call stack until handled.

```
Method A

↓

Method B

↓

Method C

↓

Exception

↓

Caller
```

---

# Common Runtime Exceptions ★★★★★

- NullPointerException
- ArithmeticException
- NumberFormatException
- IllegalArgumentException
- IllegalStateException
- ClassCastException
- IndexOutOfBoundsException

---

# Frequently Asked Questions

1. Difference between checked and unchecked exceptions.
2. Difference between throw and throws.
3. Can finally block not execute?
4. Why use try-with-resources?
5. How do you create a custom exception?
6. Difference between Exception and Error.
7. Can we have multiple catch blocks?
8. What is exception propagation?


# Multithreading & Concurrency

---

# Process vs Thread ★★★★★

| Process | Thread |
|----------|--------|
| Independent program | Smallest unit of execution |
| Own memory | Shares process memory |
| Heavyweight | Lightweight |
| Communication is expensive | Communication is fast |

Example

```
Chrome

    Process

        ↓

Tabs

    Threads
```

---

# Creating Threads ★★★★★

There are two common ways.

### Implement Runnable (Preferred)

```java
class MyTask implements Runnable {

    public void run() {

    }
}

Thread t = new Thread(new MyTask());
t.start();
```

### Extend Thread

```java
class MyThread extends Thread {

    public void run() {

    }
}
```

### Which one should be preferred?

Implement **Runnable** because Java supports single inheritance.

---

# Thread Lifecycle ★★★★★

```
NEW

↓

RUNNABLE

↓

RUNNING

↓

BLOCKED / WAITING / TIMED_WAITING

↓

TERMINATED
```

---

# synchronized ★★★★★

## Interview Answer

`synchronized` allows only one thread to execute a critical section at a time by acquiring an object's monitor lock.

It helps prevent race conditions and ensures thread safety.

Example

```java
public synchronized void withdraw() {

}
```

or

```java
synchronized(lock){

}
```

### Method vs Block

Method

Entire method is locked.

Block

Only critical section is locked.

> Prefer synchronized block because it reduces lock contention.

---

# wait() vs sleep() ★★★★★

| wait() | sleep() |
|----------|----------|
| Object class | Thread class |
| Releases lock | Does not release lock |
| Used for thread communication | Used for delay |
| Must be inside synchronized | Can be called anywhere |

---

# notify() vs notifyAll() ★★★★☆

notify()

Wakes one waiting thread.

notifyAll()

Wakes all waiting threads.

> In Producer-Consumer, prefer notifyAll().

---

# volatile ★★★★★

## Interview Answer

volatile guarantees **visibility**.

Whenever one thread updates a volatile variable, all other threads read the updated value from main memory.

It **does not** provide atomicity.

Suitable for

- Status flag
- Stop signal

Not suitable for

```
count++
```

---

# AtomicInteger ★★★★★

## Interview Answer

AtomicInteger performs atomic operations using CAS (Compare-And-Swap) without using synchronized.

Example

```java
AtomicInteger count = new AtomicInteger();

count.incrementAndGet();
```

Use when a single variable is modified by multiple threads.

---

# synchronized vs AtomicInteger ★★★★★

| synchronized | AtomicInteger |
|---------------|---------------|
| Locks thread | Lock-free |
| Can protect multiple variables | Single variable only |
| Slower | Faster |

---

# ReentrantLock ★★★★★

## Interview Answer

ReentrantLock provides explicit locking with additional features over synchronized.

Advantages

- tryLock()
- lockInterruptibly()
- Fair locking
- Multiple Conditions

Always remember

```java
lock.lock();

try{

}
finally{

    lock.unlock();
}
```

---

# synchronized vs ReentrantLock ★★★★★

| synchronized | ReentrantLock |
|---------------|---------------|
| Automatic unlock | Manual unlock |
| Simple | More flexible |
| No tryLock | Supports tryLock |
| No fairness | Supports fairness |

---

# ExecutorService ★★★★★

## Interview Answer

ExecutorService manages a pool of reusable threads.

Instead of creating new threads every time, tasks are submitted to the thread pool.

Example

```java
ExecutorService service =
        Executors.newFixedThreadPool(5);

service.submit(task);

service.shutdown();
```

Advantages

- Thread reuse
- Better performance
- Controlled concurrency

---

# Callable vs Runnable ★★★★☆

| Runnable | Callable |
|-----------|----------|
| No return value | Returns value |
| Cannot throw checked exception | Can throw checked exception |

---

# Future ★★★★☆

Represents the result of an asynchronous task.

```
submit()

↓

Future

↓

get()
```

---

# CompletableFuture ★★★★☆

Improves asynchronous programming.

Supports

- Chaining
- Combining tasks
- Non-blocking execution

---

# Deadlock ★★★★★

## Interview Answer

Deadlock occurs when two or more threads wait indefinitely for each other's locks.

Conditions

- Mutual exclusion
- Hold and wait
- No preemption
- Circular wait

Avoid using

- Consistent lock ordering
- tryLock()
- Timeout

---

# Starvation ★★★☆☆

A thread never gets CPU because higher priority threads keep executing.

---

# Livelock ★★★☆☆

Threads keep responding to each other but make no progress.

---

# Producer Consumer ★★★★★

Producer

Produces data.

Consumer

Consumes data.

Implemented using

- wait()
- notifyAll()
- BlockingQueue

---

# BlockingQueue ★★★★★

Thread-safe queue.

Producer waits when queue is full.

Consumer waits when queue is empty.

Implementations

- ArrayBlockingQueue
- LinkedBlockingQueue

---

# Thread-safe Collections ★★★★★

- ConcurrentHashMap
- CopyOnWriteArrayList
- BlockingQueue
- ConcurrentLinkedQueue

---

# Thread Dump ★★★★★

## Interview Answer

Thread dump is a snapshot of all threads in the JVM at a particular point in time.

Useful for

- Deadlock analysis
- Hung application
- High CPU
- Blocked threads

---

# Common Interview Questions

1. synchronized vs ReentrantLock.
2. wait() vs sleep().
3. volatile vs AtomicInteger.
4. Why volatile doesn't provide atomicity?
5. ExecutorService.
6. Producer Consumer.
7. Thread dump.
8. Deadlock.
9. Callable vs Runnable.
10. Future vs CompletableFuture.
11. notify vs notifyAll.
12. Thread lifecycle.
13. How does AtomicInteger work?
14. Explain CAS.
15. What happens if unlock() is forgotten?
