# 1. SQL Joins

SQL Joins are used to combine rows from two or more tables based on a related column.

# Sample Tables

## Students Table

| student_id | name  |
| ---------- | ----- |
| 1          | Sri   |
| 2          | Ravi  |
| 3          | Anu   |
| 4          | Kiran |

## Marks Table

| student_id | subject | marks |
| ---------- | ------- | ----- |
| 1          | Math    | 95    |
| 2          | Science | 88    |
| 3          | English | 91    |
| 5          | Physics | 85    |


# Types of SQL Joins

1. INNER JOIN
2. LEFT JOIN
3. RIGHT JOIN
4. FULL OUTER JOIN
5. CROSS JOIN
6. SELF JOIN


# 1. INNER JOIN

Returns only matching rows from both tables.

## Syntax

```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;
```


## Example

```sql
SELECT students.name, marks.subject, marks.marks
FROM students
INNER JOIN marks
ON students.student_id = marks.student_id;
```

## Output

| name | subject | marks |
| ---- | ------- | ----- |
| Sri  | Math    | 95    |
| Ravi | Science | 88    |
| Anu  | English | 91    |


## Explanation

* Only records with matching `student_id` values appear.
* Student with ID 4 is excluded because no matching marks exist.
* Student with ID 5 is excluded because no matching student exists.


# 2. LEFT JOIN

Returns all rows from the left table and matching rows from the right table.

## Syntax

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;
```

## Example

```sql
SELECT students.name, marks.subject, marks.marks
FROM students
LEFT JOIN marks
ON students.student_id = marks.student_id;
```

## Output

| name  | subject | marks |
| ----- | ------- | ----- |
| Sri   | Math    | 95    |
| Ravi  | Science | 88    |
| Anu   | English | 91    |
| Kiran | NULL    | NULL  |

## Explanation

* All students are displayed.
* Kiran has no matching marks, so NULL values appear.


# 3. RIGHT JOIN

Returns all rows from the right table and matching rows from the left table.

## Syntax

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;
```

## Example

```sql
SELECT students.name, marks.subject, marks.marks
FROM students
RIGHT JOIN marks
ON students.student_id = marks.student_id;
```


## Output

| name | subject | marks |
| ---- | ------- | ----- |
| Sri  | Math    | 95    |
| Ravi | Science | 88    |
| Anu  | English | 91    |
| NULL | Physics | 85    |


## Explanation

* All rows from the Marks table are displayed.
* Since student ID 5 does not exist in Students table, NULL appears.

# 4. FULL OUTER JOIN

Returns all matching and non-matching rows from both tables.


## Syntax

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column_name = table2.column_name;
```

## Example

```sql
SELECT students.name, marks.subject, marks.marks
FROM students
FULL OUTER JOIN marks
ON students.student_id = marks.student_id;
```


## Output

| name  | subject | marks |
| ----- | ------- | ----- |
| Sri   | Math    | 95    |
| Ravi  | Science | 88    |
| Anu   | English | 91    |
| Kiran | NULL    | NULL  |
| NULL  | Physics | 85    |


## Explanation

* Includes matching and non-matching rows from both tables.


# 5. CROSS JOIN

Returns the Cartesian product of both tables.


## Syntax

```sql
SELECT columns
FROM table1
CROSS JOIN table2;
```


## Example

```sql
SELECT students.name, marks.subject
FROM students
CROSS JOIN marks;
```


## Explanation

* Every row from Students combines with every row from Marks.
* If Students has 4 rows and Marks has 4 rows, output contains 16 rows.


# 6. SELF JOIN

A table joins with itself.


## Employee Table

| employee_id | employee_name | manager_id |
| ----------- | ------------- | ---------- |
| 1           | Arun          | NULL       |
| 2           | Ravi          | 1          |
| 3           | Kiran         | 1          |


## Example

```sql
SELECT A.employee_name AS Employee,
       B.employee_name AS Manager
FROM employees A
JOIN employees B
ON A.manager_id = B.employee_id;
```


## Output

| Employee | Manager |
| -------- | ------- |
| Ravi     | Arun    |
| Kiran    | Arun    |
