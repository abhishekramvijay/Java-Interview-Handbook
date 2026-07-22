# Low-Level Design (LLD)

> Low-Level Design (LLD) focuses on designing classes, objects, relationships, and interactions within a system. It answers *how* a system should be implemented. Senior Java interviews evaluate not only your knowledge of design patterns but also your ability to write clean, extensible, maintainable, and object-oriented code.

---

# Must Revise (★★★★★)

- Object-Oriented Design
- SOLID Principles
- Class Relationships
- Composition vs Inheritance
- UML Class Diagrams
- Design Patterns
- LLD Interview Approach

---

# Contents

1. What is LLD?
2. Object-Oriented Design
3. SOLID Principles
4. Class Relationships
5. UML Basics
6. Design Patterns
7. LLD Interview Approach
8. Common Mistakes

---

# What is Low-Level Design? ★★★★★

## Interview Answer

Low-Level Design (LLD) focuses on designing classes, interfaces, objects, and their interactions to implement a software system.

It defines

- Classes
- Interfaces
- Relationships
- Methods
- Object interactions

LLD is implementation-oriented.

---

# HLD vs LLD ★★★★★

| High-Level Design | Low-Level Design |
|-------------------|------------------|
| System Architecture | Class Design |
| Components | Classes & Objects |
| Services | Methods |
| Database Selection | Data Models |
| Scalability | Maintainability |

---

# Object-Oriented Design (OOD)

Object-Oriented Design applies object-oriented principles to create software that is modular, reusable, extensible and easy to maintain.

Core concepts

- Encapsulation
- Abstraction
- Inheritance
- Polymorphism

These concepts should guide every design decision.

---

# SOLID Principles ★★★★★

SOLID consists of five design principles that improve maintainability and extensibility.

---

# S — Single Responsibility Principle (SRP)

## Interview Answer

A class should have only one reason to change.

Example

Instead of

```
EmployeeService

- Save Employee
- Generate PDF
- Send Email
```

Split into

```
EmployeeService

EmailService

ReportService
```

### Benefits

- Easier testing
- Better maintainability
- Smaller classes

### Interview Signals

Use when

- Class has multiple unrelated responsibilities.

Avoid

- Splitting classes too aggressively.

---

# O — Open Closed Principle (OCP)

## Interview Answer

Software entities should be open for extension but closed for modification.

Instead of modifying existing code,

extend it.

Example

Instead of

```java
if(type.equals("CARD")){

}

else if(type.equals("UPI")){

}
```

Create

```
PaymentStrategy

CreditCardPayment

UPIPayment
```

New payment methods require new implementations, not changes to existing code.

### Senior Engineer Perspective

OCP minimizes regression risk because existing, tested code remains unchanged when introducing new functionality.

---

# L — Liskov Substitution Principle (LSP)

## Interview Answer

Objects of a subclass should be replaceable with objects of the parent class without changing program correctness.

Bad Example

```
Bird

↓

Penguin
```

If Bird has

```
fly()
```

Penguin cannot correctly implement it.

This violates LSP.

### Solution

Separate flying birds from non-flying birds.

---

# I — Interface Segregation Principle (ISP)

## Interview Answer

Clients should not depend on methods they do not use.

Bad

```
Machine

print()

scan()

fax()
```

Printer must implement unnecessary methods.

Better

```
Printer

Scanner

FaxMachine
```

---

# D — Dependency Inversion Principle (DIP)

## Interview Answer

High-level modules should depend on abstractions instead of concrete implementations.

Instead of

```
OrderService

↓

MySQLRepository
```

Design

```
OrderService

↓

OrderRepository

↓

MySQLRepository

PostgresRepository
```

Dependency Injection is a common implementation of DIP.

---

# SOLID Quick Summary

| Principle | Meaning |
|-----------|----------|
| SRP | One Responsibility |
| OCP | Extend, Don't Modify |
| LSP | Child should replace Parent |
| ISP | Small Interfaces |
| DIP | Depend on Abstractions |

---

# Class Relationships ★★★★★

Understanding relationships is one of the most common LLD interview topics.

---

# Association

Objects know about each other.

Example

```
Teacher

↓

Student
```

Both can exist independently.

---

# Aggregation

Weak "Has-A" relationship.

Child can exist independently.

Example

```
Department

↓

Employee
```

Deleting Department does not delete Employee.

---

# Composition

Strong "Has-A" relationship.

Child cannot exist without parent.

Example

```
House

↓

Room
```

Deleting House removes its Rooms.

---

# Inheritance

Represents an "Is-A" relationship.

Example

```
Vehicle

↓

Car
```

Use only when inheritance truly models the domain.

---

# Composition vs Inheritance ★★★★★

| Composition | Inheritance |
|--------------|-------------|
| Has-A | Is-A |
| Flexible | Tightly Coupled |
| Preferred | Use carefully |

### Senior Engineer Perspective

Prefer composition over inheritance unless there is a clear "is-a" relationship. Composition leads to better flexibility, easier testing, and fewer inheritance-related issues.

---

# UML Class Diagram Basics ★★★★☆

Common symbols

```
+ public

- private

# protected
```

Relationship symbols

```
Inheritance

────────▷

Association

────────

Aggregation

◇───────

Composition

◆───────
```

Interviewers generally expect you to communicate relationships rather than draw perfect UML diagrams.

---

# Dependency Injection in LLD ★★★★★

Constructor Injection is the preferred approach.

Example

```
OrderService

↓

OrderRepository
```

Instead of creating dependencies directly,

inject them.

Benefits

- Loose coupling
- Easy unit testing
- Better extensibility

---

# Favor Composition Over Inheritance ★★★★★

Good

```
Car

↓

Engine
```

Instead of

```
Car extends Engine
```

Composition models ownership more accurately and avoids unnecessary coupling.

---

# LLD Interview Approach ★★★★★

A structured approach is often valued more than reaching the perfect design immediately.

### Step 1

Clarify requirements.

- Functional requirements
- Non-functional requirements
- Assumptions

---

### Step 2

Identify entities.

Example

```
Parking Lot

Vehicle

Parking Spot

Ticket

Gate
```

---

### Step 3

Identify relationships.

```
Has-A

Is-A

Uses-A
```

---

### Step 4

Identify responsibilities.

Each class should have a single responsibility.

---

### Step 5

Apply SOLID principles.

Avoid large God classes.

---

### Step 6

Introduce design patterns only when needed.

Do not force patterns into every solution.

---

### Step 7

Discuss extensibility.

Examples

- New Vehicle Type
- Multiple Payment Methods
- New Pricing Strategy

A good design should support these with minimal changes.

---

# Common Mistakes

- Creating God Classes.
- Using inheritance where composition is sufficient.
- Ignoring SOLID principles.
- Applying every design pattern unnecessarily.
- Tight coupling between classes.
- Exposing internal implementation details.
- Missing interfaces where multiple implementations are expected.

---

# Frequently Asked Questions

1. What is LLD?
2. HLD vs LLD.
3. Explain SOLID principles.
4. Composition vs Inheritance.
5. Association vs Aggregation vs Composition.
6. Why is Constructor Injection preferred?
7. What is Dependency Inversion?
8. What is Single Responsibility Principle?
9. How do you approach an LLD interview?
10. Why should design patterns not be overused?

---

# LLD Quick Revision

### Core Principles
- Encapsulation
- Abstraction
- Inheritance
- Polymorphism

### SOLID
- SRP
- OCP
- LSP
- ISP
- DIP

### Relationships
- Association
- Aggregation
- Composition
- Inheritance

### Best Practices
- Prefer Composition
- Constructor Injection
- Loose Coupling
- High Cohesion

### Interview Flow
- Requirements
- Entities
- Relationships
- Responsibilities
- SOLID
- Design Patterns
- Extensibility

### Most Asked Questions
- SOLID
- Composition vs Inheritance
- Aggregation vs Composition
- Dependency Injection
- LLD Approach
