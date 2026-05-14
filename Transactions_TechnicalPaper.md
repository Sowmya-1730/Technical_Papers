# Transactions in DBMS and SQL

# Introduction

A transaction is a sequence of one or more SQL operations executed as a single logical unit of work. A transaction should either:

* Complete fully
  OR
* Fail completely

This behavior is controlled using ACID properties.

Transactions are extremely important in database systems because they ensure:

* Data consistency
* Data integrity
* Reliable operations
* Safe concurrent access

Transactions are commonly used in:

* Banking systems
* E-commerce applications
* Ticket booking systems
* Payroll systems
* Inventory management systems


# Real-World Example

## Bank Money Transfer

Suppose:

* ₹1000 transferred from Account A to Account B

Steps:

1. Deduct ₹1000 from Account A
2. Add ₹1000 to Account B

If only one step succeeds:

* Database becomes inconsistent

Therefore:

* Both operations must succeed together.


# Example Transaction

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;

COMMIT;
```

# Transaction States

A transaction passes through different states during execution.

# 1. Active State

Transaction is currently executing.

Example:

* SQL statements are running.

# 2. Partially Committed State

All statements executed successfully.

But changes are not permanently saved yet.

# 3. Committed State

Transaction completed successfully.

Changes are permanently stored.

# 4. Failed State

Transaction encounters an error.

Example:

* System crash
* Constraint violation
* Deadlock

# 5. Aborted State

Transaction is rolled back.

All changes are undone.

# Transaction Control Commands (TCL)

Transactions are controlled using TCL commands:

1. BEGIN / START TRANSACTION
2. COMMIT
3. ROLLBACK
4. SAVEPOINT

# 1. BEGIN Transaction

# Definition

BEGIN starts a new transaction.

# Syntax

```sql
BEGIN;
```

OR

```sql
START TRANSACTION;
```

# Example

```sql
BEGIN;
```

# 2. COMMIT Command

# Definition

COMMIT permanently saves all changes made during the transaction.

# Syntax

```sql
COMMIT;
```

# Example

```sql
BEGIN;

UPDATE employees
SET salary = 60000
WHERE emp_id = 1;

COMMIT;
```

After COMMIT:

* Changes become permanent.

# 3. ROLLBACK Command

# Definition

ROLLBACK undoes all changes made during the transaction.

# Syntax

```sql
ROLLBACK;
```

# Example

```sql
BEGIN;

DELETE FROM employees
WHERE emp_id = 5;

ROLLBACK;
```

Deleted data is restored.

# 4. SAVEPOINT Command

# Definition

SAVEPOINT creates a temporary checkpoint inside a transaction.

Allows partial rollback.

# Syntax

```sql
SAVEPOINT savepoint_name;
```

# Example

```sql
BEGIN;

INSERT INTO employees
VALUES (1, 'John', 50000, 'HR');

SAVEPOINT sp1;

INSERT INTO employees
VALUES (2, 'Alice', 60000, 'IT');

ROLLBACK TO sp1;

COMMIT;
```

Only the first insert remains.

# Why Transactions are Important

Transactions ensure:

1. Reliable operations
2. Data consistency
3. Safe concurrent access
4. Error recovery
5. Prevention of partial updates
