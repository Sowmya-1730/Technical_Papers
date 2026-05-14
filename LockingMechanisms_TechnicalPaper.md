# What is a Lock?

A lock is a restriction applied on database objects.

Locks prevent unauthorized concurrent access.

Database objects that can be locked:

* Rows
* Tables
* Pages
* Databases

# Goals of Locking

1. Prevent data inconsistency
2. Maintain isolation
3. Avoid lost updates
4. Support concurrent transactions safely
5. Ensure ACID properties

# Types of Locks

1. Shared Lock (Read Lock)
2. Exclusive Lock (Write Lock)
3. Update Lock
4. Intent Lock
5. Schema Lock


# 1. Shared Lock (S Lock)

# Definition

Shared lock allows multiple transactions to read data simultaneously.

But:

* No transaction can modify the data while shared lock exists.

# Characteristics

* Multiple reads allowed
* Writing blocked
* Used for SELECT operations

# Example

```sql
SELECT *
FROM accounts
WHERE account_id = 1;
```

Database may place a shared lock on the row.

# Scenario

## Transaction A

Reads account balance.

## Transaction B

Can also read same balance.

## Transaction C

Cannot update balance until locks are released.

# Advantages

1. Supports concurrent reads
2. Improves performance
3. Prevents dirty writes

# Disadvantages

1. Write operations must wait
2. Can reduce update performance



# 2. Exclusive Lock (X Lock)

# Definition

Exclusive lock allows only one transaction to read and modify data.

No other transaction can:

* Read
* Write

Until lock is released.

# Characteristics

* Used for INSERT, UPDATE, DELETE
* Full access to transaction owner
* Prevents all concurrent access

# Example

```sql
UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;
```

Database applies exclusive lock.

# Scenario

## Transaction A

Updates account balance.

## Transaction B

Cannot:

* Read balance
* Modify balance

Until Transaction A commits or rolls back.

# Advantages

1. Strong consistency
2. Prevents conflicting updates
3. Ensures transaction safety

# Disadvantages

1. Reduced concurrency
2. Transactions may wait longer



# 3. Update Lock

# Definition

Update lock is used when a transaction intends to modify data later.

Helps prevent deadlocks.

# Example Scenario

Transaction first reads data.

Later:

* Converts update lock into exclusive lock.

# Advantages

1. Reduces deadlocks
2. Efficient lock conversion



# 4. Intent Locks

# Definition

Intent locks indicate that a transaction plans to place locks at lower levels.

Used in hierarchical locking.

# Types

1. Intent Shared (IS)
2. Intent Exclusive (IX)
3. Shared Intent Exclusive (SIX)

# Example

If a row lock is needed:

* Database places intent lock on table first.



# 5. Schema Locks

# Definition

Schema locks protect database structure.

Used during:

* ALTER TABLE
* DROP TABLE
* CREATE INDEX

# Example

```sql
ALTER TABLE employees
ADD email VARCHAR(100);
```

Schema lock prevents other operations during modification.

