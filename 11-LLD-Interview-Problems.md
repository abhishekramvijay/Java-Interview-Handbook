# LLD Interview Problems

> This section focuses on how Low-Level Design interviews are actually conducted. The goal is not to memorize complete solutions, but to develop a structured approach that can be applied to any design problem.

---

# Must Revise (★★★★★)

- Requirement Clarification
- Entity Identification
- Class Relationships
- SOLID Principles
- Design Patterns
- Extensibility
- Trade-offs

---

# LLD Interview Framework ★★★★★

Follow the same approach for every design problem.

## Step 1 — Clarify Requirements

Never start coding immediately.

Ask questions like

- What are the functional requirements?
- What are the non-functional requirements?
- Are there any constraints?
- What assumptions can we make?

Interviewers often evaluate the quality of your questions before your design.

---

## Step 2 — Identify Entities

Identify the primary objects in the system.

Example

Parking Lot

```
ParkingLot
ParkingSpot
Vehicle
Ticket
Gate
Payment
```

---

## Step 3 — Define Relationships

Determine how entities are related.

```
Is-A

Has-A

Uses-A
```

Prefer composition over inheritance whenever possible.

---

## Step 4 — Define Responsibilities

Each class should have a clear responsibility.

Bad

```
ParkingLot

Book Spot

Calculate Price

Generate Ticket

Make Payment

Send Receipt
```

Good

```
ParkingLot

↓

SpotManager

↓

PricingStrategy

↓

TicketService

↓

PaymentService
```

---

## Step 5 — Apply SOLID

Ask yourself

- Is every class doing one job?
- Can new functionality be added without modifying existing classes?
- Are interfaces small?
- Are dependencies abstract?

---

## Step 6 — Introduce Design Patterns

Only when they naturally fit.

Examples

| Requirement | Pattern |
|-------------|----------|
| Multiple payment methods | Strategy |
| Object creation | Factory |
| Notifications | Observer |
| Optional features | Decorator |
| Complex object creation | Builder |

---

## Step 7 — Discuss Extensibility

Interviewers almost always ask

"What happens if requirements change?"

Examples

- New vehicle type
- New payment gateway
- Dynamic pricing
- VIP parking
- Reservation support

Explain how your design accommodates these changes.

---

# Problem 1 — Parking Lot ★★★★★

## Typical Requirements

- Multiple floors
- Multiple spot types
- Entry & Exit gates
- Ticket generation
- Parking fee calculation
- Multiple payment methods

---

## Core Entities

```
ParkingLot

Floor

ParkingSpot

Vehicle

Ticket

Gate

Payment
```

---

## Relationships

```
ParkingLot

◆── Floor

Floor

◆── ParkingSpot

Vehicle

── Ticket

Ticket

── Payment
```

---

## Recommended Design Patterns

| Requirement | Pattern |
|-------------|----------|
| Vehicle creation | Factory |
| Pricing | Strategy |
| Payment | Strategy |
| Notifications | Observer |

---

## Common Follow-up Questions

- How would you support electric vehicle charging?
- How would you reserve parking spots?
- How would you support hourly and daily pricing?
- How would you prevent double booking?

---

# Problem 2 — Splitwise ★★★★★

## Requirements

- Users
- Groups
- Expenses
- Equal Split
- Percentage Split
- Exact Split

---

## Core Entities

```
User

Expense

Group

Split

BalanceSheet
```

---

## Design Patterns

| Requirement | Pattern |
|-------------|----------|
| Split calculation | Strategy |
| Expense creation | Factory |

---

## Common Follow-up Questions

- Add settlement reminders.
- Support multiple currencies.
- Track expense history.
- Simplify debt graph.

---

# Problem 3 — Elevator System ★★★★☆

## Requirements

- Multiple elevators
- External requests
- Internal requests
- Scheduling algorithm

---

## Core Entities

```
Elevator

Floor

Button

Display

Request

Scheduler
```

---

## Design Patterns

| Requirement | Pattern |
|-------------|----------|
| Scheduling algorithm | Strategy |
| Elevator states | State |

---

## Follow-up Questions

- Minimize waiting time.
- Handle maintenance mode.
- Fire emergency mode.
- VIP elevators.

---

# Problem 4 — Library Management ★★★★☆

## Requirements

- Books
- Members
- Borrow
- Return
- Fine Calculation

---

## Core Entities

```
Library

Book

Member

Loan

Fine

Catalog
```

---

## Design Patterns

| Requirement | Pattern |
|-------------|----------|
| Fine calculation | Strategy |
| Notifications | Observer |

---

# Problem 5 — Movie Ticket Booking ★★★★☆

## Requirements

- Movies
- Shows
- Seats
- Booking
- Payment

---

## Core Entities

```
Movie

Show

Seat

Booking

Payment

User
```

---

## Follow-up Questions

- Prevent double booking.
- Seat locking.
- Payment timeout.
- Booking cancellation.

---

# Problem 6 — ATM Machine ★★★★☆

## Requirements

- Authenticate customer
- Withdraw cash
- Deposit cash
- Balance inquiry
- PIN validation

---

## Core Entities

```
ATM

Card

Account

Transaction

CashDispenser

Bank
```

---

## Design Patterns

| Requirement | Pattern |
|-------------|----------|
| ATM state | State |
| Transactions | Command |

---

# Problem 7 — Snake & Ladder ★★★☆☆

## Core Entities

```
Game

Player

Board

Snake

Ladder

Dice
```

---

## Design Patterns

| Requirement | Pattern |
|-------------|----------|
| Dice | Strategy (optional) |
| Game states | State |

---

# Problem 8 — Tic Tac Toe ★★★☆☆

## Core Entities

```
Board

Cell

Player

Game
```

---

## Follow-up Questions

- NxN board.
- AI player.
- Undo support.
- Online multiplayer.

---

# What Interviewers Actually Evaluate ★★★★★

Most interviewers are **not** looking for a perfect design.

They evaluate whether you can

- Clarify ambiguous requirements.
- Identify the right entities.
- Define clean responsibilities.
- Apply SOLID principles.
- Choose appropriate design patterns.
- Design for future extensibility.
- Communicate your thought process clearly.

A clean, well-reasoned design is usually preferred over an overly complex one.

---

# Common Mistakes

- Jumping into code without clarifying requirements.
- Creating God classes.
- Using inheritance everywhere.
- Applying every design pattern.
- Ignoring extensibility.
- Forgetting edge cases.
- Spending too much time on syntax instead of design.

---

# Frequently Asked Questions

1. How do you start an LLD interview?
2. How many classes should be created?
3. When should design patterns be introduced?
4. How do you identify entities?
5. How much UML is expected?
6. How do you discuss scalability in LLD?
7. How do you justify design decisions?
8. What if requirements change midway?

---

# LLD Final Revision

### Interview Flow

Requirements

↓

Entities

↓

Relationships

↓

Responsibilities

↓

SOLID

↓

Design Patterns

↓

Extensibility

---

### Most Used Patterns

- Strategy
- Factory
- Builder
- Observer
- State
- Command

---

### Most Asked Problems

- Parking Lot
- Splitwise
- Elevator
- Library
- Movie Ticket Booking
- ATM

---

### Golden Rules

- Clarify before designing.
- Keep classes cohesive.
- Prefer composition over inheritance.
- Apply patterns only when needed.
- Design for change, not for today's requirements.
- Explain trade-offs throughout the interview.
