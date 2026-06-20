# Django Models and Python Concepts

# 1. What is models.py in Django?

The `models.py` file is used to define the structure of the database.

A Django model represents a database table.

Each model:

* Creates a table in the database
* Defines columns using fields
* Allows data insertion, update, deletion, and retrieval

Example:

```python
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=100)
    age = models.IntegerField()
```

Database Table:

| id | name | age |
| -- | ---- | --- |
| 1  | Sri  | 21  |
| 2  | John | 22  |

Here:

* `Student` → Table
* `name`, `age` → Columns
* Each record → Row



## Why Do We Use Models?

Without models:

```sql
CREATE TABLE student (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT
);
```

With Django:

```python
class Student(models.Model):
    name = models.CharField(max_length=100)
    age = models.IntegerField()
```

Django automatically creates SQL queries behind the scenes.

This is called:

```text
ORM (Object Relational Mapping)
```


## Example Model

```python
from django.db import models

class Employee(models.Model):
    first_name = models.CharField(max_length=50)
    last_name = models.CharField(max_length=50)
    salary = models.DecimalField(max_digits=10, decimal_places=2)

    def __str__(self):
        return self.first_name
```

After migration:

```bash
python manage.py makemigrations
python manage.py migrate
```

Django creates the corresponding database table.


# 2. What is on_delete?

When two tables are connected using a Foreign Key, Django must know what to do if the parent record is deleted.

Example:

```python
class Department(models.Model):
    name = models.CharField(max_length=100)

class Employee(models.Model):
    department = models.ForeignKey(
        Department,
        on_delete=models.CASCADE
    )
```

Question:

What happens if a Department is deleted?

Answer depends on the `on_delete` option.



# 3. What is CASCADE?

```python
on_delete=models.CASCADE
```

Meaning:

If the parent record is deleted, all related child records are also deleted.

Example:

Department Table

| id | name |
| -- | ---- |
| 1  | HR   |

Employee Table

| id | name | department_id |
| -- | ---- | ------------- |
| 1  | Sri  | 1             |
| 2  | John | 1             |

Delete Department:

```python
Department.objects.get(id=1).delete()
```

Result:

Department Table

(empty)

Employee Table

(empty)

All related employees are automatically deleted.


## Real-Life Example

```text
Department
    ↓
Employees
```

If the department no longer exists, employees belonging to that department may also be removed.

This is called:

```text
Cascade Delete
```


## Other on_delete Options

## PROTECT

```python
on_delete=models.PROTECT
```

Prevents deletion of parent record if children exist.

Example:

```python
department.delete()
```

Error:

```text
ProtectedError
```

Use when data must not be accidentally deleted.


## SET_NULL

```python
department = models.ForeignKey(
    Department,
    on_delete=models.SET_NULL,
    null=True
)
```

When department is deleted:

Before:

| Employee | Department |
| -------- | ---------- |
| Sri      | HR         |

After:

| Employee | Department |
| -------- | ---------- |
| Sri      | NULL       |

Employee remains.

Department reference becomes NULL.


## SET_DEFAULT

```python
department = models.ForeignKey(
    Department,
    on_delete=models.SET_DEFAULT,
    default=1
)
```

Assigns a default department.


## DO_NOTHING

```python
on_delete=models.DO_NOTHING
```

Django does nothing.

Can cause database integrity errors.

Rarely used.


## RESTRICT

```python
on_delete=models.RESTRICT
```

Prevents deletion if dependent records exist.

Similar to PROTECT.


# 4. Understanding Django Fields

Fields define what type of data can be stored in a database column.


## CharField

Stores text.

```python
name = models.CharField(max_length=100)
```

Examples:

```text
Sri
John
Django
```

Must specify:

```python
max_length
```


## TextField

Stores large text.

```python
description = models.TextField()
```

Examples:

* Blog content
* Articles
* Comments


## IntegerField

Stores whole numbers.

```python
age = models.IntegerField()
```

Examples:

```text
10
50
100
```


## FloatField

Stores decimal values.

```python
price = models.FloatField()
```

Example:

```text
99.99
10.5
```


## DecimalField

Used for accurate decimal calculations.

```python
salary = models.DecimalField(
    max_digits=10,
    decimal_places=2
)
```

Best for:

* Money
* Financial calculations


## BooleanField

Stores:

```python
True
False
```

Example:

```python
is_active = models.BooleanField(default=True)
```


## DateField

Stores dates.

```python
dob = models.DateField()
```

Example:

```text
2026-06-20
```


## TimeField

Stores time.

```python
start_time = models.TimeField()
```

Example:

```text
09:30:00
```


## DateTimeField

Stores both date and time.

```python
created_at = models.DateTimeField(auto_now_add=True)
```

Example:

```text
2026-06-20 09:30:15
```


## EmailField

Stores email addresses.

```python
email = models.EmailField()
```

Django validates email format.


## URLField

Stores URLs.

```python
website = models.URLField()
```

Example:

```text
https://example.com
```


## ImageField

Stores image files.

```python
profile_pic = models.ImageField(
    upload_to="images/"
)
```

Requires:

```bash
pip install pillow
```


## FileField

Stores files.

```python
resume = models.FileField(
    upload_to="files/"
)
```


## ForeignKey

Represents Many-to-One relationship.

```python
department = models.ForeignKey(
    Department,
    on_delete=models.CASCADE
)
```

Many Employees → One Department


## OneToOneField

Represents One-to-One relationship.

```python
user = models.OneToOneField(
    User,
    on_delete=models.CASCADE
)
```

One User → One Profile



## ManyToManyField

Represents Many-to-Many relationship.

```python
courses = models.ManyToManyField(Course)
```

Many Students ↔ Many Courses



# 5. What are Validators?

Validators check whether data is valid before saving it.

Example:

```python
from django.core.validators import MinValueValidator

age = models.IntegerField(
    validators=[MinValueValidator(18)]
)
```

Age below 18:

```text
Validation Error
```


## Common Validators

## MinValueValidator

```python
MinValueValidator(1)
```

Minimum value allowed.


## MaxValueValidator

```python
MaxValueValidator(100)
```

Maximum value allowed.


## MinLengthValidator

```python
MinLengthValidator(5)
```

Minimum text length.


## MaxLengthValidator

```python
MaxLengthValidator(50)
```

Maximum text length.


## EmailValidator

```python
EmailValidator()
```

Checks email format.


## URLValidator

```python
URLValidator()
```

Checks URL format.


## RegexValidator

```python
RegexValidator(
    regex=r'^[0-9]{10}$'
)
```

Used for phone number validation.

Example:

```text
9876543210
```

Valid.

```text
98765
```

Invalid.


# Custom Validator Example

```python
from django.core.exceptions import ValidationError

def validate_even(value):
    if value % 2 != 0:
        raise ValidationError(
            "Only even numbers allowed"
        )
```

Usage:

```python
number = models.IntegerField(
    validators=[validate_even]
)
```


# 6. Python Module vs Python Class

This is a very common interview question.


## What is a Module?

A module is simply a Python file.

Example:

```text
math_utils.py
```

```python
def add(a, b):
    return a + b
```

Usage:

```python
import math_utils

math_utils.add(5, 3)
```

Output:

```text
8
```

A module is used to organize code.


## What is a Class?

A class is a blueprint for creating objects.

Example:

```python
class Student:
    def __init__(self, name):
        self.name = name
```

Create object:

```python
s1 = Student("Sri")
```

Output:

```python
s1.name
```

```text
Sri
```

Class is used to represent real-world entities.

