# Spring Boot

> Spring Boot is built on top of the Spring Framework and simplifies application development by eliminating boilerplate configuration. It provides auto-configuration, embedded servers, starter dependencies, production-ready features, and opinionated defaults that enable rapid development of enterprise applications.

---

# Must Revise (★★★★★)

- Spring Boot
- Auto Configuration
- Starter Dependencies
- Embedded Server
- Spring Boot Annotations
- Configuration Properties
- Profiles
- Actuator
- Spring Boot Lifecycle
- Exception Handling

---

# Contents

1. Introduction
2. Spring vs Spring Boot
3. Auto Configuration
4. Starter Dependencies
5. Embedded Server
6. Configuration Files
7. Profiles
8. Spring Boot Annotations
9. Actuator
10. Exception Handling
11. Common Interview Questions

---

# What is Spring Boot? ★★★★★

## Interview Answer

Spring Boot is an extension of the Spring Framework that simplifies application development by providing auto-configuration, starter dependencies, embedded servers, and production-ready features.

It eliminates most XML configuration and significantly reduces boilerplate code.

---

# Advantages

- Rapid application development
- Minimal configuration
- Embedded web server
- Production-ready features
- Easy dependency management
- Opinionated defaults

---

# Spring vs Spring Boot ★★★★★

| Spring | Spring Boot |
|---------|-------------|
| Requires manual configuration | Auto configuration |
| External server required | Embedded server |
| XML/Java configuration | Minimal configuration |
| Dependency management is manual | Starter dependencies |
| More setup effort | Faster development |

---

# Auto Configuration ★★★★★

## Interview Answer

Auto Configuration automatically configures Spring Beans based on the dependencies available in the classpath.

For example,

If Spring Boot detects

```
spring-boot-starter-data-jpa
```

it automatically configures

- DataSource
- EntityManager
- Transaction Manager

without requiring manual configuration.

---

# How Auto Configuration Works

```
Application Starts

↓

@SpringBootApplication

↓

@EnableAutoConfiguration

↓

Reads Auto Configuration Classes

↓

Creates Required Beans
```

---

# Can Auto Configuration be Disabled?

Yes.

For a specific configuration

```java
@SpringBootApplication(
exclude = DataSourceAutoConfiguration.class
)
```

---

# Starter Dependencies ★★★★★

## Interview Answer

Starter dependencies are pre-configured dependency bundles that simplify Maven or Gradle configuration.

Examples

```
spring-boot-starter-web

spring-boot-starter-data-jpa

spring-boot-starter-security

spring-boot-starter-test

spring-boot-starter-validation
```

Instead of adding multiple individual dependencies, a single starter brings in all commonly required libraries.

---

# Embedded Server ★★★★★

Spring Boot packages an embedded web server within the application.

Supported servers

- Tomcat (Default)
- Jetty
- Undertow

Application starts using

```java
java -jar app.jar
```

without deploying to an external server.

---

# @SpringBootApplication ★★★★★

## Interview Answer

This is the primary annotation used to bootstrap a Spring Boot application.

It combines

```
@SpringBootConfiguration

+

@EnableAutoConfiguration

+

@ComponentScan
```

Example

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {

        SpringApplication.run(Application.class, args);

    }
}
```

---

# Configuration Files ★★★★★

Spring Boot supports

```
application.properties

application.yml
```

Both serve the same purpose.

YAML is generally preferred for hierarchical configuration.

Example

```yaml
server:
  port: 8080

spring:
  datasource:
    url: jdbc:mysql://localhost/test
```

---

# application.properties vs application.yml ★★★★☆

| application.properties | application.yml |
|-------------------------|-----------------|
| Key-value format | Hierarchical |
| More verbose | Cleaner for nested properties |

---

# Reading Properties ★★★★★

Using

```java
@Value("${server.port}")
```

Example

```java
@Value("${application.name}")
private String applicationName;
```

---

# @ConfigurationProperties ★★★★★

## Interview Answer

Used to bind multiple related configuration properties into a Java object.

Example

```yaml
app:

  name: Interview Handbook

  version: 1.0
```

```java
@ConfigurationProperties(prefix = "app")
public class AppProperties {

    private String name;

    private String version;

}
```

Preferred over multiple @Value annotations.

---

# Profiles ★★★★★

Profiles allow different configurations for different environments.

Examples

```
dev

test

stage

prod
```

Configuration files

```
application-dev.yml

application-test.yml

application-prod.yml
```

Activate profile

```properties
spring.profiles.active=dev
```

---

# Common Spring Boot Annotations ★★★★★

| Annotation | Purpose |
|------------|----------|
| @SpringBootApplication | Bootstraps application |
| @Configuration | Configuration class |
| @Bean | Creates Bean |
| @Value | Read property |
| @ConfigurationProperties | Bind configuration |
| @EnableScheduling | Scheduler support |
| @EnableCaching | Cache support |
| @EnableAsync | Async processing |

---

# CommandLineRunner ★★★☆☆

Runs immediately after application startup.

Example

```java
@Component
class StartupRunner
implements CommandLineRunner {

    @Override
    public void run(String... args){

    }
}
```

Useful for

- Initial data loading
- Cache warm-up
- Startup validation

---

# Spring Boot Actuator ★★★★★

## Interview Answer

Spring Boot Actuator provides production-ready endpoints to monitor and manage an application.

Common endpoints

```
/health

/info

/metrics

/env

/beans

/mappings

/loggers
```

---

# Why Actuator?

- Health Monitoring
- Metrics
- Application Information
- Environment Details
- Performance Monitoring

---

# Global Exception Handling ★★★★★

Spring Boot provides centralized exception handling using

```java
@RestControllerAdvice
```

and

```java
@ExceptionHandler
```

Example

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handle(Exception ex){

        return ResponseEntity
                .internalServerError()
                .body(ex.getMessage());

    }

}
```

Advantages

- Consistent API responses
- Reduced duplicate code
- Centralized exception management

---

# Bean Loading Order ★★★☆☆

Typical startup sequence

```
Application Starts

↓

ApplicationContext Created

↓

Beans Instantiated

↓

Dependency Injection

↓

@PostConstruct

↓

Application Ready
```

---

# Frequently Asked Questions

1. What is Spring Boot?
2. Spring vs Spring Boot.
3. What is Auto Configuration?
4. How does Auto Configuration work?
5. What are Starter Dependencies?
6. Why Embedded Server?
7. Explain @SpringBootApplication.
8. application.properties vs application.yml.
9. @Value vs @ConfigurationProperties.
10. What are Profiles?
11. What is Spring Boot Actuator?
12. What is CommandLineRunner?
13. How is Global Exception Handling implemented?
14. What happens during Spring Boot startup?

---

# Spring Boot Quick Revision

### Core Features
- Auto Configuration
- Embedded Server
- Starter Dependencies
- Opinionated Defaults

### Important Annotations
- @SpringBootApplication
- @Configuration
- @Bean
- @Value
- @ConfigurationProperties

### Configuration
- application.yml
- Profiles
- Environment-specific configuration

### Monitoring
- Actuator
- Health
- Metrics
- Info

### Exception Handling
- @RestControllerAdvice
- @ExceptionHandler

### Startup
- ApplicationContext
- Bean Creation
- Dependency Injection
- CommandLineRunner

### Most Asked Questions

- Spring vs Spring Boot
- Auto Configuration
- Starter Dependencies
- @SpringBootApplication
- @Value vs @ConfigurationProperties
- Profiles
- Actuator
- Global Exception Handling
