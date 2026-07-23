# Design Patterns

> Design patterns are proven, reusable solutions to recurring software design problems. They are not frameworks or libraries, but design templates that improve flexibility, maintainability, and extensibility. Senior interviews evaluate not only whether you know a pattern, but whether you can identify the right situation to apply it.

---

# Must Revise (★★★★★)

- Singleton
- Factory
- Builder
- Strategy
- Observer
- Decorator
- Adapter
- Template Method
- Command

---

# Contents

## Creational Patterns
1. Singleton
2. Factory Method
3. Abstract Factory
4. Builder
5. Prototype

## Structural Patterns
6. Adapter
7. Decorator
8. Facade
9. Proxy

## Behavioral Patterns
10. Strategy
11. Observer
12. Command
13. Template Method
14. Chain of Responsibility
15. State

---

# Pattern Categories

| Category | Purpose |
|----------|----------|
| Creational | Object Creation |
| Structural | Object Composition |
| Behavioral | Object Interaction |

---

# Singleton Pattern ★★★★★

## Intent

Ensure only one instance of a class exists.

## Interview Answer

Singleton restricts object creation to a single instance and provides a global access point.

## Problem

Creating multiple objects may lead to inconsistent state.

Examples

- Logger
- Configuration Manager
- Cache Manager

## Solution

- Private constructor
- Static instance
- Public getter

## Structure

```
Application

↓

Logger.getInstance()

↓

Logger
```

## When to Use

- Exactly one instance is required.
- Shared configuration.
- Shared cache.
- Logging.

## Avoid When

- Object maintains request-specific state.
- Independent instances are needed.
- Testability is important.

## Advantages

- Single instance
- Controlled access
- Reduced memory usage

## Disadvantages

- Hidden global state
- Harder to unit test
- Can become a bottleneck

## Production Insight

In Spring applications, Singleton is usually managed by the IoC container. Explicit Singleton implementations are rarely required.

## Interview Signals

Use when

- "Only one instance"
- "Shared object"
- "Global configuration"

---

# Factory Method Pattern ★★★★★

## Intent

Create objects without exposing creation logic.

## Interview Answer

Factory Method delegates object creation to a dedicated factory, allowing clients to work with abstractions.

## Problem

Client code directly creates concrete implementations.

```java
new CreditCardPayment();
```

Adding new payment methods requires modifying client code.

## Solution

```
PaymentFactory

↓

Payment

↓

CardPayment

UPIPayment

NetBankingPayment
```

## When to Use

- Multiple implementations.
- Creation logic is complex.
- Client should depend on interfaces.

## Avoid When

- Only one implementation exists.
- Object creation is trivial.

## Advantages

- Loose coupling
- Easy extensibility
- Better testing

## Disadvantages

- Additional classes
- Slightly higher complexity

## Production Insight

Spring's dependency injection often replaces explicit factory classes, but the underlying idea remains the same.

## Interview Signals

Use when

- Large if-else for object creation.
- Multiple implementations.
- Future extensibility.

---

# Abstract Factory ★★★★☆

## Intent

Create families of related objects.

Example

```
WindowsFactory

Button

Checkbox
```

```
MacFactory

Button

Checkbox
```

### Use When

Multiple related objects should be created together.

### Avoid When

Only one product hierarchy exists.

---

# Builder Pattern ★★★★★

## Intent

Construct complex objects step by step.

## Interview Answer

Builder separates object construction from its representation, making code readable and supporting immutable objects.

Example

Instead of

```java
new Employee(a,b,c,d,e,f,g);
```

Use

```java
Employee.builder()
        .name(...)
        .age(...)
        .salary(...)
        .build();
```

## When to Use

- Many optional fields.
- Immutable objects.
- Readability is important.

## Avoid When

Objects contain only a few mandatory fields.

## Advantages

- Readable
- Immutable
- Flexible

## Production Insight

Lombok's `@Builder` is widely used in Spring Boot projects to reduce boilerplate.

## Interview Signals

- Constructor has many parameters.
- Multiple optional fields.
- Fluent API required.

---

# Prototype Pattern ★★★☆☆

## Intent

Create objects by cloning existing ones.

### Use When

Object creation is expensive.

### Examples

- Game characters
- Document templates

---

# Adapter Pattern ★★★★☆

## Intent

Allow incompatible interfaces to work together.

## Problem

Two classes expose different interfaces.

## Solution

```
Client

↓

Adapter

↓

Third Party Library
```

## Real-world Example

Integrating a third-party payment gateway with your application's payment interface.

## Interview Signals

- Third-party integration.
- Legacy system integration.

---

# Decorator Pattern ★★★★☆

## Intent

Add functionality dynamically without modifying existing classes.

Example

```
Coffee

↓

MilkDecorator

↓

SugarDecorator
```

Each decorator adds new behavior.

## Use When

Behavior should be added dynamically.

## Avoid When

Only one variation exists.

## Production Insight

Spring Security filters and Java I/O streams are classic examples of the Decorator pattern.

---

# Facade Pattern ★★★☆☆

## Intent

Provide a simplified interface to a complex subsystem.

Example

```
TravelFacade

↓

Flight

Hotel

Payment
```

Client interacts only with the facade.

---

# Proxy Pattern ★★★☆☆

## Intent

Provide a placeholder or surrogate for another object.

Common Uses

- Lazy Loading
- Security
- Remote Access
- Caching

Example

Spring AOP proxies.

---

# Strategy Pattern ★★★★★

## Intent

Encapsulate interchangeable algorithms.

## Interview Answer

Strategy allows behavior to change at runtime by selecting different implementations of a common interface.

## Problem

Large if-else blocks.

```java
if(payment=="CARD")

else if(payment=="UPI")

else if(payment=="NETBANKING")
```

## Solution

```
PaymentStrategy

↓

CardPayment

UPIPayment

NetBankingPayment
```

## When to Use

- Runtime behavior changes.
- Multiple algorithms.
- Business rules vary.

## Avoid When

- Only one implementation exists.
- Behavior never changes.

## Advantages

- Open for extension.
- Removes conditional logic.
- Easy testing.

## Production Insight

Spring Boot commonly injects multiple implementations of an interface and selects the required strategy based on business logic.

## Interview Signals

- "Support multiple payment methods."
- "Different pricing algorithms."
- "Different discount rules."

---

# Observer Pattern ★★★★★

## Intent

Notify dependent objects when state changes.

## Example

```
Order Service

↓

Inventory

↓

Email

↓

SMS
```

Each observer reacts independently.

## Use When

One event triggers multiple independent actions.

## Avoid When

Only one consumer exists.

## Production Insight

Modern microservices often replace in-memory observers with Kafka or other message brokers for better scalability.

---

# Command Pattern ★★★★☆

## Intent

Encapsulate a request as an object.

Common Uses

- Undo
- Scheduling
- Queues
- Task execution

---

# Template Method Pattern ★★★★☆

## Intent

Define the overall algorithm while allowing subclasses to customize specific steps.

Example

```
Payment

↓

Validate()

↓

Process()

↓

GenerateReceipt()
```

Subclasses override only required steps.

---

# Chain of Responsibility ★★★☆☆

## Intent

Pass a request through multiple handlers until one processes it.

Example

```
Authentication

↓

Authorization

↓

Validation

↓

Business Logic
```

Common in web filters.

---

# State Pattern ★★★☆☆

## Intent

Allow an object to change behavior based on its internal state.

Example

```
Order

Created

↓

Paid

↓

Shipped

↓

Delivered
```

Removes complex state-based conditionals.

---

# Choosing the Right Pattern

| Situation | Pattern |
|-----------|----------|
| One instance | Singleton |
| Complex object creation | Builder |
| Object creation logic | Factory |
| Runtime behavior | Strategy |
| Event notification | Observer |
| Add functionality | Decorator |
| Third-party integration | Adapter |
| Simplify subsystem | Facade |
| Access control | Proxy |
| Request pipeline | Chain of Responsibility |
| Algorithm skeleton | Template Method |
| State transitions | State |

---

# Common Mistakes

- Using Singleton everywhere.
- Choosing inheritance instead of composition.
- Applying patterns for simple problems.
- Using Factory when direct construction is sufficient.
- Confusing Strategy with State.
- Confusing Decorator with Adapter.
- Over-engineering small applications.

---

# Frequently Asked Questions

1. Singleton vs Spring Singleton.
2. Factory vs Abstract Factory.
3. Builder vs Factory.
4. Strategy vs State.
5. Adapter vs Decorator.
6. Decorator vs Proxy.
7. Observer vs Pub/Sub.
8. Template Method vs Strategy.
9. When should design patterns be avoided?
10. Which design patterns are most frequently asked in Java interviews?

---

# Design Patterns Quick Revision

### Creational
- Singleton
- Factory
- Abstract Factory
- Builder
- Prototype

### Structural
- Adapter
- Decorator
- Facade
- Proxy

### Behavioral
- Strategy
- Observer
- Command
- Template Method
- Chain of Responsibility
- State

### Most Asked
- Singleton
- Factory
- Builder
- Strategy
- Observer
- Decorator

### Golden Rule

Don't apply a design pattern because you know it.

Apply it because the problem naturally requires it.
