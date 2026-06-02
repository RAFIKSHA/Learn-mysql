
# SQL VIEW – Complete Teaching Flow

## What is a View?

### Definition

A **View** is a virtual table created from one or more tables using a SQL query.

```text
Table → Physical Data Store
View  → Virtual Table
```

### Real Life Example

Maan lo Students table me 10 columns hain:

| student_id | name | email | phone | course | fees |
| ---------- | ---- | ----- | ----- | ------ | ---- |

Teacher ko sirf:

| name | course |
| ---- | ------ |

dekhna hai.

Har baar query likhne ki jagah View bana dete hain.

---

# Module 1: Create Table

```sql
CREATE TABLE students(
    student_id INT PRIMARY KEY,
    name VARCHAR(50),
    course VARCHAR(50),
    fees INT
);
```

---

# Module 2: Insert Data

```sql
INSERT INTO students VALUES
(101,'Rafik','Python',5000),
(102,'Ali','Java',6000),
(103,'Shah','SQL',4000),
(104,'Aman','Django',7000);
```

---

# View Data

```sql
SELECT * FROM students;
```

Output

| student_id | name  | course | fees |
| ---------- | ----- | ------ | ---- |
| 101        | Rafik | Python | 5000 |
| 102        | Ali   | Java   | 6000 |
| 103        | Shah  | SQL    | 4000 |
| 104        | Aman  | Django | 7000 |

---

# Module 3: Create First View

```sql
CREATE VIEW student_view AS
SELECT name, course
FROM students;
```

---

# Understanding Syntax

| Keyword      | Meaning        |
| ------------ | -------------- |
| CREATE VIEW  | Creates a view |
| student_view | View Name      |
| AS           | Defines query  |
| SELECT       | Data to show   |

---

# View Data from View

```sql
SELECT * FROM student_view;
```

Output

| name  | course |
| ----- | ------ |
| Rafik | Python |
| Ali   | Java   |
| Shah  | SQL    |
| Aman  | Django |

---

# How View Works?

```text
student_view
      ↓
SELECT name,course
FROM students
      ↓
Fetches data from students table
```

View data store nahi karta.

View actual table se data fetch karta hai.

---

# Module 4: Update Base Table

```sql
UPDATE students
SET course='Data Science'
WHERE student_id=101;
```

---

# Check View Again

```sql
SELECT * FROM student_view;
```

Output

| name  | course       |
| ----- | ------------ |
| Rafik | Data Science |

Automatically update ho gaya.

---

# Important Point

```text
View does not store data.
View always shows latest data from original table.
```

---

# Module 5: View with Condition

```sql
CREATE VIEW python_students AS
SELECT *
FROM students
WHERE course='Python';
```

---

# Execute

```sql
SELECT * FROM python_students;
```

Output

| student_id | name  | course | fees |
| ---------- | ----- | ------ | ---- |
| 101        | Rafik | Python | 5000 |

---

# Module 6: View with Multiple Tables

## Create Courses Table

```sql
CREATE TABLE courses(
    course_id INT PRIMARY KEY,
    course_name VARCHAR(50)
);
```

---

## Insert Data

```sql
INSERT INTO courses VALUES
(1,'Python'),
(2,'Java'),
(3,'SQL');
```

---

# Create Enrollment Table

```sql
CREATE TABLE enrollment(
    student_id INT,
    course_id INT
);
```

---

## Insert Data

```sql
INSERT INTO enrollment VALUES
(101,1),
(102,2),
(103,3);
```

---

# Create Join View

```sql
CREATE VIEW student_course_view AS
SELECT
s.name,
c.course_name
FROM students s
JOIN enrollment e
ON s.student_id=e.student_id
JOIN courses c
ON e.course_id=c.course_id;
```

---

# Execute

```sql
SELECT * FROM student_course_view;
```

Output

| name  | course_name |
| ----- | ----------- |
| Rafik | Python      |
| Ali   | Java        |
| Shah  | SQL         |

---

# Module 7: Replace View

```sql
CREATE OR REPLACE VIEW student_view AS
SELECT
name,
course,
fees
FROM students;
```

---

# Execute

```sql
SELECT * FROM student_view;
```

Now fees column bhi show hoga.

---

# Module 8: Delete View

```sql
DROP VIEW student_view;
```

---

# Check

```sql
SELECT * FROM student_view;
```

Output

```text
Error:
View does not exist
```

---

# Advantages of View

| Advantage        | Explanation                        |
| ---------------- | ---------------------------------- |
| Security         | Hide sensitive columns             |
| Simplicity       | Complex query ko simple banata hai |
| Reusability      | Same query baar-baar nahi likhni   |
| Data Abstraction | User ko limited data dikhana       |

---

# Interview Questions

### What is a View?

A virtual table created using a SQL query.

### Does View Store Data?

No.

### Can View be Updated?

Yes, simple views can be updated.

### Difference Between Table and View?

| Table           | View                |
| --------------- | ------------------- |
| Stores data     | Does not store data |
| Physical object | Virtual object      |
| Takes storage   | Very little storage |

---

# Final Definition

**A View is a virtual table based on the result of a SQL query. It does not store data itself but displays data from one or more underlying tables.**

learning order:

**Tables → SELECT → WHERE → JOIN → VIEW → INDEX → STORED PROCEDURE → TRIGGER**


