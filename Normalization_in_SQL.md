# Database Normalization in SQL

# 1. Introduction to Normalization

Normalization is the process of organizing data in a database to:

* Reduce data redundancy
* Improve data consistency
* Avoid anomalies
* Improve database structure

Normalization divides large tables into smaller related tables and establishes relationships between them.


# Why Normalization is Important

Without normalization:

* Duplicate data increases storage usage
* Updating data becomes difficult
* Data inconsistencies occur
* Insert/Delete/Update anomalies appear


# Goals of Normalization

1. Eliminate duplicate data
2. Maintain data integrity
3. Organize data efficiently
4. Improve scalability


# Types of Anomalies

# 1. Insert Anomaly

Occurs when data cannot be inserted without additional unnecessary data.

## Example

You cannot add a course unless a student enrolls in it.


# 2. Update Anomaly

Occurs when the same data is repeated in multiple rows.

## Example

Changing a department name requires updating many rows.

# 3. Delete Anomaly

Occurs when deleting one record unintentionally removes other important data.

## Example

Deleting the last student from a course removes course information.


# Example of Unnormalized Table

| student_id | student_name | course | instructor | instructor_phone |
| ---------- | ------------ | ------ | ---------- | ---------------- |
| 1          | Sri          | DBMS   | Kumar      | 9876543210       |
| 1          | Sri          | SQL    | Ravi       | 8765432109       |
| 2          | Anu          | DBMS   | Kumar      | 9876543210       |

Problems:

* Instructor details are repeated
* Data redundancy exists
* Update anomaly may occur


# Normal Forms

1. First Normal Form (1NF)
2. Second Normal Form (2NF)
3. Third Normal Form (3NF)
4. Boyce-Codd Normal Form (BCNF)
5. Fourth Normal Form (4NF)
6. Fifth Normal Form (5NF)


# 1NF — First Normal Form

A table is in 1NF if:

* Each column contains atomic values
* No repeating groups exist
* Each row is unique


# Example Before 1NF

| student_id | student_name | phone_numbers |
| ---------- | ------------ | ------------- |
| 1          | Sri          | 9876, 8765    |
| 2          | Ravi         | 7654          |

Problem:

* Multiple values exist in one column.

# Convert to 1NF

| student_id | student_name | phone_number |
| ---------- | ------------ | ------------ |
| 1          | Sri          | 9876         |
| 1          | Sri          | 8765         |
| 2          | Ravi         | 7654         |


# SQL Example

```sql
CREATE TABLE students_1nf (
    student_id INT,
    student_name VARCHAR(50),
    phone_number VARCHAR(15)
);
```

# Advantages of 1NF

* Eliminates repeating groups
* Easier data retrieval
* Better organization


# 2NF — Second Normal Form

A table is in 2NF if:

* It is already in 1NF
* No partial dependency exists
* Non-key attributes depend on the whole primary key


# Partial Dependency

Occurs when a non-key attribute depends only on part of a composite key.


# Example Before 2NF

## Student_Course Table

| student_id | course_id | student_name | course_name |
| ---------- | --------- | ------------ | ----------- |
| 1          | C1        | Sri          | DBMS        |
| 1          | C2        | Sri          | SQL         |
| 2          | C1        | Ravi         | DBMS        |

Primary Key = (student_id, course_id)

Problems:

* student_name depends only on student_id
* course_name depends only on course_id

This causes partial dependency.


# Convert to 2NF

## Students Table

| student_id | student_name |
| ---------- | ------------ |
| 1          | Sri          |
| 2          | Ravi         |


## Courses Table

| course_id | course_name |
| --------- | ----------- |
| C1        | DBMS        |
| C2        | SQL         |


## Student_Course Table

| student_id | course_id |
| ---------- | --------- |
| 1          | C1        |
| 1          | C2        |
| 2          | C1        |


# SQL Example

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50)
);

CREATE TABLE courses (
    course_id VARCHAR(10) PRIMARY KEY,
    course_name VARCHAR(50)
);

CREATE TABLE student_course (
    student_id INT,
    course_id VARCHAR(10),
    PRIMARY KEY(student_id, course_id),
    FOREIGN KEY(student_id) REFERENCES students(student_id),
    FOREIGN KEY(course_id) REFERENCES courses(course_id)
);
```

# Advantages of 2NF

* Removes partial dependency
* Reduces redundancy
* Improves consistency


# 3NF — Third Normal Form

A table is in 3NF if:

* It is already in 2NF
* No transitive dependency exists

# Transitive Dependency

Occurs when a non-key attribute depends on another non-key attribute.

# Example Before 3NF

| employee_id | employee_name | department_id | department_name |
| ----------- | ------------- | ------------- | --------------- |
| 1           | Sri           | D1            | HR              |
| 2           | Ravi          | D2            | IT              |

Problems:

* department_name depends on department_id
* department_id depends on employee_id indirectly

This creates transitive dependency.


# Convert to 3NF

## Employees Table

| employee_id | employee_name | department_id |
| ----------- | ------------- | ------------- |
| 1           | Sri           | D1            |
| 2           | Ravi          | D2            |


## Departments Table

| department_id | department_name |
| ------------- | --------------- |
| D1            | HR              |
| D2            | IT              |


# SQL Example

```sql
CREATE TABLE departments (
    department_id VARCHAR(10) PRIMARY KEY,
    department_name VARCHAR(50)
);

CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(50),
    department_id VARCHAR(10),
    FOREIGN KEY(department_id)
    REFERENCES departments(department_id)
);
```

# Advantages of 3NF

* Removes transitive dependency
* Better data integrity
* Easier updates

# BCNF — Boyce-Codd Normal Form

BCNF is an advanced version of 3NF.

A table is in BCNF if:

* For every functional dependency,
  the determinant must be a candidate key.


# Example

| teacher | subject | classroom |
| ------- | ------- | --------- |
| Kumar   | DBMS    | R1        |
| Ravi    | SQL     | R2        |

Assumptions:

* One teacher teaches one subject
* One subject has one classroom

Functional Dependencies:

```text
teacher → subject
subject → classroom
```

Problem:

* subject is not a candidate key
* Violates BCNF


# Convert to BCNF

## Teacher_Subject Table

| teacher | subject |
| ------- | ------- |
| Kumar   | DBMS    |
| Ravi    | SQL     |

## Subject_Classroom Table

| subject | classroom |
| ------- | --------- |
| DBMS    | R1        |
| SQL     | R2        |


# 4NF — Fourth Normal Form

A table is in 4NF if:

* It is in BCNF
* No multi-valued dependency exists

# Example Before 4NF

| student | hobby | language |
| ------- | ----- | -------- |
| Sri     | Music | English  |
| Sri     | Dance | English  |
| Sri     | Music | Hindi    |
| Sri     | Dance | Hindi    |

Problems:

* Hobbies and languages are independent.
* Causes unnecessary combinations.


# Convert to 4NF

## Student_Hobby Table

| student | hobby |
| ------- | ----- |
| Sri     | Music |
| Sri     | Dance |


## Student_Language Table

| student | language |
| ------- | -------- |
| Sri     | English  |
| Sri     | Hindi    |


# 5NF — Fifth Normal Form

A table is in 5NF if:

* It is in 4NF
* No join dependency exists

5NF is used in very complex databases.


# Functional Dependency

A functional dependency occurs when:

```text
A → B
```

Meaning:

* Attribute A uniquely determines attribute B.

# Types of Functional Dependency

## 1. Full Functional Dependency

Entire primary key determines attribute.

## 2. Partial Dependency

Part of primary key determines attribute.

## 3. Transitive Dependency

Non-key attribute determines another non-key attribute.

# Candidate Key

A candidate key is:

* A minimal set of columns that uniquely identify a row.

Example:

```text
Student_ID
Email
```

Both can uniquely identify students.

# Primary Key

A primary key is:

* The candidate key selected to identify records uniquely.


# Foreign Key

A foreign key:

* Creates relationship between tables.

Example:

```sql
FOREIGN KEY(department_id)
REFERENCES departments(department_id)
```

# Advantages of Normalization

1. Reduces data redundancy
2. Improves consistency
3. Saves storage space
4. Easier maintenance
5. Prevents anomalies
6. Better database structure


# Disadvantages of Normalization

1. More tables are created
2. Complex joins may reduce performance
3. Query writing becomes harder
4. High normalization may impact speed

# Denormalization

Denormalization is the process of combining normalized tables to improve read performance.

Used in:

* Data warehouses
* Analytics systems
* Reporting systems


# Normalization vs Denormalization

| Feature        | Normalization | Denormalization |
| -------------- | ------------- | --------------- |
| Redundancy     | Low           | High            |
| Performance    | Slower reads  | Faster reads    |
| Data Integrity | High          | Moderate        |
| Storage Usage  | Low           | High            |
| Complexity     | More joins    | Fewer joins     |
