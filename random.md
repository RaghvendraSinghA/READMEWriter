# SQL Concepts - Technical Paper

## Introduction

A database is an organized collection of data that allows applications to store, retrieve, modify, and manage information efficiently.

A Database Management System (DBMS) is software responsible for managing databases. Examples include:

* PostgreSQL
* MySQL
* SQLite
* Oracle Database
* Microsoft SQL Server

SQL Structured Query Language is used to interact with relational databases. SQL allows us to:

* Create databases and tables
* Insert data
* Retrieve data

A relational database stores information in tables, where:

* A row represents a record.
* A column represents an attribute.
* A primary key uniquely identifies a row.
* A foreign key establishes relationships between tables.



---

# 2. ACID Properties

ACID describes four properties that help database transactions remain reliable:

1. Atomicity
2. Consistency
3. Isolation
4. Durability

These properties are fundamental to transactional database systems.

---

## 2.1 Atomicity

Atomicity means that a transaction is treated as a single unit of work.

Either:

* All operations succeed, or
* None of them are applied.

Atomicity guarantees that the transaction is rolled back, instead of partially applied.

---

## 2.2 Consistency

Consistency means that a transaction must move the database from one valid state to another valid state.

Database constraints help maintain consistency.

For example:

```sql
CREATE TABLE accounts (
    account_id INT PRIMARY KEY,
    balance NUMERIC CHECK (balance >= 0)
);
```

The `CHECK` constraint prevents invalid balances:

```sql
INSERT INTO accounts VALUES (1, -500);
```
The database rejects the operation because it violates the constraint.

Consistency can be enforced using:

* Primary keys
* Foreign keys
* Unique constraints
* NOT NULL constraints
* etc.

---

## 2.3 Isolation

Isolation controls how concurrently executing transactions interact with each other.

Suppose two users attempt to modify the same bank account simultaneously.
Without proper isolation, one transaction could interfere with another.

The SQL standard defines four isolation levels:

1. Read Uncommitted
2. Read Committed
3. Repeatable Read
4. Serializable

PostgreSQL implements three distinct behaviors internally because its `READ UNCOMMITTED` behaves like `READ COMMITTED`.

---

## 2.4 Durability

Durability means that once a transaction is successfully committed, its changes should survive failures such as:

* Application crashes
* Database crashes
* Operating-system failures
* Server restarts

Database systems use mechanisms such as write-ahead logging (WAL) to support durability.

---

# 3. CAP Theorem

The CAP theorem applies primarily to distributed systems rather than a traditional single-node relational database.

CAP stands for:

* C — Consistency
* A — Availability
* P — Partition Tolerance

The theorem states that during a network partition like partition in 2 separate copy of same database, a distributed system cannot    
simultaneously guarantee both strong consistency and availability.

---

## 3.1 Consistency

Consistency in CAP means that a read receives the most recent successful write, or        
the system reports an error instead of returning an inconsistent result.

Example:

```text
User updates:
balance = ₹10,000
```

If another server immediately reads the balance, a strongly consistent system should return:

```text
₹10,000
```

rather than an older value.

---

## 3.2 Availability

Availability means that every request receives a response, even if some nodes are unavailable.

For example:

```text
Server A
Server B
Server C
```

If Server B fails, an available system should still respond using other nodes.
The response may potentially contain data that is not the most recent, depending on the consistency model.

---

## 3.3 Partition Tolerance

A network partition occurs when distributed nodes cannot communicate reliably.

For example:

```text
Node A  ----X----  Node B
```

The nodes are still running, but communication between them has failed.
Partition tolerance means the system continues operating despite this network failure.
Distributed systems generally need to tolerate network partitions, so the practical design decision during a    
partition becomes a trade-off between consistency and availability.

---

## 3.4 CP Systems

CP = Consistency + Partition Tolerance

During a network partition, the system sacrifices availability to preserve consistency.
This approach is useful when incorrect data is worse than temporary unavailability.

Examples of suitable workloads include:

* Financial transactions
* Inventory management
* Systems requiring strong correctness

---

## 3.5 AP Systems

AP = Availability + Partition Tolerance

During a network partition, the system continues responding even if some nodes temporarily have different data.

This commonly involves eventual consistency.

Example:
* Profile page management
* Video recommendation

---

# 4. Joins

A JOIN combines rows from two or more tables based on a related column.

---

## 4.1 INNER JOIN

An `INNER JOIN` returns only rows that have matching records in both tables.


---

## 4.2 LEFT JOIN

A `LEFT JOIN` returns:

* Every row from the left table
* Matching rows from the right table
* `NULL` when no match exists


---

## 4.3 RIGHT JOIN

A `RIGHT JOIN` returns every row from the right table and matching rows from the left table.
A `RIGHT JOIN` can generally be rewritten as a `LEFT JOIN` by reversing the table order.

---

## 4.4 FULL OUTER JOIN

A `FULL OUTER JOIN` returns:

* Matching rows
* Unmatched rows from the left table
* Unmatched rows from the right table


## 4.5 CROSS JOIN

A `CROSS JOIN` produces the Cartesian product.

---

## 4.6 SELF JOIN

A self join joins a table with itself.

---

# 5. Aggregations and Filters

SQL provides aggregate functions for calculating values across multiple rows.

Common aggregate functions include:

* `COUNT()`
* `SUM()`
* `AVG()`
* `MIN()`
* `MAX()`

---

## 5.1 COUNT

```sql
SELECT COUNT(*)
FROM orders;
```

Counts the number of rows.

---

## 5.2 SUM

```sql
SELECT SUM(amount)
FROM orders;
```

Calculates the total amount.

---

# 6. GROUP BY

`GROUP BY` creates groups of rows.

For example:

```sql
SELECT
    customer_id,
    SUM(amount) AS total_amount
FROM orders
GROUP BY customer_id;
```

---

# 7. HAVING

`HAVING` filters groups after aggregation.

For example:

```sql
SELECT
    customer_id,
    SUM(amount) AS total_amount
FROM orders
GROUP BY customer_id
HAVING SUM(amount) > 500;
```

This returns only customers whose total purchases exceed 500.

---

# 8. Normalization

Normalization is the process of organizing data to reduce redundancy and improve data integrity.

## 8.1 First Normal Form (1NF)

A table is generally in **1NF** when:

* Each column contains atomic values.
* There are no repeating groups.
* Each row represents a distinct record.


## 8.2 Second Normal Form (2NF)

A table is in 2NF when:

1. It is in 1NF.
2. Non-key attributes depend on the whole primary key, not just part of a composite key.


# 8.3 Third Normal Form (3NF)

A table is in 3NF when:

1. It is in 2NF.
2. Non-key attributes do not depend on other non-key attributes.


### Advantages of Normalization

Normalization helps:

* Reduce duplicate data
* Prevent update anomalies
* Prevent insertion anomalies
* Prevent deletion anomalies
* Improve data consistency
* Make relationships clearer

---

# 9. Indexes

An **index** is a database structure that allows the database to locate rows more efficiently.

Without an index, a database may need to scan every row.

Suppose a table contains:

```text
10,000,000 customers
```

and we execute:

```sql
SELECT *
FROM customers
WHERE email = 'alice@example.com';
```

Without an appropriate index, the database may perform a sequential scan.

Creating an index:

```sql
CREATE INDEX idx_customers_email
ON customers(email);
```

can allow the database to find matching rows more efficiently.

---

# 17. How an Index Works

A common index structure is a **B-tree**.

Conceptually:

```text
                 [50]
                /    \
             [20]    [80]
            /  \      /  \
          ...  ...  ...  ...
```

Instead of checking every row, the database can navigate the index structure toward the required value.

---

# 18. Types of Indexes

Different database systems provide different index types.

Common examples include:

* B-tree
* Hash
* GIN
* GiST
* BRIN

For example:

```sql
CREATE INDEX idx_users_name
ON users(name);
```

---

# 19. Composite Indexes

An index can contain multiple columns:

```sql
CREATE INDEX idx_orders_customer_date
ON orders(customer_id, order_date);
```

This can be useful for queries such as:

```sql
SELECT *
FROM orders
WHERE customer_id = 10
ORDER BY order_date;
```

The order of columns in a composite index matters.

---

# 20. Index Advantages

Indexes can significantly improve:

```sql
SELECT
UPDATE
DELETE
JOIN
ORDER BY
WHERE
```

operations when the indexed columns are useful to the query planner.

---

# 21. Index Disadvantages

Indexes are not free.

They:

* Consume disk space.
* Increase storage requirements.
* Must be maintained when rows are inserted.
* Must be updated when indexed values change.
* Can slow down write-heavy workloads.

Therefore, adding an index to every column is generally a bad strategy.

Indexes should be created based on actual query patterns.

---

# 22. Transactions

A **transaction** is a sequence of database operations treated as one logical unit.

Basic syntax:

```sql
BEGIN;

-- SQL operations

COMMIT;
```

If something goes wrong:

```sql
ROLLBACK;
```

---

## 22.1 COMMIT

`COMMIT` permanently applies the transaction.

```sql
BEGIN;

INSERT INTO customers(name)
VALUES ('Alice');

COMMIT;
```

---

## 22.2 ROLLBACK

`ROLLBACK` cancels changes made by the current transaction.

```sql
BEGIN;

DELETE FROM customers
WHERE customer_id = 10;

ROLLBACK;
```

The deletion is undone.

---

## 22.3 SAVEPOINT

A savepoint allows partial rollback within a transaction.

```sql
BEGIN;

INSERT INTO customers(name)
VALUES ('Alice');

SAVEPOINT customer_insert;

INSERT INTO customers(name)
VALUES ('Bob');

ROLLBACK TO SAVEPOINT customer_insert;

COMMIT;
```

The Alice insertion remains, while the Bob insertion is rolled back.

---

# 23. Locking Mechanisms

When multiple transactions access the same data simultaneously, the database needs mechanisms to coordinate them.

A **lock** controls access to database resources.

Consider two transactions:

```text
Transaction A
     ↓
Updates row X

Transaction B
     ↓
Attempts to update row X
```

The database must prevent the transactions from corrupting each other's changes.

PostgreSQL provides table-level, row-level, page-level, and advisory locks, along with mechanisms for handling deadlocks.

---

# 24. Row-Level Lock

A transaction can explicitly lock rows:

```sql
SELECT *
FROM accounts
WHERE account_id = 1
FOR UPDATE;
```

The selected row is locked for update.

Another transaction attempting a conflicting operation may have to wait.

This is useful for operations such as:

```text
Read account balance
       ↓
Modify account balance
       ↓
Commit
```

---

# 25. Table-Level Lock

A table-level lock affects a larger resource.

Example:

```sql
LOCK TABLE accounts;
```

Table-level locks can restrict concurrent operations more broadly than row-level locks.

They should therefore be used carefully.

---

# 26. Shared and Exclusive Locks

Conceptually, locks can be categorized as:

### Shared Lock

Multiple transactions may hold compatible shared locks simultaneously.

Useful when data is being read.

### Exclusive Lock

Only one transaction can hold the required exclusive access.

Used for operations that modify data.

The exact lock modes and compatibility rules depend on the database system.

---

# 27. Deadlocks

A **deadlock** occurs when two or more transactions wait for each other indefinitely.

Example:

```text
Transaction A
locks Row 1
     ↓
waits for Row 2

Transaction B
locks Row 2
     ↓
waits for Row 1
```

Diagram:

```text
Transaction A ──waits──> Row 2
      ↑                    │
      │                    ↓
    Row 1 <──waits──── Transaction B
```

Neither transaction can continue.

Database systems detect deadlocks and abort one of the transactions so that the other can proceed.

---

# 28. Database Isolation Levels

Isolation levels determine how transactions interact with concurrent transactions.

The four standard levels are:

1. Read Uncommitted
2. Read Committed
3. Repeatable Read
4. Serializable

The main anomalies used to describe isolation behavior are:

* Dirty reads
* Non-repeatable reads
* Phantom reads
* Serialization anomalies

PostgreSQL documents these levels and their behavior explicitly.

---

# 29. Dirty Read

A dirty read occurs when one transaction reads data written by another transaction that has not yet committed.

Example:

```text
Transaction A:
UPDATE balance = 10000
-- not committed

Transaction B:
SELECT balance
-- reads 10000
```

If Transaction A later executes:

```sql
ROLLBACK;
```

Transaction B has read data that never actually became committed.

---

# 30. Non-Repeatable Read

Suppose Transaction A reads:

```text
balance = 5000
```

Then Transaction B changes it:

```text
balance = 7000
```

and commits.

Transaction A reads the same row again and gets:

```text
7000
```

The same query produced different results within the same transaction.

This is a **non-repeatable read**.

---

# 31. Phantom Read

A phantom read occurs when a transaction repeats a query and discovers a different set of rows because another transaction inserted or removed matching rows.

Example:

Transaction A:

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

Suppose it returns 10 rows.

Transaction B inserts another employee:

```text
salary = 60000
```

and commits.

Transaction A executes the query again and now gets 11 rows.

The new row is a **phantom row**.

---

# 32. Read Uncommitted

The weakest standard isolation level.

Conceptually:

```text
Dirty reads       → possible
Non-repeatable    → possible
Phantom reads     → possible
```

However, PostgreSQL treats `READ UNCOMMITTED` as `READ COMMITTED`, so dirty reads are not actually permitted in PostgreSQL.

---

# 33. Read Committed

`READ COMMITTED` is PostgreSQL's default isolation level.

Each query sees data committed before that query begins.

Two queries within the same transaction can therefore see different committed data if another transaction commits changes between them.

Example:

```sql
BEGIN;

SELECT balance
FROM accounts
WHERE account_id = 1;

-- Another transaction modifies and commits.

SELECT balance
FROM accounts
WHERE account_id = 1;

COMMIT;
```

The two queries may see different values.

---

# 34. Repeatable Read

Repeatable Read provides a stable snapshot for the transaction.

Conceptually:

```text
Transaction starts
       ↓
Snapshot created
       ↓
Query 1 sees snapshot
       ↓
Other transactions commit
       ↓
Query 2 still sees transaction snapshot
```

PostgreSQL's implementation provides stronger protection than the minimum required by the SQL standard and does not permit phantom reads under its Repeatable Read implementation.

---

# 35. Serializable

`SERIALIZABLE` provides the strongest isolation.

The goal is to make concurrent transactions behave as though they had executed one after another.

For example:

```text
Transaction A
      ↓
Transaction B
      ↓
Equivalent to:
A → B
```

or:

```text
B → A
```

If the database detects that concurrent execution cannot produce a valid serial ordering, one transaction can fail and must be retried.

PostgreSQL's Serializable mode can therefore produce serialization failures that applications should be prepared to retry.

---

# 36. Isolation Level Comparison

| Isolation Level  | Dirty Read | Non-repeatable Read | Phantom Read | Serialization Anomaly |
| ---------------- | ---------- | ------------------- | ------------ | --------------------- |
| Read Uncommitted | Possible*  | Possible            | Possible     | Possible              |
| Read Committed   | No         | Possible            | Possible     | Possible              |
| Repeatable Read  | No         | No                  | Possible**   | Possible              |
| Serializable     | No         | No                  | No           | No                    |

`*` PostgreSQL maps Read Uncommitted to Read Committed.

`**` The SQL standard permits phantom reads at Repeatable Read, but PostgreSQL's implementation prevents them.

---

# 37. Setting Isolation Levels in PostgreSQL

Isolation can be specified using:

```sql
BEGIN;

SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;

-- operations

COMMIT;
```

Or:

```sql
BEGIN TRANSACTION ISOLATION LEVEL REPEATABLE READ;

-- operations

COMMIT;
```

---

# 38. Triggers

A **trigger** is a database mechanism that automatically executes a function or procedure when a specified database event occurs.

Triggers can respond to events such as:

* `INSERT`
* `UPDATE`
* `DELETE`

For example:

```text
INSERT into users
       ↓
Trigger executes
       ↓
Audit record created
```

---

# 39. Why Use Triggers?

Triggers can be useful for:

* Audit logging
* Maintaining derived data
* Enforcing complex business rules
* Automatically updating timestamps
* Recording changes
* Maintaining history tables

---

# 40. Trigger Example

Suppose we want to automatically update an `updated_at` column.

```sql
CREATE OR REPLACE FUNCTION update_timestamp()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_at = CURRENT_TIMESTAMP;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

Create the trigger:

```sql
CREATE TRIGGER set_updated_at
BEFORE UPDATE ON customers
FOR EACH ROW
EXECUTE FUNCTION update_timestamp();
```

Now:

```sql
UPDATE customers
SET name = 'Alice Smith'
WHERE customer_id = 1;
```

automatically updates:

```text
updated_at
```

---

# 41. BEFORE and AFTER Triggers

A trigger can execute:

### BEFORE

Before the operation occurs.

```sql
BEFORE INSERT
```

Useful for modifying or validating `NEW` values.

### AFTER

After the operation succeeds.

```sql
AFTER INSERT
```

Useful for auditing or recording an event.

---

# 42. Row-Level vs Statement-Level Triggers

### Row-Level Trigger

Runs once for every affected row.

```sql
FOR EACH ROW
```

If an `UPDATE` modifies 100 rows:

```text
Trigger executes 100 times
```

### Statement-Level Trigger

Runs once for the entire SQL statement.

```sql
FOR EACH STATEMENT
```

If an `UPDATE` modifies 100 rows:

```text
Trigger executes once
```

---

# 43. OLD and NEW

In row-level triggers, `OLD` and `NEW` can represent row values.

For an update:

```text
OLD → value before update
NEW → value after update
```

Example:

```sql
CREATE OR REPLACE FUNCTION log_name_change()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO customer_audit(
        customer_id,
        old_name,
        new_name
    )
    VALUES (
        OLD.customer_id,
        OLD.name,
        NEW.name
    );

    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

This can be used to maintain an audit history.

---

# 44. Trigger Advantages

Triggers can:

* Automatically execute database logic
* Centralize certain integrity rules
* Maintain audit information
* Reduce duplicated application logic
* Ensure logic runs regardless of which application performs the operation

---

# 45. Trigger Disadvantages

Triggers can also make systems harder to understand.

Problems include:

* Hidden behavior
* Difficult debugging
* Unexpected side effects
* Additional database workload
* Complex chains of triggers

For example:

```text
INSERT
 ↓
Trigger A
 ↓
UPDATE
 ↓
Trigger B
 ↓
INSERT
 ↓
Trigger C
```

The original SQL statement may appear simple while triggering substantial additional work.

Therefore, triggers should be used when database-level automatic behavior is genuinely useful.

---

# 46. Relationship Between Transactions, Locks and Isolation

These concepts are closely related.

Consider two users attempting to purchase the last item:

```text
Inventory:
Product A
Quantity = 1
```

Two transactions execute concurrently.

Without proper concurrency control:

```text
Transaction A → reads quantity = 1
Transaction B → reads quantity = 1

Transaction A → purchases item
Transaction B → purchases item
```

The system may sell two items even though only one existed.

Concurrency control can prevent this.

For example:

```sql
BEGIN;

SELECT quantity
FROM inventory
WHERE product_id = 1
FOR UPDATE;

UPDATE inventory
SET quantity = quantity - 1
WHERE product_id = 1;

COMMIT;
```

The row lock coordinates concurrent updates.

The transaction provides the unit of work, the lock controls conflicting access, and the isolation level defines what concurrent transactions can observe.

---

# 47. ACID vs Transactions vs Isolation

These concepts are related but not identical.

### Transaction

A transaction is the **unit of work**.

```sql
BEGIN;
...
COMMIT;
```

### ACID

ACID describes the **properties expected from reliable transactions**.

```text
Atomicity
Consistency
Isolation
Durability
```

### Isolation Level

Isolation level determines **how much concurrent transactions are isolated from each other**.

```text
Read Committed
Repeatable Read
Serializable
```

### Locking

Locking is one mechanism used by database systems to coordinate concurrent access.

---

# 48. Practical Example

Consider an online store.

### Tables

```sql
CREATE TABLE products (
    product_id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    stock INT CHECK (stock >= 0)
);

CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    product_id INT REFERENCES products(product_id),
    quantity INT CHECK (quantity > 0)
);
```

A customer purchases a product.

The operation should:

1. Check stock.
2. Reduce stock.
3. Create the order.
4. Commit both operations.

A transaction can be used:

```sql
BEGIN;

SELECT stock
FROM products
WHERE product_id = 1
FOR UPDATE;

UPDATE products
SET stock = stock - 1
WHERE product_id = 1;

INSERT INTO orders(product_id, quantity)
VALUES (1, 1);

COMMIT;
```

If the order insertion fails:

```sql
ROLLBACK;
```

The stock reduction is also rolled back.

This example demonstrates how several database concepts work together:

```text
Transaction
    ↓
Atomicity
    ↓
Row Lock
    ↓
Concurrency Control
    ↓
Isolation
    ↓
Consistency
```

---

