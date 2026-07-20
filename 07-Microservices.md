# Microservices

> Microservices is an architectural style where an application is built as a collection of small, independent services. Each service focuses on a specific business capability, owns its data, and communicates with other services using lightweight protocols such as REST, gRPC, or messaging systems.

---

# Must Revise (★★★★★)

- Microservices
- Monolith vs Microservices
- Service Discovery
- API Gateway
- Inter-Service Communication
- Synchronous vs Asynchronous Communication
- Circuit Breaker
- Retry
- Timeout
- Distributed Transactions
- Saga Pattern
- Idempotency
- Distributed Tracing

---

# Contents

1. Introduction
2. Monolith vs Microservices
3. Advantages & Challenges
4. Service Discovery
5. API Gateway
6. Communication Patterns
7. Fault Tolerance
8. Data Management
9. Distributed Transactions
10. Observability

---

# What are Microservices? ★★★★★

## Interview Answer

Microservices is an architectural style where an application is divided into multiple small, independently deployable services.

Each service

- Owns a specific business capability
- Has its own database
- Can be developed and deployed independently
- Communicates with other services through APIs or messaging systems

---

# Characteristics ★★★★★

- Independent deployment
- Loose coupling
- High cohesion
- Independent database
- Technology independence
- Fault isolation
- Scalability

---

# Monolith vs Microservices ★★★★★

| Monolith | Microservices |
|----------|---------------|
| Single application | Multiple services |
| Single deployment | Independent deployment |
| Shared database | Database per service |
| Difficult to scale | Scale individual services |
| One technology stack | Technology flexibility |
| Tightly coupled | Loosely coupled |

---

# Advantages ★★★★★

- Independent deployment
- Independent scaling
- Better fault isolation
- Faster development
- Easier maintenance
- Technology flexibility

---

# Challenges ★★★★★

- Distributed systems complexity
- Network latency
- Service discovery
- Monitoring
- Distributed transactions
- Data consistency
- Debugging
- Deployment complexity

---

# Database Per Service ★★★★★

## Interview Answer

Each microservice should own its database.

Other services should never directly access another service's database.

Instead, communication should happen through APIs or events.

Benefits

- Loose coupling
- Independent deployment
- Better scalability
- Clear ownership

---

# Service Discovery ★★★★★

## Interview Answer

In a dynamic environment, service instances frequently start, stop, or change addresses.

Service Discovery helps services locate each other without hardcoding IP addresses.

Popular tools

- Eureka
- Consul
- Kubernetes Service Discovery

---

# Client-Side vs Server-Side Discovery ★★★★☆

| Client Side | Server Side |
|--------------|-------------|
| Client chooses instance | Load balancer chooses instance |
| Eureka + Ribbon | Kubernetes, AWS ALB, Nginx |

---

# API Gateway ★★★★★

## Interview Answer

API Gateway acts as the single entry point for all client requests.

Responsibilities

- Routing
- Authentication
- Rate Limiting
- SSL Termination
- Request Logging
- Response Aggregation

Popular examples

- Spring Cloud Gateway
- Kong
- NGINX
- AWS API Gateway

---

# Why API Gateway?

Without Gateway

```
Client

↓

Order Service

↓

Payment Service

↓

Inventory Service

↓

Notification Service
```

Client needs to know every service.

---

With Gateway

```
Client

↓

API Gateway

↓

Microservices
```

Single endpoint.

Centralized security.

---

# Inter-Service Communication ★★★★★

Two common approaches

## Synchronous

- REST
- gRPC

Caller waits for response.

Suitable for immediate processing.

---

## Asynchronous

- Kafka
- RabbitMQ
- ActiveMQ

Producer publishes events.

Consumer processes later.

Suitable for loosely coupled systems.

---

# REST vs Messaging ★★★★★

| REST | Messaging |
|------|-----------|
| Request-Response | Event Driven |
| Immediate response | Eventually processed |
| Tightly coupled | Loosely coupled |
| Blocking | Non-blocking |

---

# Synchronous vs Asynchronous ★★★★★

| Synchronous | Asynchronous |
|--------------|--------------|
| Caller waits | Caller continues |
| Immediate result | Eventual consistency |
| Easier debugging | Better scalability |

---

# Fault Tolerance ★★★★★

Distributed systems must assume that remote services can fail.

Common techniques

- Retry
- Timeout
- Circuit Breaker
- Fallback
- Bulkhead

---

# Retry ★★★★★

Retries failed requests caused by temporary failures.

Use for

- Network glitches
- Temporary service failures

Avoid infinite retries.

Use exponential backoff.

---

# Timeout ★★★★★

Always configure request timeouts.

Without timeouts

- Threads remain blocked
- Resources get exhausted
- Cascading failures occur

---

# Circuit Breaker ★★★★★

## Interview Answer

Circuit Breaker prevents repeated calls to an unhealthy service.

States

### Closed

Requests pass normally.

---

### Open

Requests fail immediately.

No call reaches the remote service.

---

### Half-Open

Limited requests are allowed.

If successful

```
Closed
```

Otherwise

```
Open
```

Popular libraries

- Resilience4j
- Spring Cloud Circuit Breaker

---

# Fallback ★★★★☆

Provides an alternative response when a service fails.

Example

Return cached data instead of failing the request.

---

# Bulkhead Pattern ★★★☆☆

Isolates resources so that failure in one service does not impact others.

Example

Separate thread pools for different downstream services.

---

# Distributed Transactions ★★★★★

Traditional database transactions do not work across multiple microservices.

Instead, microservices use

- Saga Pattern
- Event-driven coordination
- Eventual Consistency

---

# Saga Pattern ★★★★★

## Interview Answer

Saga is a sequence of local transactions.

Each service completes its own transaction.

If a later step fails,

previous successful transactions are compensated.

Two approaches

- Choreography
- Orchestration

---

# Choreography vs Orchestration ★★★★☆

| Choreography | Orchestration |
|--------------|---------------|
| Event Driven | Central Coordinator |
| No central controller | Dedicated orchestrator |
| Simpler for small systems | Better for complex workflows |

---

# Eventual Consistency ★★★★★

Instead of immediate consistency,

all services become consistent over time through events.

Widely used in distributed systems.

---

# Idempotency ★★★★★

Operations should produce the same final result even if executed multiple times.

Important for

- Payment processing
- Order creation
- Retry mechanisms
- Message processing

Common approaches

- Unique Request ID
- Idempotency Key
- Database Constraints

---

# Distributed Tracing ★★★★☆

Tracks a request across multiple services.

Popular tools

- Zipkin
- Jaeger
- OpenTelemetry

Useful for

- Debugging
- Performance analysis
- Root cause analysis

---

# Centralized Logging ★★★★☆

Instead of checking logs on individual services,

logs are aggregated centrally.

Popular stack

- Elasticsearch
- Logstash
- Kibana (ELK)

---

# Health Checks ★★★★☆

Each service exposes health endpoints.

Example

```
/actuator/health
```

Used by

- Kubernetes
- Load Balancers
- Monitoring tools

---

# Frequently Asked Questions

1. What are Microservices?
2. Monolith vs Microservices.
3. Why database per service?
4. What is Service Discovery?
5. Why API Gateway?
6. REST vs Messaging.
7. Synchronous vs Asynchronous communication.
8. What is Circuit Breaker?
9. Retry vs Timeout.
10. What is Saga Pattern?
11. Choreography vs Orchestration.
12. What is Eventual Consistency?
13. Why Idempotency is important?
14. What is Distributed Tracing?
15. How do you monitor Microservices?

---

# Microservices Quick Revision

### Architecture
- Small independent services
- Database per service
- Independent deployment
- Independent scaling

### Communication
- REST
- gRPC
- Kafka
- RabbitMQ

### Infrastructure
- API Gateway
- Service Discovery
- Load Balancer

### Fault Tolerance
- Retry
- Timeout
- Circuit Breaker
- Fallback
- Bulkhead

### Data
- Saga Pattern
- Eventual Consistency
- Idempotency

### Monitoring
- Distributed Tracing
- Centralized Logging
- Health Checks

### Most Asked Questions
- Monolith vs Microservices
- API Gateway
- Service Discovery
- Circuit Breaker
- Retry vs Timeout
- Saga Pattern
- Choreography vs Orchestration
- Eventual Consistency
- Idempotency
