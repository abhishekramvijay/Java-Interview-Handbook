# SQL

> SQL (Structured Query Language) is the standard language for interacting with relational databases. For backend engineers, SQL is essential for designing schemas, retrieving data efficiently, optimizing queries, and maintaining data consistency. Senior interviews focus not only on writing queries but also on understanding performance implications.

---

# Must Revise (★★★★★)

- Joins
- Group By
- Having
- Order By
- Window Functions
- CTE
- Indexes
- Normalization
- ACID
- Transactions
- Isolation Levels
- Optimistic vs Pessimistic Locking

---

# Contents

1. SQL Basics
2. Joins
3. Group By & Having
4. Subqueries
5. Window Functions
6. CTE
7. Indexes
8. Transactions
9. Locking
10. Normalization

---

# What is SQL? ★★★★★

## Interview Answer

SQL (Structured Query Language) is used to create, retrieve, update and manage data stored in relational databases.

Common operations are categorized as

- DDL
- DML
- DQL
- DCL
- TCL

---

# SQL Categories ★★★★★

| Category | Purpose | Examples |
|----------|---------|----------|
| DDL | Database Structure | CREATE, ALTER, DROP, TRUNCATE |
| DML | Modify Data | INSERT, UPDATE, DELETE |
| DQL | Retrieve Data | SELECT |
| DCL | Access Control | GRANT, REVOKE |
| TCL | Transaction Control | COMMIT, ROLLBACK, SAVEPOINT |

---

# WHERE vs HAVING ★★★★★

| WHERE | HAVING |
|--------|---------|
| Filters rows | Filters groups |
| Executes before GROUP BY | Executes after GROUP BY |
| Cannot use aggregate functions | Can use aggregate functions |

Example

```sql
SELECT department, COUNT(*)
FROM Employee
GROUP BY department
HAVING COUNT(*) > 5;
```

---

# GROUP BY ★★★★★

Groups rows having the same value.

Example

```sql
SELECT department,
       COUNT(*)
FROM Employee
GROUP BY department;
```

---

# ORDER BY ★★★★☆

Sorts the result.

```sql
ORDER BY salary DESC;
```

Default order

```
ASC
```

---

# LIMIT / FETCH FIRST ★★★☆☆

Used to limit returned rows.

MySQL

```sql
LIMIT 10;
```

Oracle

```sql
FETCH FIRST 10 ROWS ONLY;
```

---

# SQL Joins ★★★★★

## INNER JOIN

Returns matching rows.

```sql
SELECT *
FROM Employee e
INNER JOIN Department d
ON e.dept_id = d.id;
```

---

## LEFT JOIN

Returns all rows from left table and matching rows from right.

---

## RIGHT JOIN

Returns all rows from right table and matching rows from left.

---

## FULL OUTER JOIN

Returns all matching and non-matching rows.

(Not supported directly in MySQL.)

---

## CROSS JOIN

Cartesian Product.

Every row joins with every row.

---

# JOIN Comparison ★★★★★

| Join | Returns |
|------|----------|
| INNER | Matching rows |
| LEFT | All left + matching right |
| RIGHT | All right + matching left |
| FULL | All rows |
| CROSS | Cartesian product |

---

# Subquery ★★★★★

## Interview Answer

A subquery is a query written inside another SQL query.

Example

```sql
SELECT *
FROM Employee
WHERE salary >

(
SELECT AVG(salary)
FROM Employee
);
```

---

# Correlated Subquery ★★★★☆

Executed once for every row of the outer query.

Generally slower than normal subqueries.

---

# Window Functions ★★★★★

## Interview Answer

Window functions perform calculations across a set of rows without collapsing them into a single row.

Common functions

- ROW_NUMBER()
- RANK()
- DENSE_RANK()
- LEAD()
- LAG()

---

# ROW_NUMBER()

Assigns unique sequence numbers.

```sql
SELECT name,
ROW_NUMBER() OVER
(ORDER BY salary DESC)
FROM Employee;
```

---

# RANK()

Equal values receive the same rank.

Ranks are skipped.

```
100

100

90

Ranks

1

1

3
```

---

# DENSE_RANK()

Equal values receive the same rank.

No gaps.

```
100

100

90

Ranks

1

1

2
```

---

# ROW_NUMBER vs RANK vs DENSE_RANK ★★★★★

| ROW_NUMBER | RANK | DENSE_RANK |
|-------------|------|------------|
| Unique numbers | Skips rank | No gaps |

---

# Common Interview Query

Find the 2nd highest salary.

```sql
SELECT salary
FROM

(
SELECT salary,
DENSE_RANK() OVER
(ORDER BY salary DESC) r
FROM Employee
)t

WHERE r = 2;
```

---

# LEAD() and LAG() ★★★★☆

Used to access next or previous row.

Example

```sql
LAG(salary)
OVER(ORDER BY id)
```

---

# Common Table Expression (CTE) ★★★★☆

## Interview Answer

A CTE is a temporary named result set that improves readability and simplifies complex queries.

Example

```sql
WITH HighSalary AS (

SELECT *
FROM Employee
WHERE salary > 100000

)

SELECT *
FROM HighSalary;
```

---

# Index ★★★★★

## Interview Answer

An index is a database structure that improves query performance by reducing the amount of data scanned.

Trade-off

- Faster reads
- Slower inserts and updates
- Additional storage

---

# Types of Indexes

- Primary Index
- Unique Index
- Composite Index
- Clustered Index*
- Non-Clustered Index*

*Database support varies by vendor.

---

# When Should You Create an Index?

- Frequently searched columns
- JOIN columns
- ORDER BY columns
- GROUP BY columns

Avoid indexing

- Small tables
- Frequently updated columns
- Low-cardinality columns (e.g., boolean flags)

---

# Senior Engineer Perspective

Indexes improve read performance but increase write overhead because every INSERT, UPDATE, and DELETE must also update the index.

Adding indexes indiscriminately can slow down write-heavy applications and increase storage usage.

Always create indexes based on query patterns, not assumptions.

---

# Transactions ★★★★★

## Interview Answer

A transaction is a sequence of operations executed as a single unit of work.

Either all operations succeed or all are rolled back.

---

# ACID Properties ★★★★★

| Property | Meaning |
|----------|---------|
| Atomicity | All or nothing |
| Consistency | Valid state before and after transaction |
| Isolation | Concurrent transactions do not interfere |
| Durability | Committed changes survive failures |

---

# Isolation Levels ★★★★★

| Level | Dirty Read | Non-repeatable Read | Phantom Read |
|------|-------------|---------------------|---------------|
| Read Uncommitted | Yes | Yes | Yes |
| Read Committed | No | Yes | Yes |
| Repeatable Read | No | No | Yes |
| Serializable | No | No | No |

---

# Optimistic Locking ★★★★★

## Interview Answer

Optimistic locking assumes conflicts are rare.

Instead of locking rows, it detects conflicts using a version number.

If the version changes before update,

the transaction retries or fails.

Commonly implemented using

```java
@Version
```

in JPA.

---

# Pessimistic Locking ★★★★★

Locks rows before modification.

Other transactions must wait until the lock is released.

Suitable when conflicts are expected.

---

# Optimistic vs Pessimistic Locking ★★★★★

| Optimistic | Pessimistic |
|------------|-------------|
| No lock initially | Lock acquired immediately |
| Better concurrency | Lower concurrency |
| Version based | Database lock based |
| Retry on conflict | Wait for lock |

---

# Normalization ★★★★☆

Normalization reduces data redundancy and improves data integrity.

Most commonly discussed forms

- 1NF
- 2NF
- 3NF

---

# Frequently Asked Questions

1. WHERE vs HAVING.
2. INNER vs LEFT JOIN.
3. GROUP BY.
4. ROW_NUMBER vs RANK vs DENSE_RANK.
5. Find the Nth highest salary.
6. What is a CTE?
7. What is an Index?
8. When should indexes be avoided?
9. Explain ACID properties.
10. Isolation Levels.
11. Optimistic vs Pessimistic Locking.
12. What is Normalization?

---

# SQL Quick Revision

### SQL Categories
- DDL
- DML
- DQL
- DCL
- TCL

### Joins
- INNER
- LEFT
- RIGHT
- FULL
- CROSS

### Aggregation
- GROUP BY
- HAVING
- ORDER BY

### Window Functions
- ROW_NUMBER
- RANK
- DENSE_RANK
- LEAD
- LAG

### Performance
- Index
- Composite Index
- Query Optimization

### Transactions
- ACID
- Isolation Levels
- Optimistic Locking
- Pessimistic Locking

### Most Asked Questions
- WHERE vs HAVING
- INNER vs LEFT JOIN
- GROUP BY
- ROW_NUMBER vs RANK
- Nth Highest Salary
- Index
- ACID
- Isolation Levels
- Optimistic vs Pessimistic Locking
