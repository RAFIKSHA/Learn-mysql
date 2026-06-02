
---

# DDL (Data Definition Language)

DDL commands are used to create and modify database structures.

---

## 1. CREATE DATABASE

### What does it do?

Creates a new database named `college`.

### Query

```sql
CREATE DATABASE college;
```

### Output

```text
Query OK, 1 row affected
```

---

## 2. USE DATABASE

### What does it do?

Selects the `college` database so that all upcoming operations are performed inside it.

### Query

```sql
USE college;
```

### Output

```text
Database changed
```

---

## 3. CREATE TABLE

### What does it do?

Creates a new table named `students`.

* `student_id` → Unique ID for each student.
* `PRIMARY KEY` → Uniquely identifies each row.
* `AUTO_INCREMENT` → Automatically generates IDs.
* `NOT NULL` → Name cannot be empty.
* `UNIQUE` → Email cannot be duplicated.

### Query

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    age INT,
    email VARCHAR(100) UNIQUE
);
```

### Output

```text
Query OK, 0 rows affected
```

---

## 4. ALTER TABLE ADD COLUMN

### What does it do?

Adds a new column named `phone` to the existing students table.

### Before

| student_id | name  | age |
| ---------- | ----- | --- |
| 1          | Rahul | 20  |

### Query

```sql
ALTER TABLE students
ADD phone VARCHAR(15);
```

### After

| student_id | name  | age | phone |
| ---------- | ----- | --- | ----- |
| 1          | Rahul | 20  | NULL  |

---

## 5. ALTER TABLE MODIFY

### What does it do?

Changes the data type or size of an existing column.

### Query

```sql
ALTER TABLE students
MODIFY city VARCHAR(100);
```

### Explanation

The city column size increases from 50 characters to 100 characters.

---

## 6. DROP COLUMN

### What does it do?

Removes a specific column from the table permanently.

### Query

```sql
ALTER TABLE students
DROP COLUMN phone;
```

### Result

The `phone` column no longer exists.

---

# DML (Data Manipulation Language)

Used to insert, update, and delete records.

---

## 7. INSERT

### What does it do?

Adds a new student record into the table.

### Query

```sql
INSERT INTO students(name,age,email)
VALUES
('Rahul',20,'rahul@gmail.com');
```

### Before

| student_id | name |
| ---------- | ---- |
| Empty      |      |

### After

| student_id | name  |
| ---------- | ----- |
| 1          | Rahul |

---

## 8. UPDATE

### What does it do?

Modifies existing data in the table.

### Query

```sql
UPDATE students
SET city='Delhi'
WHERE student_id=1;
```

### Before

| student_id | city |
| ---------- | ---- |
| 1          | Pune |

### After

| student_id | city  |
| ---------- | ----- |
| 1          | Delhi |

---

## 9. DELETE

### What does it do?

Removes selected records from the table.

### Query

```sql
DELETE FROM students
WHERE student_id=1;
```

### Before

| student_id | name  |
| ---------- | ----- |
| 1          | Rahul |
| 2          | Priya |

### After

| student_id | name  |
| ---------- | ----- |
| 2          | Priya |

---

# DQL (Data Query Language)

Used to retrieve data.

---

## 10. SELECT

### What does it do?

Displays all records from the table.

### Query

```sql
SELECT * FROM students;
```

### Output

| student_id | name  |
| ---------- | ----- |
| 1          | Rahul |
| 2          | Priya |

---

## 11. WHERE

### What does it do?

Filters records based on a condition.

### Query

```sql
SELECT *
FROM students
WHERE age > 20;
```

### Output

Only students whose age is greater than 20 are displayed.

---

## 12. ORDER BY

### What does it do?

Sorts records in ascending or descending order.

### Query

```sql
SELECT *
FROM students
ORDER BY age DESC;
```

### Result

Students appear from highest age to lowest age.

---

## 13. LIMIT

### What does it do?

Restricts the number of rows returned.

### Query

```sql
SELECT *
FROM students
LIMIT 3;
```

### Result

Only the first 3 rows are displayed.

---

# TCL (Transaction Control Language)

Controls transactions.

---

## 14. START TRANSACTION

### What does it do?

Starts a transaction block.

### Query

```sql
START TRANSACTION;
```

---

## 15. COMMIT

### What does it do?

Permanently saves all changes made during the transaction.

### Query

```sql
COMMIT;
```

### Result

Changes cannot be undone using ROLLBACK.

---

## 16. ROLLBACK

### What does it do?

Cancels all changes made after the last transaction started.

### Query

```sql
ROLLBACK;
```

### Result

Database returns to the previous state.

---

## 17. SAVEPOINT

### What does it do?

Creates a checkpoint inside a transaction.

### Query

```sql
SAVEPOINT sp1;
```

### Result

You can return to this point using:

```sql
ROLLBACK TO sp1;
```

---

1. **Purpose**
2. **Syntax**
3. **Output**
4. **Before/After Effect**

sab clear ho jata hai. Ye training notes aur PPT dono ke liye ideal format hai.
