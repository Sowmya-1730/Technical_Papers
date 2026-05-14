# What is a Trigger?

A trigger is a stored database procedure that runs automatically when certain events occur.

Events include:

* INSERT
* UPDATE
* DELETE

Triggers are associated with:

* Tables
* Views


# Real-World Example

## Banking System

Suppose:

* Every money transfer must be logged.

Instead of manually inserting logs:

* A trigger automatically stores transaction history.

# Why Triggers are Important

Triggers help in:

1. Automating repetitive tasks
2. Maintaining consistency
3. Tracking data changes
4. Improving security
5. Enforcing business rules

# How Triggers Work

When a specified database event occurs:

1. Trigger automatically activates
2. Trigger executes predefined SQL statements
3. Database operation continues


# Basic Trigger Syntax

```sql
CREATE TRIGGER trigger_name
BEFORE | AFTER | INSTEAD OF
INSERT | UPDATE | DELETE
ON table_name
FOR EACH ROW
EXECUTE FUNCTION function_name();
```

# Trigger Timing Types

1. BEFORE Trigger
2. AFTER Trigger
3. INSTEAD OF Trigger



# 1. BEFORE Trigger

# Definition

BEFORE trigger executes before the actual database operation.

# Uses

* Data validation
* Data modification before insert/update
* Preventing invalid operations

# Example

```sql
CREATE OR REPLACE FUNCTION check_salary()
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.salary < 0 THEN
        RAISE EXCEPTION 'Salary cannot be negative';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

# Creating BEFORE Trigger

```sql
CREATE TRIGGER salary_validation
BEFORE INSERT OR UPDATE
ON employees
FOR EACH ROW
EXECUTE FUNCTION check_salary();
```

# Explanation

Before inserting or updating:

* Trigger checks salary value.
* Negative salaries are rejected.

# Advantages

1. Prevents invalid data
2. Maintains integrity
3. Useful for validation



# 2. AFTER Trigger

# Definition

AFTER trigger executes after database operation completes successfully.

# Uses

* Logging
* Auditing
* Notifications
* Maintaining history

# Example

## Audit Table

```sql
CREATE TABLE employee_audit (
    emp_id INT,
    action_time TIMESTAMP
);
```

# Trigger Function

```sql
CREATE OR REPLACE FUNCTION log_employee_insert()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO employee_audit
    VALUES (NEW.emp_id, NOW());

    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

# Creating AFTER Trigger

```sql
CREATE TRIGGER employee_insert_log
AFTER INSERT
ON employees
FOR EACH ROW
EXECUTE FUNCTION log_employee_insert();
```

# Explanation

Whenever new employee added:

* Trigger automatically stores audit record.

# Advantages

1. Automatic logging
2. Useful for auditing
3. Tracks database changes



# 3. INSTEAD OF Trigger

# Definition

INSTEAD OF trigger replaces the actual database operation.

Mostly used on:

* Views

# Uses

* Updating complex views
* Custom database behavior

# Example

```sql
CREATE TRIGGER update_view_trigger
INSTEAD OF UPDATE
ON employee_view
FOR EACH ROW
EXECUTE FUNCTION update_employee_view();
```

# Trigger Event Types

Triggers can execute on:

1. INSERT
2. UPDATE
3. DELETE

# INSERT Trigger

Executes when new row inserted.

# Example

```sql
AFTER INSERT
```


# UPDATE Trigger

Executes when row updated.

# Example

```sql
BEFORE UPDATE
```



# DELETE Trigger

Executes when row deleted.

# Example

```sql
AFTER DELETE
```

