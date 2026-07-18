# Spring Framework

> Spring is one of the most widely used Java frameworks for building enterprise applications. It provides Dependency Injection, Inversion of Control, Aspect-Oriented Programming, transaction management, and seamless integration with databases, messaging systems, and web frameworks.

---

# Must Revise (★★★★★)

- IoC
- Dependency Injection
- Spring Container
- Bean
- Bean Lifecycle
- Bean Scopes
- @Component
- @Service
- @Repository
- @Controller
- @Autowired
- @Qualifier
- @Primary
- Constructor Injection
- AOP
- Transactions

---

# Contents

1. IoC & Dependency Injection
2. Spring Container
3. Beans
4. Bean Scopes
5. Dependency Injection
6. Bean Annotations
7. Bean Lifecycle
8. Constructor vs Field Injection
9. AOP
10. Transactions

---

# Inversion of Control (IoC) ★★★★★

## Interview Answer

Inversion of Control means the responsibility of creating and managing objects is transferred from the application to the Spring Container.

Instead of using

```java
EmployeeService service = new EmployeeService();
```

Spring creates and manages the object.

### Advantages

- Loose Coupling
- Easier Testing
- Better Maintainability

---

# Dependency Injection (DI) ★★★★★

## Interview Answer

Dependency Injection is a design pattern where Spring injects the required dependencies into an object instead of the object creating them itself.

Example

Without DI

```java
EmployeeRepository repo =
        new EmployeeRepository();
```

With DI

```java
@Autowired
EmployeeRepository repo;
```

Advantages

- Loose coupling
- Better testing
- Easy maintenance

---

# IoC vs Dependency Injection ★★★★★

| IoC | Dependency Injection |
|------|----------------------|
| Design Principle | Design Pattern |
| Spring controls object creation | Spring injects dependencies |
| Achieved using DI | Implementation of IoC |

---

# Spring Container ★★★★★

## Interview Answer

The Spring Container is responsible for

- Creating Beans
- Managing Bean Lifecycle
- Injecting Dependencies
- Managing Scopes

Two implementations

- BeanFactory
- ApplicationContext

---

# BeanFactory vs ApplicationContext ★★★★☆

| BeanFactory | ApplicationContext |
|--------------|-------------------|
| Basic Container | Advanced Container |
| Lazy Initialization | Eager Initialization (Singletons) |
| Limited Features | Events, AOP, i18n, Validation |

ApplicationContext is used in almost all applications.

---

# Bean ★★★★★

## Interview Answer

A Bean is an object created, managed and maintained by the Spring Container.

Spring handles

- Creation
- Initialization
- Dependency Injection
- Destruction

---

# Bean Scopes ★★★★★

| Scope | Description |
|--------|-------------|
| singleton | One object per Spring Container |
| prototype | New object every request |
| request | One object per HTTP request |
| session | One object per HTTP session |
| application | One object per ServletContext |

Default scope

```
singleton
```

---

# Dependency Injection Types ★★★★★

## Constructor Injection

```java
@Service
class EmployeeService {

    private final EmployeeRepository repository;

    EmployeeService(EmployeeRepository repository) {
        this.repository = repository;
    }
}
```

---

## Setter Injection

```java
@Autowired
public void setRepository(EmployeeRepository repository){

}
```

---

## Field Injection

```java
@Autowired
private EmployeeRepository repository;
```

---

# Constructor vs Field Injection ★★★★★

| Constructor | Field |
|--------------|--------|
| Recommended | Not recommended |
| Immutable dependencies | Mutable |
| Easier Unit Testing | Difficult Testing |
| Dependency mandatory | Dependency optional |

### Why Constructor Injection?

- Easier testing
- Immutability
- Dependency visible
- Avoids NullPointerException

---

# @Autowired ★★★★★

## Interview Answer

@Autowired tells Spring to automatically inject a matching Bean.

Injection can happen through

- Constructor
- Setter
- Field

Spring first searches by type.

---

# @Qualifier ★★★★★

## Interview Answer

Used when multiple Beans of the same type exist.

Example

```java
@Autowired
@Qualifier("creditCard")
private PaymentService paymentService;
```

Without Qualifier

```
NoUniqueBeanDefinitionException
```

may occur.

---

# @Primary ★★★★☆

Marks a Bean as the default Bean when multiple Beans of the same type are available.

Example

```java
@Primary
@Component
class CreditCardPayment
implements PaymentService {

}
```

---

# Common Stereotype Annotations ★★★★★

## @Component

Generic Spring Bean.

---

## @Service

Business Layer.

---

## @Repository

Persistence Layer.

Also translates database exceptions into Spring exceptions.

---

## @Controller

MVC Controller returning Views.

---

## @RestController

REST API Controller.

Equivalent to

```
@Controller

+

@ResponseBody
```

---

# @Bean ★★★★★

## Interview Answer

@Bean tells Spring that the returned object should be managed as a Spring Bean.

Used inside

```java
@Configuration
```

Example

```java
@Bean
public ObjectMapper objectMapper(){

    return new ObjectMapper();
}
```

### When should @Bean be used?

- Third-party libraries
- External objects
- Custom Bean creation

---

# @Component vs @Bean ★★★★★

| @Component | @Bean |
|-------------|--------|
| Class Level | Method Level |
| Automatic Detection | Manual Bean Creation |
| Component Scanning | Configuration Class |

---

# Bean Lifecycle ★★★★☆

```
Bean Created

↓

Dependency Injection

↓

@PostConstruct

↓

Ready

↓

@PreDestroy

↓

Destroyed
```

---

# AOP (Aspect-Oriented Programming) ★★★★★

## Interview Answer

AOP separates cross-cutting concerns from business logic.

Common use cases

- Logging
- Security
- Transactions
- Auditing

---

## Common AOP Terms

Aspect

Cross-cutting logic.

Advice

Action performed.

Join Point

Point during execution.

Pointcut

Expression selecting Join Points.

---

# Transactions ★★★★★

## Interview Answer

Transactions ensure that a group of operations either complete successfully together or all rollback on failure.

Spring provides transaction management using

```java
@Transactional
```

---

# ACID Properties ★★★★★

- Atomicity
- Consistency
- Isolation
- Durability

---

# Propagation Modes ★★★☆☆

Most common

- REQUIRED (Default)
- REQUIRES_NEW
- SUPPORTS

---

# Isolation Levels ★★★☆☆

- READ_UNCOMMITTED
- READ_COMMITTED
- REPEATABLE_READ
- SERIALIZABLE

---

# Frequently Asked Questions

1. What is IoC?
2. What is Dependency Injection?
3. IoC vs DI.
4. BeanFactory vs ApplicationContext.
5. What is a Spring Bean?
6. Constructor vs Field Injection.
7. Why Constructor Injection is preferred?
8. What is @Autowired?
9. @Qualifier vs @Primary.
10. @Component vs @Bean.
11. @Service vs @Repository.
12. What is Bean Lifecycle?
13. What is AOP?
14. What is @Transactional?
15. Explain ACID properties.

---

# Spring Quick Revision

### IoC
- Spring creates objects
- Loose coupling

### DI
- Spring injects dependencies
- Constructor preferred

### Container
- BeanFactory
- ApplicationContext

### Bean
- Managed by Spring
- Default scope Singleton

### Scopes
- Singleton
- Prototype
- Request
- Session

### Injection
- Constructor ✅
- Setter
- Field ❌

### Important Annotations
- @Component
- @Service
- @Repository
- @Controller
- @RestController
- @Bean
- @Autowired
- @Qualifier
- @Primary

### AOP
- Logging
- Security
- Transactions

### Transactions
- @Transactional
- ACID
- Rollback
- Propagation
- Isolation

### Most Asked Questions
- IoC vs DI
- Constructor vs Field Injection
- @Component vs @Bean
- @Qualifier vs @Primary
- Bean Lifecycle
- AOP
- Transactions
