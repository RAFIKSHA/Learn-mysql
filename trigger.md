# SQL TRIGGERS – COMPLETE THEORY + PRACTICAL + OUTPUT FILE (MySQL)

---

# Module 1: Creating a Table

## What is a Table?

A table is a collection of rows and columns used to store related data.

Example:

| student_id | name  | course | fees |
| ---------- | ----- | ------ | ---- |
| 101        | Rafik | Python | 5000 |

---

## Create Database

```sql
CREATE DATABASE trigger_demo;
USE trigger_demo;
```

### Output

```text
Database changed
```

---

## Create Students Table

```sql
CREATE TABLE students(
    student_id INT PRIMARY KEY,
    name VARCHAR(50),
    course VARCHAR(50),
    fees INT
);
```

### Output

```text
Query OK, 0 rows affected
```

---

## Understanding the Code

| Keyword      | Meaning                         |
| ------------ | ------------------------------- |
| CREATE TABLE | Creates a new table             |
| students     | Table name                      |
| student_id   | Column name                     |
| INT          | Integer data type               |
| PRIMARY KEY  | Unique identifier               |
| VARCHAR(50)  | Stores text up to 50 characters |

---

## View Table Structure

```sql
DESC students;
```

### Output

| Field      | Type        |
| ---------- | ----------- |
| student_id | int         |
| name       | varchar(50) |
| course     | varchar(50) |
| fees       | int         |

---

# Module 2: INSERT Operation

## What is INSERT?

INSERT is used to add records into a table.

---

## Insert Single Record

```sql
INSERT INTO students
VALUES(101,'Rafik','Python',5000);
```

### Output

```text
Query OK, 1 row affected
```

---

## Insert Multiple Records

```sql
INSERT INTO students
VALUES
(102,'Ali','Java',6000),
(103,'Shah','SQL',4000),
(104,'Aman','Django',7000);
```

### Output

```text
Query OK, 3 rows affected
```

---

## View Data

```sql
SELECT * FROM students;
```

### Output

| student_id | name  | course | fees |
| ---------- | ----- | ------ | ---- |
| 101        | Rafik | Python | 5000 |
| 102        | Ali   | Java   | 6000 |
| 103        | Shah  | SQL    | 4000 |
| 104        | Aman  | Django | 7000 |

---

# Module 3: UPDATE Operation

## What is UPDATE?

Used to modify existing data.

---

## Update Course

```sql
UPDATE students
SET course='Data Science'
WHERE student_id=101;
```

### Output

```text
Query OK, 1 row affected
```

---

### Before Update

| student_id | name  | course |
| ---------- | ----- | ------ |
| 101        | Rafik | Python |

---

### After Update

```sql
SELECT * FROM students
WHERE student_id=101;
```

| student_id | name  | course       |
| ---------- | ----- | ------------ |
| 101        | Rafik | Data Science |

---

## Update Fees

```sql
UPDATE students
SET fees=8000
WHERE student_id=102;
```

### Output

```text
Query OK, 1 row affected
```

---

# Module 4: DELETE Operation

## What is DELETE?

DELETE removes records from a table.

---

## Delete Record

```sql
DELETE FROM students
WHERE student_id=104;
```

### Output

```text
Query OK, 1 row affected
```

---

## Verify

```sql
SELECT * FROM students;
```

### Output

| student_id | name  | course       | fees |
| ---------- | ----- | ------------ | ---- |
| 101        | Rafik | Data Science | 5000 |
| 102        | Ali   | Java         | 8000 |
| 103        | Shah  | SQL          | 4000 |

---

# Module 5: Create Log Table

## Why Log Table?

Stores all activities performed on students table.

---

```sql
CREATE TABLE student_logs(
    log_id INT AUTO_INCREMENT PRIMARY KEY,
    message VARCHAR(255)
);
```

### Output

```text
Query OK, 0 rows affected
```

---

## Check Logs

```sql
SELECT * FROM student_logs;
```

### Output

```text
Empty Set
```

---

# Module 6: Why Triggers?

Suppose a new student is inserted.

```sql
INSERT INTO students
VALUES(105,'Sana','AI',9000);
```

Student is added successfully.

But how will Administrator know?

Without Trigger:

```sql
INSERT INTO student_logs(message)
VALUES('Student Added');
```

Problem:

```text
Developer must remember to create logs manually.
Developer may forget.
```

Solution:

```text
TRIGGER
```

---

# Module 7: What is a Trigger?

## Definition

A Trigger is a database object that automatically executes when an INSERT, UPDATE, or DELETE operation occurs on a table.

---

## Trigger Architecture

```text
User Action
     ↓
INSERT / UPDATE / DELETE
     ↓
Trigger Fires Automatically
     ↓
Log Table Updated
```

---

# Module 8: AFTER INSERT Trigger

## Create Trigger

```sql
DROP TRIGGER IF EXISTS trg_insert;

DELIMITER $$

CREATE TRIGGER trg_insert
AFTER INSERT
ON students
FOR EACH ROW
BEGIN

    INSERT INTO student_logs(message)
    VALUES(
        CONCAT(
            'Student Added : ',
            NEW.name
        )
    );

END $$

DELIMITER ;
```

### Output

```text
Query OK
```

---

## Verify Trigger

```sql
SHOW TRIGGERS;
```

### Output

| Trigger    | Event  | Table    |
| ---------- | ------ | -------- |
| trg_insert | INSERT | students |

---

## Test Trigger

```sql
INSERT INTO students
VALUES(106,'Khan','MySQL',5000);
```

### Output

```text
Query OK, 1 row affected
```

---

## Check Students Table

```sql
SELECT * FROM students
WHERE student_id=106;
```

### Output

| student_id | name | course | fees |
| ---------- | ---- | ------ | ---- |
| 106        | Khan | MySQL  | 5000 |

---

## Check Logs

```sql
SELECT * FROM student_logs;
```

### Output

| log_id | message              |
| ------ | -------------------- |
| 1      | Student Added : Khan |

---

## NEW Keyword

NEW refers to the newly inserted row.

Inserted Row:

| student_id | name | course | fees |
| ---------- | ---- | ------ | ---- |
| 106        | Khan | MySQL  | 5000 |

Inside Trigger:

```sql
NEW.student_id
```

Output:

```text
106
```

```sql
NEW.name
```

Output:

```text
Khan
```

```sql
NEW.course
```

Output:

```text
MySQL
```

```sql
NEW.fees
```

Output:

```text
5000
```

---

# Module 9: AFTER UPDATE Trigger

## Create Trigger

```sql
DROP TRIGGER IF EXISTS trg_fee_update;

DELIMITER $$

CREATE TRIGGER trg_fee_update
AFTER UPDATE
ON students
FOR EACH ROW
BEGIN

    INSERT INTO student_logs(message)
    VALUES(
        CONCAT(
            'Fees Changed From ',
            OLD.fees,
            ' To ',
            NEW.fees
        )
    );

END $$

DELIMITER ;
```

### Output

```text
Query OK
```

---

## Test Trigger

```sql
UPDATE students
SET fees=10000
WHERE student_id=106;
```

### Output

```text
Query OK, 1 row affected
```

---

## Check Logs

```sql
SELECT * FROM student_logs;
```

### Output

| log_id | message                         |
| ------ | ------------------------------- |
| 1      | Student Added : Khan            |
| 2      | Fees Changed From 5000 To 10000 |

---

# Module 10: OLD vs NEW

### Before Update

| fees |
| ---- |
| 5000 |

---

### After Update

| fees  |
| ----- |
| 10000 |

---

### OLD Value

```sql
OLD.fees
```

Output:

```text
5000
```

---

### NEW Value

```sql
NEW.fees
```

Output:

```text
10000
```

---

## Visual Explanation

```text
Before Update

OLD.fees = 5000

      ↓ UPDATE

NEW.fees = 10000

After Update
```

---

# Module 11: AFTER DELETE Trigger

## Create Trigger

```sql
DROP TRIGGER IF EXISTS trg_delete;

DELIMITER $$

CREATE TRIGGER trg_delete
AFTER DELETE
ON students
FOR EACH ROW
BEGIN

    INSERT INTO student_logs(message)
    VALUES(
        CONCAT(
            'Deleted Student : ',
            OLD.name
        )
    );

END $$

DELIMITER ;
```

### Output

```text
Query OK
```

---

## Test Trigger

```sql
DELETE FROM students
WHERE student_id=106;
```

### Output

```text
Query OK, 1 row affected
```

---

## Check Students Table

```sql
SELECT * FROM students;
```

### Output

| student_id | name  | course       | fees |
| ---------- | ----- | ------------ | ---- |
| 101        | Rafik | Data Science | 5000 |
| 102        | Ali   | Java         | 8000 |
| 103        | Shah  | SQL          | 4000 |
| 105        | Sana  | AI           | 9000 |

---

## Check Logs

```sql
SELECT * FROM student_logs;
```

### Output

| log_id | message                         |
| ------ | ------------------------------- |
| 1      | Student Added : Khan            |
| 2      | Fees Changed From 5000 To 10000 |
| 3      | Deleted Student : Khan          |

---

## Why OLD?

After DELETE:

```text
Row no longer exists.
```

Therefore:

```sql
NEW.name
```

❌ Not Available

```sql
OLD.name
```

✅ Available

---

# Module 12: BEFORE INSERT Trigger

## Purpose

Validate data before insertion.

Example:

```text
Fees cannot be negative.
```

---

## Create Trigger

```sql
DROP TRIGGER IF EXISTS trg_before_insert;

DELIMITER $$

CREATE TRIGGER trg_before_insert
BEFORE INSERT
ON students
FOR EACH ROW
BEGIN

    IF NEW.fees < 0 THEN

        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT='Fees Cannot Be Negative';

    END IF;

END $$

DELIMITER ;
```

---

## Test

```sql
INSERT INTO students
VALUES(110,'Riya','ML',-5000);
```

### Output

```text
ERROR 1644 (45000):
Fees Cannot Be Negative
```

---

# Module 13: Trigger Types Summary

| Trigger Type  | OLD | NEW |
| ------------- | --- | --- |
| BEFORE INSERT | ❌   | ✅   |
| AFTER INSERT  | ❌   | ✅   |
| BEFORE UPDATE | ✅   | ✅   |
| AFTER UPDATE  | ✅   | ✅   |
| BEFORE DELETE | ✅   | ❌   |
| AFTER DELETE  | ✅   | ❌   |

---

# Complete End-to-End Test

```sql
INSERT INTO students
VALUES(201,'Rafik','Python',5000);

UPDATE students
SET fees=7000
WHERE student_id=201;

DELETE FROM students
WHERE student_id=201;

SELECT * FROM student_logs;
```

### Final Output

| log_id | message                         |
| ------ | ------------------------------- |
| 1      | Student Added : Khan            |
| 2      | Fees Changed From 5000 To 10000 |
| 3      | Deleted Student : Khan          |
| 4      | Student Added : Rafik           |
| 5      | Fees Changed From 5000 To 7000  |
| 6      | Deleted Student : Rafik         |

---

# Interview Questions

### What is a Trigger?

**A Trigger is a database object that automatically executes a predefined set of SQL statements whenever an INSERT, UPDATE, or DELETE operation occurs on a table.**

### Why Use Triggers?

1. Audit Logging
2. Data Validation
3. Security Rules
4. Automatic Calculations
5. Maintaining Data Integrity

### Difference Between OLD and NEW

| OLD                       | NEW                       |
| ------------------------- | ------------------------- |
| Previous value            | Updated/New value         |
| Used in UPDATE and DELETE | Used in INSERT and UPDATE |

---

# Real-Life Example

```text
ATM Transaction
      ↓
Money Withdrawn
      ↓
Trigger Fires
      ↓
Transaction Log Stored

Student Admission
      ↓
INSERT
      ↓
Trigger Fires
      ↓
Admission Log Stored
```

**Final Definition:**
**Trigger = Automatic SQL Event Handler inside the database.** 🚀
