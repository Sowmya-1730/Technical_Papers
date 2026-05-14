# ACID Properties in DBMS

# Introduction

ACID properties are a set of rules that ensure reliable and consistent database transactions.

ACID stands for:

* A → Atomicity
* C → Consistency
* I → Isolation
* D → Durability

These properties are essential in relational database systems like:

* PostgreSQL
* MySQL
* Oracle
* SQL Server

ACID properties help maintain:

* Data integrity
* Data accuracy
* Reliability
* Safe concurrent transactions


# What is a Transaction?

A transaction is a sequence of one or more SQL operations executed as a single unit.

Examples:

* Bank money transfer
* Online shopping payment
* Ticket booking system
* Updating employee salary

A transaction should either:

* Complete fully
  OR
* Fail completely


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

This transaction transfers money from one account to another.



# 1. Atomicity

# Definition

Atomicity means:

"Either all operations in a transaction are completed successfully or none of them are performed."

It follows the:

"All or Nothing" principle.



# Why Atomicity is Important

Without atomicity:

* Partial updates may happen
* Database becomes inconsistent
* Money may disappear in banking systems



# Example Without Atomicity

Suppose:

* ₹1000 deducted from Account A
* System crashes before adding to Account B

Result:

* Money lost
* Database inconsistency


# Example With Atomicity

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

If any statement fails:

```sql
ROLLBACK;
```

All changes are undone.



# Real-World Example

## ATM Withdrawal

Steps:

1. Deduct amount from account
2. Dispense cash
3. Update transaction history

If cash is not dispensed:

* Amount deduction must also be cancelled



# 2. Consistency

# Definition

Consistency ensures that the database remains in a valid state before and after transactions.

It maintains:

* Rules
* Constraints
* Relationships
* Data integrity


# Why Consistency is Important

Consistency prevents:

* Invalid data
* Duplicate primary keys
* Foreign key violations
* Incorrect balances



# Example

Suppose a bank rule says:

"Total money before and after transfer must remain same."

Before transfer:

* Account A = 5000
* Account B = 3000
* Total = 8000

After transfer of 1000:

* Account A = 4000
* Account B = 4000
* Total = 8000

Consistency maintained.



# Constraints That Ensure Consistency

## Primary Key Constraint

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

Prevents duplicate IDs.


## Foreign Key Constraint

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id)
    REFERENCES customers(customer_id)
);
```

Ensures valid relationships.


## CHECK Constraint

```sql
CREATE TABLE employees (
    emp_id INT,
    salary INT CHECK (salary > 0)
);
```

Prevents invalid salaries.


# 3. Isolation

# Definition

Isolation ensures that multiple transactions execute independently without interfering with each other.

Each transaction should behave as if it is the only transaction running.


# Why Isolation is Important

Without isolation:

* Dirty reads occur
* Lost updates occur
* Incorrect data may appear


# Example Scenario

Two users withdraw money simultaneously.

Initial balance = 5000

User A withdraws 1000.
User B withdraws 2000.

Without isolation:

* Incorrect final balance may occur.

With isolation:

* Transactions are properly separated.


# Isolation Problems

# Dirty Read

Reading uncommitted data.

Example:

* Transaction A updates salary but does not commit.
* Transaction B reads updated salary.
* Transaction A rolls back.

Transaction B read invalid data.

# Non-Repeatable Read

Same query gives different results within same transaction.

# Phantom Read

New rows appear during transaction execution.

# Isolation Levels

## Read Uncommitted

* Lowest isolation
* Dirty reads possible

## Read Committed

* Prevents dirty reads
* Most commonly used

## Repeatable Read

* Prevents non-repeatable reads

## Serializable

* Highest isolation level
* Safest but slowest


# Example

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```


# 4. Durability

# Definition

Durability ensures that once a transaction is committed, the changes are permanently saved.

Even if:

* System crashes
* Power failure occurs
* Database restarts

Committed data remains safe.

# Why Durability is Important

Without durability:

* Data may disappear after crash
* Financial systems become unreliable


# Example

```sql
BEGIN;

UPDATE employees
SET salary = 60000
WHERE emp_id = 1;

COMMIT;
```

After COMMIT:

* Changes are permanently stored.

Even after restart:

* Updated salary remains.

# How Durability is Achieved

Databases use:

* Transaction logs
* Write-ahead logging (WAL)
* Backups
* Recovery systems


# Real-World Example

## Online Payment

After successful payment:

* Order information must remain stored
* Even if server crashes immediately after payment


# Complete ACID Example

Suppose:

Account A transfers ₹2000 to Account B.

---

## Step 1: Begin Transaction

```sql
BEGIN;
```

## Step 2: Deduct Money

```sql
UPDATE accounts
SET balance = balance - 2000
WHERE account_id = 1;
```

## Step 3: Add Money

```sql
UPDATE accounts
SET balance = balance + 2000
WHERE account_id = 2;
```


## Step 4: Commit

```sql
COMMIT;
```

# How ACID Works Here

## Atomicity

* Both updates happen together.

## Consistency

* Total money remains same.

## Isolation

* Other users cannot interfere.

## Durability

* Changes remain after commit.

# Advantages of ACID Properties

1. Maintains data integrity
2. Prevents inconsistent data
3. Supports safe concurrent access
4. Ensures reliable transactions
5. Essential for banking systems
6. Important for e-commerce systems
7. Prevents data corruption


# Disadvantages of Strict ACID Systems

1. Can reduce performance
2. Higher storage usage for logs
3. Locking may slow concurrent transactions
4. Distributed systems become complex
