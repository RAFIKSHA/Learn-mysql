# SQL Triggers – Complete Step-by-Step Teaching Flow (Beginner to Advanced)


---

# Module 1: Creating a Table

## Create Students Table

```sql
CREATE TABLE students(
    student_id INT PRIMARY KEY,
    name VARCHAR(50),
    course VARCHAR(50),
    fees INT
);
```

---

## Understanding the Code

| Keyword      | Meaning                         |
| ------------ | ------------------------------- |
| CREATE TABLE | Creates a new table             |
| students     | Table name                      |
| student_id   | Column name                     |
| INT          | Integer data type               |
| PRIMARY KEY  | Unique identifier for each row  |
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

## Insert a Single Record

```sql
INSERT INTO students
VALUES(101,'Rafik','Python',5000);
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

## Update Course

```sql
UPDATE students
SET course='Data Science'
WHERE student_id=101;
```

---

### Before Update

| student_id | name  | course |
| ---------- | ----- | ------ |
| 101        | Rafik | Python |

---

### After Update

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

---

# Module 4: DELETE Operation

## Delete a Record

```sql
DELETE FROM students
WHERE student_id=104;
```

---

### Before Delete

| student_id | name |
| ---------- | ---- |
| 104        | Aman |

---

### After Delete

The record is removed from the table.

---

# Module 5: Creating a Log Table

Now we create a table that will store activity logs.

```sql
CREATE TABLE student_logs(
    log_id INT AUTO_INCREMENT PRIMARY KEY,
    message VARCHAR(255)
);
```

---

## View Log Table

```sql
SELECT * FROM student_logs;
```

### Output

```text
Empty Set
```

---

# Module 6: Understanding the Problem

Suppose a new student is added.

```sql
INSERT INTO students
VALUES(105,'Sana','AI',9000);
```

The student is successfully inserted.

But how does the administrator know that a new student was added?

Without a Trigger, we must manually insert a log record.

```sql
INSERT INTO student_logs(message)
VALUES('New Student Added');
```

---

### Problem

```text
Student Table Updated
        ↓
Developer manually inserts log
        ↓
May forget to do it
```

This problem is solved using Triggers.

---

# Module 7: What is a Trigger?

### Definition

A **Trigger** is a database object that automatically executes when an INSERT, UPDATE, or DELETE event occurs on a table.

---

# Module 8: Creating the First Trigger

```sql
CREATE TRIGGER trg_insert AFTER INSERT ON students FOR EACH ROW BEGIN INSERT INTO student_logs(message) VALUES('Student Added'); END
```

---

# Understanding Each Line

### CREATE TRIGGER

```sql
CREATE TRIGGER
```

Creates a trigger.

---

### Trigger Name

```sql
trg_insert
```

Name of the trigger.

---

### Event Timing

```sql
AFTER INSERT
```

Execute the trigger after data is inserted.

---

### Target Table

```sql
ON students
```

The trigger is attached to the students table.

---

### FOR EACH ROW

```sql
FOR EACH ROW
```

Execute the trigger for every inserted row.

---

### Action

```sql
INSERT INTO student_logs
```

Insert a record into the log table.

---

# Testing the Trigger

```sql
INSERT INTO students
VALUES(106,'Khan','MySQL',5000);
```

The database automatically executes:

```sql
INSERT INTO student_logs(message)
VALUES('Student Added');
```

---

## View Logs

```sql
SELECT * FROM student_logs;
```

### Output

| log_id | message       |
| ------ | ------------- |
| 1      | Student Added |

---

# Module 9: Understanding the NEW Keyword

Question:

How can we know which student was added?

The message "Student Added" does not provide enough information.

Use the **NEW** keyword.

---

## Improved Trigger

```sql
CREATE TRIGGER trg_insert
AFTER INSERT
ON students
FOR EACH ROW
INSERT INTO student_logs(message)
VALUES(
CONCAT(
'Student Added : ',
NEW.name
)
);
```

---

## Insert a Record

```sql
INSERT INTO students
VALUES(107,'Riya','ML',7000);
```

---

## Log Output

| log_id | message              |
| ------ | -------------------- |
| 2      | Student Added : Riya |

---

# What is NEW?

NEW represents the newly inserted row.

Inserted Row:

| student_id | name | course | fees |
| ---------- | ---- | ------ | ---- |
| 107        | Riya | ML     | 7000 |

---

Inside the Trigger:

```sql
NEW.student_id
```

Output:

```text
107
```

---

```sql
NEW.name
```

Output:

```text
Riya
```

---

```sql
NEW.course
```

Output:

```text
ML
```

---

```sql
NEW.fees
```

Output:

```text
7000
```

---

# Module 10: UPDATE Trigger

```sql
CREATE TRIGGER trg_update
AFTER UPDATE
ON students
FOR EACH ROW
INSERT INTO student_logs(message)
VALUES('Student Updated');
```

---

## Test the Trigger

```sql
UPDATE students
SET fees=10000
WHERE student_id=107;
```

---

### Log Output

```text
Student Updated
```

---

# Module 11: Understanding OLD and NEW

### Before Update

| fees |
| ---- |
| 7000 |

---

### After Update

| fees  |
| ----- |
| 10000 |

---

Inside the Trigger:

```sql
OLD.fees
```

Output:

```text
7000
```

---

```sql
NEW.fees
```

Output:

```text
10000
```

---

# Advanced UPDATE Trigger

```sql
CREATE TRIGGER trg_fee_update
AFTER UPDATE
ON students
FOR EACH ROW
INSERT INTO student_logs(message)
VALUES(
CONCAT(
'Fees Changed From ',
OLD.fees,
' To ',
NEW.fees
)
);
```

---

### Output

```text
Fees Changed From 7000 To 10000
```

---

# Module 12: DELETE Trigger

```sql
CREATE TRIGGER trg_delete
AFTER DELETE
ON students
FOR EACH ROW
INSERT INTO student_logs(message)
VALUES(
CONCAT(
'Deleted Student : ',
OLD.name
)
);
```

---

## Delete a Record

```sql
DELETE FROM students
WHERE student_id=107;
```

---

### Log Output

```text
Deleted Student : Riya
```

---

# Why OLD is Used?

After deletion, the row no longer exists in the table.

Therefore:

```sql
OLD.name
```

still contains the deleted student's information.

---

# Trigger Types Summary

| Trigger Type  | OLD | NEW |
| ------------- | --- | --- |
| BEFORE INSERT | ❌   | ✅   |
| AFTER INSERT  | ❌   | ✅   |
| BEFORE UPDATE | ✅   | ✅   |
| AFTER UPDATE  | ✅   | ✅   |
| BEFORE DELETE | ✅   | ❌   |
| AFTER DELETE  | ✅   | ❌   |

---

# Recommended Teaching Flow

### Session 1: SQL Fundamentals

1. Create Table
2. Data Types
3. Primary Key
4. INSERT
5. SELECT

---

### Session 2: Data Modification

6. UPDATE
7. DELETE
8. WHERE Clause

---

### Session 3: Trigger Foundation

9. Create Log Table
10. Why Triggers Are Needed
11. Trigger Architecture

---

### Session 4: Trigger Implementation

12. AFTER INSERT Trigger
13. NEW Keyword
14. AFTER UPDATE Trigger
15. OLD vs NEW
16. AFTER DELETE Trigger

---

### Session 5: Advanced Concepts

17. BEFORE INSERT Trigger
18. BEFORE UPDATE Trigger
19. BEFORE DELETE Trigger
20. Audit Log Project

---

# Final Definition

**A Trigger is a database object that automatically executes a predefined set of SQL statements whenever an INSERT, UPDATE, or DELETE operation occurs on a table.** 🚀
