# Database Isolation Levels in DBMS

# Introduction

Database Isolation Levels define how transactions interact with each other when multiple transactions execute simultaneously.

Isolation levels are part of the ACID properties in DBMS.

They help control:

* Concurrent transaction access
* Data consistency
* Visibility of changes between transactions

Isolation levels mainly prevent problems like:

* Dirty reads
* Non-repeatable reads
* Phantom reads

# What is Isolation?

Isolation ensures that transactions execute independently without interfering with each other.

Even when multiple users access the database simultaneously, each transaction should behave as if it is running alone.


# What is a Transaction?

A transaction is a sequence of SQL operations executed as one logical unit.

Example:

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

# Why Isolation Levels are Needed

Without proper isolation:

* Multiple users may access same data simultaneously
* Inconsistent results may occur
* Data corruption can happen

Example:

* Two users withdraw money simultaneously
* Incorrect balance may be stored


# Types of Isolation Levels

There are four standard isolation levels:

1. Read Uncommitted
2. Read Committed
3. Repeatable Read
4. Serializable

# 1. Read Uncommitted

# Definition

Lowest isolation level.

Transactions can read uncommitted changes from other transactions.

# Characteristics

* Dirty reads possible
* Non-repeatable reads possible
* Phantom reads possible
* Highest concurrency
* Fastest performance

# Example

```sql
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
```

# Advantages

1. High performance
2. Minimal locking
3. Fast transaction execution

# Disadvantages

1. Dirty reads occur
2. Data inconsistency possible
3. Unsafe for financial systems

# Use Cases

Used rarely in production systems.

Suitable for:

* Reporting systems
* Non-critical analytics

# 2. Read Committed

# Definition

Transactions can only read committed data.

Dirty reads are prevented.

# Characteristics

* Dirty reads prevented
* Non-repeatable reads possible
* Phantom reads possible
* Most commonly used isolation level

# Example

```sql
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

# Advantages

1. Prevents dirty reads
2. Good balance between consistency and performance
3. Widely supported

# Disadvantages

1. Non-repeatable reads still possible
2. Phantom reads possible

# Use Cases

Suitable for:

* Most business applications
* Web applications
* Banking systems in some cases

# 3. Repeatable Read

# Definition

Ensures that rows read during a transaction cannot change until transaction completes.

# Characteristics

* Dirty reads prevented
* Non-repeatable reads prevented
* Phantom reads may still occur

# Example

```sql
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
```

# Advantages

1. Stable query results
2. Better consistency
3. Prevents lost updates

# Disadvantages

1. More locking
2. Reduced concurrency
3. Slower performance compared to lower levels

# Use Cases

Suitable for:

* Inventory systems
* Financial systems
* Critical transaction systems

# 4. Serializable

# Definition

Highest isolation level.

Transactions execute as if they are running one after another sequentially.

# Characteristics

* Dirty reads prevented
* Non-repeatable reads prevented
* Phantom reads prevented
* Strongest consistency
* Lowest concurrency

# Example

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

# Advantages

1. Maximum data consistency
2. Prevents all concurrency problems
3. Safest isolation level

# Disadvantages

1. Slowest performance
2. High locking overhead
3. Reduced scalability

# Use Cases

Suitable for:

* Banking systems
* Airline reservation systems
* Stock trading systems
* Critical enterprise applications
