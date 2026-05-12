# SQL DDL and DML Commands

# Introduction

SQL (Structured Query Language) is used to communicate with databases.

SQL commands are mainly divided into:

1. DDL (Data Definition Language)
2. DML (Data Manipulation Language)

---

# DDL (Data Definition Language)

DDL commands are used to define and manage the structure of database objects like:

* Databases
* Tables
* Schemas
* Indexes

DDL commands automatically commit changes in many DBMS systems.


# Types of DDL Commands

1. CREATE
2. ALTER
3. DROP
4. TRUNCATE
5. RENAME


# 1. CREATE Command

The CREATE command is used to create:

* Databases
* Tables
* Views
* Indexes

## Syntax

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype
);
```

---

## Example: Create Table

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    department VARCHAR(50)
);
```



# 2. ALTER Command

The ALTER command is used to modify an existing table.

Operations:

* Add column
* Modify column
* Rename column
* Drop column


## Add Column

### Syntax

```sql
ALTER TABLE table_name
ADD column_name datatype;
```

### Example

```sql
ALTER TABLE students
ADD email VARCHAR(100);
```


## Modify Column

### Syntax

```sql
ALTER TABLE table_name
ALTER COLUMN column_name TYPE datatype;
```

### Example

```sql
ALTER TABLE students
ALTER COLUMN name TYPE VARCHAR(200);
```


## Rename Column

### Syntax

```sql
ALTER TABLE table_name
RENAME COLUMN old_name TO new_name;
```

### Example

```sql
ALTER TABLE students
RENAME COLUMN department TO branch;
```


## Drop Column

### Syntax

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

### Example

```sql
ALTER TABLE students
DROP COLUMN email;
```



# 3. DROP Command

The DROP command completely removes a database object.

* Structure removed
* Data removed
* Cannot usually be rolled back


## Drop Table

### Syntax

```sql
DROP TABLE table_name;
```

### Example

```sql
DROP TABLE students;
```

## Drop Database

### Syntax

```sql
DROP DATABASE database_name;
```

### Example

```sql
DROP DATABASE college_db;
```



# 4. TRUNCATE Command

The TRUNCATE command removes all rows from a table.

Important:

* Table structure remains
* Faster than DELETE
* Resets identity counters in many DBMS systems


## Syntax

```sql
TRUNCATE TABLE table_name;
```

## Example

```sql
TRUNCATE TABLE students;
```


# Difference Between DELETE and TRUNCATE

| DELETE                                | TRUNCATE                |
| ------------------------------------- | ----------------------- |
| Removes selected rows                 | Removes all rows        |
| Can use WHERE clause                  | Cannot use WHERE clause |
| Slower                                | Faster                  |
| Transaction log maintained row-by-row | Minimal logging         |
| Can rollback in many DBMS             | Limited rollback        |


# 5. RENAME Command

The RENAME command changes the name of a table.


## Syntax

```sql
ALTER TABLE old_table_name
RENAME TO new_table_name;
```

## Example

```sql
ALTER TABLE students
RENAME TO student_details;
```



# DML (Data Manipulation Language)

DML commands are used to manipulate data inside tables.

Operations include:

* Insert data
* Update data
* Delete data
* Retrieve data

# Types of DML Commands

1. INSERT
2. UPDATE
3. DELETE
4. SELECT


# 1. INSERT Command

The INSERT command adds new rows into a table.

## Syntax

```sql
INSERT INTO table_name (column1, column2, column3)
VALUES (value1, value2, value3);
```


## Example

```sql
INSERT INTO students (student_id, name, age, department)
VALUES (1, 'John', 20, 'CSE');
```

## Insert Multiple Rows

```sql
INSERT INTO students (student_id, name, age, department)
VALUES
(2, 'Alice', 21, 'ECE'),
(3, 'Bob', 22, 'IT');
```

# 2. UPDATE Command

The UPDATE command modifies existing data.


## Syntax

```sql
UPDATE table_name
SET column_name = value
WHERE condition;
```


## Example

```sql
UPDATE students
SET age = 23
WHERE student_id = 1;
```


## Important Note

Always use WHERE clause carefully.

Without WHERE:

```sql
UPDATE students
SET age = 25;
```

This updates all rows.


# 3. DELETE Command

The DELETE command removes rows from a table.

## Syntax

```sql
DELETE FROM table_name
WHERE condition;
```


## Example

```sql
DELETE FROM students
WHERE student_id = 2;
```


## Delete All Rows

```sql
DELETE FROM students;
```

This removes all rows but keeps the table structure.

# 4. SELECT Command

The SELECT command retrieves data from a table.

## Syntax

```sql
SELECT column1, column2
FROM table_name;
```


## Select All Columns

```sql
SELECT *
FROM students;
```


## Select Specific Columns

```sql
SELECT name, department
FROM students;
```


# Difference Between DDL and DML

| DDL                        | DML                    |
| -------------------------- | ---------------------- |
| Defines database structure | Manipulates data       |
| Works on schema objects    | Works on records       |
| Auto commit in many DBMS   | Requires commit        |
| CREATE, ALTER, DROP        | INSERT, UPDATE, DELETE |


# Difference Between DELETE, DROP, and TRUNCATE

| DELETE            | DROP                 | TRUNCATE          |
| ----------------- | -------------------- | ----------------- |
| Removes rows      | Removes entire table | Removes all rows  |
| Structure remains | Structure removed    | Structure remains |
| Can use WHERE     | No WHERE             | No WHERE          |
| Slower            | Fast                 | Very fast         |

---

# TCL (Transaction Control Language)

TCL commands are used to manage transactions in a database.

They help maintain data consistency and integrity.

# Types of TCL Commands

1. COMMIT
2. ROLLBACK
3. SAVEPOINT
4. SET TRANSACTION


# 1. COMMIT Command

The COMMIT command permanently saves all changes made during the current transaction.

## Syntax

```sql
COMMIT;
```


## Example

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


# 2. ROLLBACK Command

The ROLLBACK command undoes changes made during the current transaction.


## Syntax

```sql
ROLLBACK;
```

## Example

```sql
BEGIN;

DELETE FROM employees
WHERE emp_id = 5;

ROLLBACK;
```

The deleted row will be restored.


# 3. SAVEPOINT Command

SAVEPOINT creates a temporary point inside a transaction.

You can rollback to that point without rolling back the entire transaction.


## Syntax

```sql
SAVEPOINT savepoint_name;
```


## Example

```sql
BEGIN;

INSERT INTO employees VALUES (1, 'John', 50000, 'HR');

SAVEPOINT sp1;

INSERT INTO employees VALUES (2, 'Alice', 60000, 'IT');

ROLLBACK TO sp1;

COMMIT;
```

Only the first insert remains.


# 4. SET TRANSACTION Command

Used to set transaction properties.


## Example

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

---

# DCL (Data Control Language)

DCL commands are used to control user permissions and access.

These commands are mainly used by database administrators.

# Types of DCL Commands

1. GRANT
2. REVOKE


# 1. GRANT Command

The GRANT command gives privileges to users.


## Syntax

```sql
GRANT privilege_name
ON table_name
TO user_name;
```


## Example

```sql
GRANT SELECT, INSERT
ON employees
TO user1;
```

This allows user1 to:

* Read data
* Insert data

# Common Privileges

* SELECT
* INSERT
* UPDATE
* DELETE
* ALL PRIVILEGES


# 2. REVOKE Command

The REVOKE command removes privileges from users.


## Syntax

```sql
REVOKE privilege_name
ON table_name
FROM user_name;
```

## Example

```sql
REVOKE INSERT
ON employees
FROM user1;
```

This removes INSERT permission from user1.


# DQL (Data Query Language)

DQL is used to retrieve data from databases.

The main DQL command is:

* SELECT


# SELECT Command

The SELECT command retrieves data from tables.

## Syntax

```sql
SELECT column1, column2
FROM table_name;
```


## Example

```sql
SELECT name, salary
FROM employees;
```


# SELECT with WHERE

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```


# SELECT with ORDER BY

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```


# SELECT with GROUP BY

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```