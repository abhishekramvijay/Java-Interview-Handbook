# High-Level Design (HLD)

> High-Level Design (HLD) focuses on designing scalable, reliable, maintainable, and fault-tolerant distributed systems. It answers *how the overall system architecture should be organized*. Senior backend interviews evaluate your ability to make sound architectural decisions and explain the trade-offs behind them.

---

# Must Revise (★★★★★)

- Scalability
- Availability
- Load Balancing
- Caching
- Database Scaling
- CAP Theorem
- Messaging
- Rate Limiting
- Microservices Communication
- Reliability Patterns

---

# Contents

1. HLD Fundamentals
2. Scalability
3. Availability
4. Load Balancing
5. Caching
6. Database Scaling
7. CAP Theorem
8. Messaging Systems
9. Reliability Patterns
10. Observability
11. Security Basics
12. HLD Interview Approach

---

# What is High-Level Design? ★★★★★

## Interview Answer

High-Level Design defines the overall architecture of a system, including services, databases, communication, scalability, and deployment.

It focuses on

- Components
- Service interactions
- Data flow
- Scalability
- Reliability

rather than implementation details.

---

# HLD vs LLD ★★★★★

| HLD | LLD |
|-----|-----|
| System Architecture | Class Design |
| Services | Objects |
| Databases | Data Models |
| Communication | Method Calls |
| Scalability | Maintainability |

---

# Functional vs Non-Functional Requirements ★★★★★

Before designing any system, separate requirements into two categories.

### Functional Requirements

Describe **what** the system should do.

Examples

- User Registration
- Search Products
- Book Tickets
- Send Notifications

### Non-Functional Requirements

Describe **how well** the system should perform.

Examples

- Scalability
- Availability
- Reliability
- Latency
- Security
- Throughput

Senior interviews spend significant time discussing non-functional requirements.

---

# Scalability ★★★★★

## Interview Answer

Scalability is the ability of a system to handle increasing load without significant performance degradation.

---

## Vertical Scaling

Increase resources of a single machine.

```
4 CPU

↓

16 CPU
```

### Advantages

- Simple
- No code changes

### Disadvantages

- Hardware limits
- Single point of failure

---

## Horizontal Scaling

Add more servers.

```
Users

↓

Load Balancer

↓

Server 1

Server 2

Server 3
```

### Advantages

- High availability
- Better fault tolerance
- Practically unlimited scaling

### Disadvantages

- More complex architecture
- Data consistency challenges

---

# Availability ★★★★★

## Interview Answer

Availability measures how often a system is operational and accessible.

Formula

```
Availability

=

Uptime

/

Total Time
```

Common targets

| Availability | Downtime / Year |
|--------------|-----------------|
| 99% | ~3.65 days |
| 99.9% | ~8.8 hours |
| 99.99% | ~52 minutes |
| 99.999% | ~5 minutes |

---

# Reliability vs Availability ★★★★★

| Reliability | Availability |
|-------------|--------------|
| Works correctly | Is accessible |
| Correct results | Can accept requests |

A system can be highly available but still return incorrect results.

---

# Stateless vs Stateful Services ★★★★★

## Stateless

Server stores no client session.

```
Client

↓

Load Balancer

↓

Any Server
```

Advantages

- Easy scaling
- Easy replacement
- Better load balancing

---

## Stateful

Server stores session information.

Requires session replication or sticky sessions.

---

# Load Balancer ★★★★★

## Interview Answer

A Load Balancer distributes incoming requests across multiple servers to improve scalability and availability.

---

## Architecture

```
          Clients
              │
              ▼
      +----------------+
      | Load Balancer  |
      +----------------+
       │      │      │
       ▼      ▼      ▼
    App1    App2    App3
```

---

## Algorithms

- Round Robin
- Least Connections
- Least Response Time
- IP Hash
- Weighted Round Robin

---

## Production Insight

Keep application servers stateless whenever possible. Stateless services allow the load balancer to route requests freely without relying on sticky sessions.

---

# Reverse Proxy vs Load Balancer ★★★★☆

| Reverse Proxy | Load Balancer |
|---------------|---------------|
| Routes requests | Distributes load |
| Often one backend | Usually multiple backends |
| SSL termination | Traffic distribution |

Examples

- Nginx
- HAProxy

can act as both.

---

# Caching ★★★★★

## Interview Answer

Caching stores frequently accessed data closer to the application to reduce latency and database load.

---

## Benefits

- Faster response time
- Reduced database load
- Lower infrastructure cost

---

## Cache-Aside Pattern

```
Application

↓

Cache

↓

Database
```

Flow

1. Check cache.
2. Cache miss.
3. Read database.
4. Update cache.
5. Return response.

Most common caching strategy.

---

## Write Through

```
Application

↓

Cache

↓

Database
```

Every write updates both cache and database.

---

## Write Back

```
Application

↓

Cache

↓

Database (Later)
```

Higher performance.

Risk of data loss.

---

## Cache Eviction

- LRU
- LFU
- FIFO
- TTL

---

# CDN ★★★★☆

Content Delivery Network caches static content close to users.

Ideal for

- Images
- CSS
- JavaScript
- Videos

Not used for dynamic database queries.

---

# Database Scaling ★★★★★

## Read Replicas

```
Primary

↓

Replica 1

Replica 2
```

Writes

↓

Primary

Reads

↓

Replicas

---

## Sharding

Split data across multiple databases.

Example

```
User A-M

↓

Shard 1

User N-Z

↓

Shard 2
```

Benefits

- Horizontal scaling
- Higher throughput

Challenges

- Cross-shard queries
- Rebalancing
- Transactions

---

# SQL vs NoSQL ★★★★★

| SQL | NoSQL |
|-----|--------|
| Structured | Flexible Schema |
| ACID | High Scalability |
| Joins | Denormalized |
| Strong Consistency | Often Eventual Consistency |

---

# CAP Theorem ★★★★★

## Interview Answer

In a distributed system, only two of the following three guarantees can be fully achieved during a network partition.

- Consistency
- Availability
- Partition Tolerance

---

## Trade-offs

| Choice | Prioritizes |
|---------|-------------|
| CP | Consistency |
| AP | Availability |

Partition tolerance is generally assumed in distributed systems.

---

# Messaging Systems ★★★★★

## Why Messaging?

Instead of direct communication,

```
Service A

↓

Service B
```

use

```
Service A

↓

Message Broker

↓

Service B
```

Benefits

- Loose coupling
- Retry
- Asynchronous processing
- Better scalability

---

## Queue vs Pub/Sub

| Queue | Pub/Sub |
|--------|---------|
| One consumer | Multiple consumers |
| Work distribution | Event broadcasting |

---

## Kafka vs RabbitMQ ★★★★☆

| Kafka | RabbitMQ |
|--------|-----------|
| High throughput | Low latency |
| Event Streaming | Task Queue |
| Durable Logs | Flexible Routing |

---

# Reliability Patterns ★★★★★

## Timeout

Prevent requests from waiting indefinitely.

---

## Retry

Retry transient failures.

Use exponential backoff.

---

## Circuit Breaker

Stops repeated requests to failing services.

```
Closed

↓

Open

↓

Half Open

↓

Closed
```

---

## Bulkhead

Isolate failures.

Example

Separate thread pools for

- Payments
- Notifications
- Search

---

## Idempotency

Repeated requests should not produce duplicate effects.

Example

Payment APIs.

---

# Observability ★★★★☆

Three pillars

- Metrics
- Logs
- Traces

---

## Metrics

Examples

- CPU
- Memory
- Request Rate
- Error Rate
- Latency

---

## Logs

Useful for debugging and auditing.

---

## Distributed Tracing

Tracks a request across multiple microservices.

Example

```
Gateway

↓

Order

↓

Payment

↓

Inventory
```

---

# Security Basics ★★★★☆

Frequently discussed topics

- HTTPS
- OAuth
- JWT
- API Keys
- Rate Limiting

Know where each fits; implementation details are usually covered in backend rounds.

---

# HLD Interview Approach ★★★★★

## Step 1

Clarify requirements.

---

## Step 2

Estimate scale.

Examples

- Daily Active Users
- QPS
- Storage
- Bandwidth

---

## Step 3

Design APIs.

---

## Step 4

Identify major components.

```
Client

↓

Gateway

↓

Services

↓

Database

↓

Cache

↓

Queue
```

---

## Step 5

Discuss bottlenecks.

- Database
- Network
- Cache
- Message Broker

---

## Step 6

Discuss trade-offs.

Every architectural decision has advantages and disadvantages.

---

# Common Mistakes

- Ignoring non-functional requirements.
- Jumping into components without estimating scale.
- Using microservices for every problem.
- Treating cache as the source of truth.
- Ignoring failure scenarios.
- Forgetting monitoring.
- Never discussing trade-offs.

---

# Frequently Asked Questions

1. Horizontal vs Vertical Scaling.
2. Stateless vs Stateful.
3. Load Balancer algorithms.
4. Cache-Aside vs Write Through.
5. SQL vs NoSQL.
6. Read Replica vs Sharding.
7. Kafka vs RabbitMQ.
8. CAP Theorem.
9. Circuit Breaker.
10. How do you approach an HLD interview?

---

# HLD Quick Revision

### Fundamentals
- Functional vs Non-Functional
- Scalability
- Availability
- Reliability

### Scaling
- Vertical
- Horizontal
- Stateless
- Stateful

### Performance
- Load Balancer
- Cache
- CDN

### Database
- SQL
- NoSQL
- Read Replica
- Sharding

### Messaging
- Queue
- Pub/Sub
- Kafka
- RabbitMQ

### Reliability
- Retry
- Timeout
- Circuit Breaker
- Bulkhead
- Idempotency

### Observability
- Metrics
- Logs
- Traces

### Interview Flow
- Requirements
- Scale Estimation
- APIs
- Components
- Bottlenecks
- Trade-offs
