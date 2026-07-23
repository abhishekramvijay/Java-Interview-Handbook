# HLD Interview Case Studies

> This section focuses on solving real High-Level Design interview problems. The objective is to learn a repeatable design process, understand architectural trade-offs, and communicate decisions clearly. Most interviewers evaluate your reasoning more than the final architecture.

---

# Must Revise (★★★★★)

- Requirement Gathering
- Capacity Estimation
- API Design
- Data Model
- Scalability
- Bottleneck Analysis
- Trade-offs

---

# HLD Interview Framework ★★★★★

Follow this framework for every HLD interview.

```
Requirements
      ↓
Capacity Estimation
      ↓
API Design
      ↓
High-Level Components
      ↓
Database Design
      ↓
Scaling
      ↓
Bottlenecks
      ↓
Trade-offs
```

---

# Step 1 – Clarify Requirements ★★★★★

Never start drawing architecture immediately.

Ask

- Who are the users?
- Core features?
- Read-heavy or write-heavy?
- Consistency requirements?
- Latency requirements?
- Expected traffic?

---

# Step 2 – Capacity Estimation ★★★★★

Interviewers usually expect rough calculations.

Estimate

- Daily Active Users (DAU)
- Requests Per Second (QPS)
- Storage
- Peak Traffic
- Network Bandwidth

Approximation is acceptable.

Example

```
10 Million Users

↓

1 Million Daily Users

↓

10 Requests/User

↓

10 Million Requests/Day

↓

≈115 Requests/Second
```

Always mention

"These are rough estimates used to guide architectural decisions."

---

# Step 3 – API Design ★★★★☆

Example

```
POST /users

POST /orders

GET /orders/{id}

DELETE /orders/{id}
```

Keep APIs

- RESTful
- Idempotent where appropriate
- Versioned if needed

---

# Step 4 – High-Level Components ★★★★★

Typical architecture

```
                Client
                   │
                   ▼
            API Gateway
                   │
        ┌──────────┼──────────┐
        ▼          ▼          ▼
   User Service Order Service Payment Service
        │          │          │
        └──────┬───┴──────┬───┘
               ▼          ▼
            Cache      Database
               │
               ▼
          Message Broker
```

---

# Step 5 – Database Design ★★★★★

Identify

- Entities
- Relationships
- Indexes
- Partitioning
- Replication

Avoid over-designing the schema.

---

# Step 6 – Scaling Strategy ★★★★★

Discuss

- Stateless services
- Load balancing
- Read replicas
- Sharding
- Caching
- Asynchronous processing

---

# Step 7 – Failure Handling ★★★★★

Interviewers expect failure scenarios.

Discuss

- Retry
- Timeout
- Circuit Breaker
- Dead Letter Queue
- Monitoring

---

# Problem 1 – TinyURL ★★★★★

## Requirements

- Generate short URLs
- Redirect quickly
- Highly available
- Billions of URLs

---

## High-Level Design

```
Client
   │
   ▼
API Gateway
   │
   ▼
URL Service
   │
   ├────────► Cache
   │
   ▼
Database
```

---

## Important Decisions

- Unique ID generation
- Base62 encoding
- Cache hot URLs
- Read-heavy optimization

---

## Common Follow-up Questions

- Custom aliases
- URL expiration
- Analytics
- Spam detection

---

# Problem 2 – Rate Limiter ★★★★★

## Requirements

- Prevent abuse
- Per-user limits
- Distributed environment

---

## Architecture

```
Client

↓

Gateway

↓

Redis

↓

Service
```

---

## Popular Algorithms

- Token Bucket
- Leaky Bucket
- Fixed Window
- Sliding Window

---

## Trade-offs

Token Bucket

✔ Burst traffic

✔ Flexible

Sliding Window

✔ More accurate

✘ Slightly expensive

---

# Problem 3 – Notification System ★★★★★

## Requirements

Support

- Email
- SMS
- Push Notifications

---

## Architecture

```
Client

↓

Notification API

↓

Kafka

↓

Email Worker

SMS Worker

Push Worker
```

---

## Benefits

- Loose coupling
- Retry support
- Independent scaling

---

## Follow-up Questions

- Retry failures
- User preferences
- Notification priority
- Scheduled notifications

---

# Problem 4 – Chat System ★★★★☆

## Requirements

- One-to-one messaging
- Online status
- Message history
- Read receipts

---

## Architecture

```
Client

↓

WebSocket Gateway

↓

Chat Service

↓

Message Queue

↓

Database
```

---

## Scaling Considerations

- Persistent WebSocket connections
- Horizontal scaling
- Distributed session management

---

# Problem 5 – Food Delivery ★★★★☆

## Requirements

- Search restaurants
- Place order
- Payment
- Delivery tracking

---

## Services

```
Restaurant

Order

Payment

Delivery

Notification
```

---

## Interview Discussion

Focus on

- Order state
- Delivery assignment
- Location updates

---

# Problem 6 – Ride Sharing ★★★★☆

## Requirements

- Driver matching
- Live location
- Trip lifecycle
- Payments

---

## Components

```
Location Service

Driver Service

Ride Service

Payment Service

Notification Service
```

---

## Important Topics

- Geo-spatial indexing
- Driver matching
- Real-time updates

---

# Problem 7 – Hotel Booking ★★★★★

## Requirements

- Search hotels
- Check availability
- Reserve room
- Payment
- Cancellation

---

## Architecture

```
Client

↓

Search Service

↓

Booking Service

↓

Inventory Service

↓

Payment Service
```

---

## Major Challenges

- Prevent double booking
- Inventory consistency
- Payment failures
- Cancellation handling

---

## Trade-offs

Use

- Optimistic locking
- Idempotency
- Event-driven notifications

---

# Choosing Components ★★★★★

| Requirement | Recommended Component |
|------------|-----------------------|
| Fast reads | Redis Cache |
| Async work | Kafka / RabbitMQ |
| File storage | Object Storage |
| Search | Elasticsearch |
| Analytics | Kafka |
| CDN | Static Content |

---

# Bottlenecks ★★★★★

Common bottlenecks

- Database
- Cache
- Network
- Message Broker
- External APIs

Always discuss mitigation strategies.

---

# What Interviewers Evaluate ★★★★★

A good HLD interview is not about drawing the biggest architecture.

Interviewers evaluate

- Requirement clarification
- Prioritization
- Communication
- Architectural reasoning
- Trade-off analysis
- Failure handling
- Extensibility

---

# Common Mistakes

- Jumping into architecture without understanding requirements.
- Ignoring scale estimation.
- Adding unnecessary microservices.
- Ignoring cache invalidation.
- Assuming databases never fail.
- Never discussing monitoring.
- Ignoring cost and operational complexity.

---

# Frequently Asked Questions

1. How do you estimate QPS?
2. When should Redis be introduced?
3. Read Replica vs Sharding.
4. Kafka vs RabbitMQ.
5. How do you avoid single points of failure?
6. How do you prevent duplicate requests?
7. When should you use eventual consistency?
8. How do you handle service failures?
9. What should be cached?
10. How do you justify architectural trade-offs?

---

# HLD Final Revision

### Interview Flow

Requirements

↓

Capacity Estimation

↓

API Design

↓

Architecture

↓

Database

↓

Scaling

↓

Failure Handling

↓

Trade-offs

---

### Most Asked Systems

- TinyURL
- Rate Limiter
- Notification System
- Chat System
- Hotel Booking
- Food Delivery
- Ride Sharing

---

### Golden Rules

- Clarify before designing.
- Estimate before scaling.
- Keep services stateless.
- Cache wisely.
- Design for failures.
- Explain every trade-off.
- Optimize only after identifying bottlenecks.
