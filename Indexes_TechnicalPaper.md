# What is an Index?

An index is a data structure that stores:

* Indexed column values
* Pointers to actual table rows

Indexes help databases locate rows efficiently.

# Why Indexes are Important

Without indexes:

* Database performs full table scans.
* Queries become slow for large tables.

With indexes:

* Queries become much faster.
* Less data scanning occurs.

# Example Without Index

```sql
SELECT *
FROM employees
WHERE emp_id = 1000;
```

Without index:

* Database scans entire table.

# Example With Index

```sql
CREATE INDEX idx_emp_id
ON employees(emp_id);
```

Now database directly locates required row.

# Types of Indexes

# 1. Primary Index

# Definition

Primary index is automatically created on a primary key.

Ensures:

* Fast searching
* Unique values

# Example

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

Database automatically creates index on:

```text
emp_id
```

# Advantages

1. Fast row access
2. Enforces uniqueness
3. Efficient searching


# 2. Unique Index

# Definition

Unique index prevents duplicate values.

# Syntax

```sql
CREATE UNIQUE INDEX index_name
ON table_name(column_name);
```

# Example

```sql
CREATE UNIQUE INDEX idx_email
ON users(email);
```

Prevents duplicate email addresses.

# Advantages

1. Ensures uniqueness
2. Faster lookups
3. Improves integrity


# 3. Composite Index

# Definition

Composite index uses multiple columns.

# Syntax

```sql
CREATE INDEX index_name
ON table_name(column1, column2);
```

# Example

```sql
CREATE INDEX idx_name_dept
ON employees(name, department);
```

Useful when queries filter using both columns.

# Example Query

```sql
SELECT *
FROM employees
WHERE name = 'John'
AND department = 'IT';
```

# Advantages

1. Faster multi-column queries
2. Better filtering performance

# 4. Clustered Index

# Definition

Clustered index determines the physical order of data storage.

Data rows are stored in sorted order.

# Characteristics

* Only one clustered index per table
* Faster range queries
* Data physically organized

# Example

In many DBMS systems:

* Primary key becomes clustered index by default.

# Advantages

1. Fast range queries
2. Efficient sorting
3. Better sequential access

# Disadvantages

1. Slower inserts and updates
2. Only one clustered index allowed



# 5. Non-Clustered Index

# Definition

Non-clustered index stores:

* Indexed values
* Pointers to actual rows

Data itself remains unordered.

# Characteristics

* Multiple non-clustered indexes allowed
* Separate structure from table

# Example

```sql
CREATE INDEX idx_salary
ON employees(salary);
```

# Advantages

1. Multiple indexes possible
2. Faster searching
3. Better query optimization

# Disadvantages

1. Additional storage required
2. Slower write operations



# 6. Full-Text Index

# Definition

Full-text indexes are used for text searching.

Useful for:

* Search engines
* Article searches
* Blog systems

# Example

```sql
CREATE FULLTEXT INDEX idx_content
ON articles(content);
```
# Example Query

```sql
SELECT *
FROM articles
WHERE MATCH(content)
AGAINST('database');
```

# 7. Hash Index

# Definition

Hash indexes use hash functions for searching.

Best for:

* Equality comparisons

# Example

```sql
SELECT *
FROM users
WHERE email = 'john@example.com';
```

# Advantages

1. Very fast equality search
2. Efficient lookups

# Disadvantages

1. Poor for range queries
2. Limited use cases

# 8. Bitmap Index

# Definition

Bitmap indexes use bitmaps for indexing.

Best for columns with:

* Low cardinality

Examples:

* Gender
* Status
* Boolean fields

# Example

```text
Gender:
Male, Female
```

# Advantages

1. Efficient storage
2. Fast analytics queries

# Disadvantages

1. Poor for frequent updates
2. Not suitable for transactional systems



# Creating an Index

# Syntax

```sql
CREATE INDEX index_name
ON table_name(column_name);
```

# Example

```sql
CREATE INDEX idx_dept
ON employees(department);
```

# Viewing Indexes

Example in PostgreSQL:

```sql
\d employees
```

OR

```sql
SELECT *
FROM pg_indexes
WHERE tablename = 'employees';
```

# Dropping an Index

# Syntax

```sql
DROP INDEX index_name;
```

# Example

```sql
DROP INDEX idx_dept;
```

# Advantages of Indexes

1. Faster SELECT queries
2. Faster JOIN operations
3. Better sorting performance
4. Efficient filtering
5. Improved query optimization

# Disadvantages of Indexes

1. Extra storage required
2. Slower INSERT operations
3. Slower UPDATE operations
4. Slower DELETE operations
5. Index maintenance overhead

# When to Use Indexes

Indexes are useful on:

* Frequently searched columns
* JOIN columns
* WHERE clause columns
* ORDER BY columns
* GROUP BY columns

# When NOT to Use Indexes

Avoid indexes on:

* Small tables
* Frequently updated columns
* Columns with very low uniqueness

# Real-World Applications

# Banking Systems

Indexes on:

* Account numbers
* Transaction IDs

# E-Commerce Platforms

Indexes on:

* Product IDs
* Customer IDs
* Order IDs

# Search Engines

Use:

* Full-text indexes

# Social Media Platforms

Indexes on:

* User IDs
* Post IDs
* Hashtags
