# 1. Aggregations in SQL

Aggregation functions perform calculations on multiple rows and return a single value.

# Common Aggregate Functions

1. COUNT()
2. SUM()
3. AVG()
4. MAX()
5. MIN()

# Sample Employee Table

| employee_id | department | salary |
| ----------- | ---------- | ------ |
| 1           | HR         | 40000  |
| 2           | IT         | 60000  |
| 3           | IT         | 70000  |
| 4           | HR         | 50000  |
| 5           | Sales      | 45000  |


# 1. COUNT()

Counts rows.

## Example

```sql
SELECT COUNT(*) AS total_employees
FROM employees;
```


## Output

| total_employees |
| --------------- |
| 5               |


# 2. SUM()

Calculates total value.

## Example

```sql
SELECT SUM(salary) AS total_salary
FROM employees;
```


## Output

| total_salary |
| ------------ |
| 265000       |



# 3. AVG()

Calculates average value.

## Example

```sql
SELECT AVG(salary) AS average_salary
FROM employees;
```


## Output

| average_salary |
| -------------- |
| 53000          |


# 4. MAX()

Returns highest value.

## Example

```sql
SELECT MAX(salary) AS highest_salary
FROM employees;
```


## Output

| highest_salary |
| -------------- |
| 70000          |


# 5. MIN()

Returns lowest value.

## Example

```sql
SELECT MIN(salary) AS lowest_salary
FROM employees;
```


## Output

| lowest_salary |
| ------------- |
| 40000         |

# GROUP BY

Groups rows with the same values.

## Example

```sql
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

## Output

| department | employee_count |
| ---------- | -------------- |
| HR         | 2              |
| IT         | 2              |
| Sales      | 1              |


# GROUP BY with SUM()

```sql
SELECT department, SUM(salary) AS total_salary
FROM employees
GROUP BY department;
```

## Output

| department | total_salary |
| ---------- | ------------ |
| HR         | 90000        |
| IT         | 130000       |
| Sales      | 45000        |



# 2. Filters in SQL

Filters are used to retrieve specific rows.

# WHERE Clause

Filters rows before grouping.

## Example

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

## Output

| employee_id | department | salary |
| ----------- | ---------- | ------ |
| 2           | IT         | 60000  |
| 3           | IT         | 70000  |

# WHERE with AND

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 65000;
```
# WHERE with OR

```sql
SELECT *
FROM employees
WHERE department = 'HR'
OR department = 'Sales';
```


# WHERE with BETWEEN

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 40000 AND 60000;
```

# WHERE with IN

```sql
SELECT *
FROM employees
WHERE department IN ('HR', 'IT');
```

# WHERE with LIKE

```sql
SELECT *
FROM employees
WHERE department LIKE 'I%';
```

# HAVING Clause

Filters grouped data after GROUP BY.

## Example

```sql
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```
## Output

| department | avg_salary |
| ---------- | ---------- |
| IT         | 65000      |


# WHERE vs HAVING

| Feature                     | WHERE           | HAVING       |
| --------------------------- | --------------- | ------------ |
| Filters                     | Individual rows | Grouped rows |
| Used Before GROUP BY        | Yes             | No           |
| Used After GROUP BY         | No              | Yes          |
| Aggregate Functions Allowed | No              | Yes          |


# ORDER BY

Used to sort results.

## Ascending Order

```sql
SELECT *
FROM employees
ORDER BY salary ASC;
```

## Descending Order

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

# LIMIT Clause

Restricts number of rows returned.

## Example

```sql
SELECT *
FROM employees
LIMIT 3;
```