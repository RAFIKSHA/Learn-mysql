# 📚 MySQL Complete Practical Guide 

# Project: College Management System

---

# Module 1: Database Basics

## 1. Create Database

Database create karne ke liye use hota hai.

```sql
CREATE DATABASE college;
```

**Output**

```text
Query OK, 1 row affected
```

---

## 2. Show Databases

Server me available databases dekhne ke liye.

```sql
SHOW DATABASES;
```

**Output**

| Database           |
| ------------------ |
| college            |
| information_schema |
| mysql              |
| performance_schema |
| sys                |

---

## 3. Select Database

Kaam karne ke liye database choose karte hain.

```sql
USE college;
```

**Output**

```text
Database changed
```

---

# Module 2: Create Project Tables

## 4. Create Departments Table

```sql
CREATE TABLE departments (
    dept_id INT PRIMARY KEY AUTO_INCREMENT,
    dept_name VARCHAR(50) NOT NULL
);
```

**Output**

```text
Query OK, 0 rows affected
```

---

## 5. Create Courses Table

```sql
CREATE TABLE courses (
    course_id INT PRIMARY KEY AUTO_INCREMENT,
    course_name VARCHAR(100) NOT NULL,
    dept_id INT,
    FOREIGN KEY (dept_id)
    REFERENCES departments(dept_id)
);
```

**Output**

```text
Query OK, 0 rows affected
```

---

## 6. Create Students Table

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    age INT,
    email VARCHAR(100) UNIQUE,
    city VARCHAR(50) DEFAULT 'Pune',
    dept_id INT,
    FOREIGN KEY (dept_id)
    REFERENCES departments(dept_id)
);
```

**Output**

```text
Query OK, 0 rows affected
```

---

## 7. Create Marks Table

```sql
CREATE TABLE marks (
    mark_id INT PRIMARY KEY AUTO_INCREMENT,
    student_id INT,
    subject VARCHAR(50),
    marks INT,
    FOREIGN KEY (student_id)
    REFERENCES students(student_id)
);
```

**Output**

```text
Query OK, 0 rows affected
```

---

## 8. Show Tables

```sql
SHOW TABLES;
```

**Output**

| Tables_in_college |
| ----------------- |
| courses           |
| departments       |
| marks             |
| students          |

---

## 9. Describe Students Table

```sql
DESC students;
```

**Output**

| Field      | Type         | Null | Key |
| ---------- | ------------ | ---- | --- |
| student_id | int          | NO   | PRI |
| name       | varchar(100) | NO   |     |
| age        | int          | YES  |     |
| email      | varchar(100) | YES  | UNI |
| city       | varchar(50)  | YES  |     |
| dept_id    | int          | YES  | MUL |

---

# Module 3: Insert Data

## 10. Insert Departments

```sql
INSERT INTO departments(dept_name)
VALUES
('Computer Science'),
('Mechanical'),
('Electrical'),
('Civil');
```

**Output**

```text
Query OK, 4 rows affected
```

---

## 11. View Departments

```sql
SELECT * FROM departments;
```

**Output**

| dept_id | dept_name        |
| ------- | ---------------- |
| 1       | Computer Science |
| 2       | Mechanical       |
| 3       | Electrical       |
| 4       | Civil            |

---

## 12. Insert Courses

```sql
INSERT INTO courses(course_name,dept_id)
VALUES
('Database Systems',1),
('Data Structures',1),
('Thermodynamics',2),
('Machine Design',2),
('Circuit Analysis',3),
('Power Systems',3),
('Surveying',4);
```

**Output**

```text
Query OK, 7 rows affected
```

---

## 13. View Courses

```sql
SELECT * FROM courses;
```

**Output**

| course_id | course_name      | dept_id |
| --------- | ---------------- | ------- |
| 1         | Database Systems | 1       |
| 2         | Data Structures  | 1       |
| 3         | Thermodynamics   | 2       |
| 4         | Machine Design   | 2       |
| 5         | Circuit Analysis | 3       |
| 6         | Power Systems    | 3       |
| 7         | Surveying        | 4       |

---

## 14. Insert Students

```sql
INSERT INTO students(name,age,email,city,dept_id)
VALUES
('Rahul',20,'rahul@gmail.com','Pune',1),
('Priya',21,'priya@gmail.com','Mumbai',2),
('Aman',19,'aman@gmail.com','Nashik',1),
('Sneha',22,'sneha@gmail.com','Pune',3),
('Karan',23,'karan@gmail.com','Nagpur',1);
```

**Output**

```text
Query OK, 5 rows affected
```

---

## 15. View Students

```sql
SELECT * FROM students;
```

**Output**

| student_id | name  | age | city   | dept_id |
| ---------- | ----- | --- | ------ | ------- |
| 1          | Rahul | 20  | Pune   | 1       |
| 2          | Priya | 21  | Mumbai | 2       |
| 3          | Aman  | 19  | Nashik | 1       |
| 4          | Sneha | 22  | Pune   | 3       |
| 5          | Karan | 23  | Nagpur | 1       |

---

## 16. Insert Marks

```sql
INSERT INTO marks(student_id,subject,marks)
VALUES
(1,'DBMS',85),
(1,'Python',90),
(2,'DBMS',75),
(3,'DBMS',65),
(4,'DBMS',95);
```

**Output**

```text
Query OK, 5 rows affected
```

---

## 17. View Marks

```sql
SELECT * FROM marks;
```

**Output**

| mark_id | student_id | subject | marks |
| ------- | ---------- | ------- | ----- |
| 1       | 1          | DBMS    | 85    |
| 2       | 1          | Python  | 90    |
| 3       | 2          | DBMS    | 75    |
| 4       | 3          | DBMS    | 65    |
| 5       | 4          | DBMS    | 95    |

---

# Module 4: Basic Queries

## 18. Select All Students

```sql
SELECT * FROM students;
```

**Output**

5 student records display honge.

---

## 19. Select Specific Columns

```sql
SELECT name, age
FROM students;
```

**Output**

| name  | age |
| ----- | --- |
| Rahul | 20  |
| Priya | 21  |
| Aman  | 19  |
| Sneha | 22  |
| Karan | 23  |

---

## 20. DISTINCT Cities

```sql
SELECT DISTINCT city
FROM students;
```

**Output**

| city   |
| ------ |
| Pune   |
| Mumbai |
| Nashik |
| Nagpur |

---
# 📚 MySQL Complete Practical Guide with Expected Output

# Part 2 (Query 21–40)

---

# Module 5: WHERE Conditions

## 21. Students Age Greater Than 20

```sql id="q1ap8m"
SELECT *
FROM students
WHERE age > 20;
```

**Output**

| student_id | name  | age |
| ---------- | ----- | --- |
| 2          | Priya | 21  |
| 4          | Sneha | 22  |
| 5          | Karan | 23  |

---

## 22. Students Age Less Than 22

```sql id="n6q28s"
SELECT *
FROM students
WHERE age < 22;
```

**Output**

| student_id | name  | age |
| ---------- | ----- | --- |
| 1          | Rahul | 20  |
| 2          | Priya | 21  |
| 3          | Aman  | 19  |

---

## 23. Students From Department 1

```sql id="xy0g4k"
SELECT *
FROM students
WHERE dept_id = 1;
```

**Output**

| student_id | name  |
| ---------- | ----- |
| 1          | Rahul |
| 3          | Aman  |
| 5          | Karan |

---

## 24. AND Operator

```sql id="y7r4fj"
SELECT *
FROM students
WHERE age > 20
AND dept_id = 1;
```

**Output**

| student_id | name  | age |
| ---------- | ----- | --- |
| 5          | Karan | 23  |

---

## 25. OR Operator

```sql id="t5x9r3"
SELECT *
FROM students
WHERE dept_id = 1
OR dept_id = 2;
```

**Output**

| name  |
| ----- |
| Rahul |
| Priya |
| Aman  |
| Karan |

---

## 26. NOT Operator

```sql id="kg0gop"
SELECT *
FROM students
WHERE NOT dept_id = 1;
```

**Output**

| name  |
| ----- |
| Priya |
| Sneha |

---

## 27. IN Operator

```sql id="tca35j"
SELECT *
FROM students
WHERE dept_id IN(1,3);
```

**Output**

| name  |
| ----- |
| Rahul |
| Aman  |
| Sneha |
| Karan |

---

## 28. NOT IN Operator

```sql id="l0xkmu"
SELECT *
FROM students
WHERE dept_id NOT IN(1,3);
```

**Output**

| name  |
| ----- |
| Priya |

---

## 29. BETWEEN Operator

```sql id="i1bbnn"
SELECT *
FROM students
WHERE age BETWEEN 20 AND 22;
```

**Output**

| name  | age |
| ----- | --- |
| Rahul | 20  |
| Priya | 21  |
| Sneha | 22  |

---

## 30. NOT BETWEEN

```sql id="6bqk6z"
SELECT *
FROM students
WHERE age NOT BETWEEN 20 AND 22;
```

**Output**

| name  | age |
| ----- | --- |
| Aman  | 19  |
| Karan | 23  |

---

# Module 6: LIKE & Wildcards

## 31. Name Starts With A

```sql id="wnk9qv"
SELECT *
FROM students
WHERE name LIKE 'A%';
```

**Output**

| name |
| ---- |
| Aman |

---

## 32. Name Ends With a

```sql id="sqmd9f"
SELECT *
FROM students
WHERE name LIKE '%a';
```

**Output**

| name  |
| ----- |
| Priya |
| Sneha |

---

## 33. Name Contains an

```sql id="a3d7ki"
SELECT *
FROM students
WHERE name LIKE '%an%';
```

**Output**

| name  |
| ----- |
| Aman  |
| Karan |

---

## 34. Wildcard _

Second character 'a' hona chahiye.

```sql id="y4vb6x"
SELECT *
FROM students
WHERE name LIKE '_a%';
```

**Output**

| name  |
| ----- |
| Rahul |
| Karan |

---

# Module 7: ORDER BY

## 35. Sort By Age Ascending

```sql id="mjlwm4"
SELECT *
FROM students
ORDER BY age ASC;
```

**Output**

| name  | age |
| ----- | --- |
| Aman  | 19  |
| Rahul | 20  |
| Priya | 21  |
| Sneha | 22  |
| Karan | 23  |

---

## 36. Sort By Age Descending

```sql id="i4c0jn"
SELECT *
FROM students
ORDER BY age DESC;
```

**Output**

| name  | age |
| ----- | --- |
| Karan | 23  |
| Sneha | 22  |
| Priya | 21  |
| Rahul | 20  |
| Aman  | 19  |

---

## 37. Sort By Name

```sql id="yuxx08"
SELECT *
FROM students
ORDER BY name;
```

**Output**

| name  |
| ----- |
| Aman  |
| Karan |
| Priya |
| Rahul |
| Sneha |

---

# Module 8: LIMIT

## 38. First 3 Students

```sql id="3gtq4f"
SELECT *
FROM students
LIMIT 3;
```

**Output**

| student_id | name  |
| ---------- | ----- |
| 1          | Rahul |
| 2          | Priya |
| 3          | Aman  |

---

## 39. Top 2 Oldest Students

```sql id="w49bj7"
SELECT *
FROM students
ORDER BY age DESC
LIMIT 2;
```

**Output**

| name  | age |
| ----- | --- |
| Karan | 23  |
| Sneha | 22  |

---

# Module 9: Alias

## 40. Alias Example

```sql id="8f31zd"
SELECT name AS StudentName,
age AS StudentAge
FROM students;
```

**Output**

| StudentName | StudentAge |
| ----------- | ---------- |
| Rahul       | 20         |
| Priya       | 21         |
| Aman        | 19         |
| Sneha       | 22         |
| Karan       | 23         |

---
# Module 10: Aggregate Functions (Basic to Advanced)

Assume the `students` table contains the following data:

| student_id | name  | age  | dept_id |
| ---------- | ----- | ---- | ------- |
| 1          | Rahul | 20   | 1       |
| 2          | Priya | 21   | 2       |
| 3          | Aman  | NULL | 1       |
| 4          | Sneha | 22   | 3       |
| 5          | Karan | 23   | 1       |

---

# 41. COUNT(*)

Counts all rows in the table.

```sql
SELECT COUNT(*)
FROM students;
```

### Output

| COUNT(*) |
| -------- |
| 5        |

---

# 42. COUNT(*) with Alias

Using `AS` to give a custom name to the output column.

```sql
SELECT COUNT(*) AS TotalStudents
FROM students;
```

### Output

| TotalStudents |
| ------------- |
| 5             |

### Explanation

Without Alias:

```sql
SELECT COUNT(*)
FROM students;
```

Output column name:

```text
COUNT(*)
```

With Alias:

```sql
SELECT COUNT(*) AS TotalStudents
FROM students;
```

Output column name:

```text
TotalStudents
```

---

# 43. COUNT(column_name)

Counts only non-NULL values in a column.

```sql
SELECT COUNT(age)
FROM students;
```

### Output

| COUNT(age) |
| ---------- |
| 4          |

### Explanation

Aman's age is NULL, so it is not counted.

---

# 44. COUNT(column_name) with Alias

```sql
SELECT COUNT(age) AS AgeCount
FROM students;
```

### Output

| AgeCount |
| -------- |
| 4        |

---

# 45. COUNT(DISTINCT dept_id)

Counts unique department IDs.

```sql
SELECT COUNT(DISTINCT dept_id)
FROM students;
```

### Output

| COUNT(DISTINCT dept_id) |
| ----------------------- |
| 3                       |

### Explanation

Unique department IDs are:

```text
1
2
3
```

---

# 46. SUM(age)

Calculates the total of all non-NULL ages.

```sql
SELECT SUM(age)
FROM students;
```

### Output

| SUM(age) |
| -------- |
| 86       |

### Calculation

```text
20 + 21 + 22 + 23 = 86
```

NULL values are ignored.

---

# 47. SUM(age) with Alias

```sql
SELECT SUM(age) AS TotalAge
FROM students;
```

### Output

| TotalAge |
| -------- |
| 86       |

---

# 48. AVG(age)

Calculates the average age.

```sql
SELECT AVG(age)
FROM students;
```

### Output

| AVG(age) |
| -------- |
| 21.50    |

### Calculation

```text
86 ÷ 4 = 21.50
```

NULL values are ignored.

---

# 49. AVG(age) with Alias

```sql
SELECT AVG(age) AS AverageAge
FROM students;
```

### Output

| AverageAge |
| ---------- |
| 21.50      |

---

# 50. ROUND(AVG(age),2)

Rounds the result to 2 decimal places.

```sql
SELECT ROUND(AVG(age),2)
FROM students;
```

### Output

| ROUND(AVG(age),2) |
| ----------------- |
| 21.50             |

---

# 51. MIN(age)

Returns the smallest value.

```sql
SELECT MIN(age)
FROM students;
```

### Output

| MIN(age) |
| -------- |
| 20       |

---

# 52. MIN(age) with Alias

```sql
SELECT MIN(age) AS YoungestStudent
FROM students;
```

### Output

| YoungestStudent |
| --------------- |
| 20              |

---

# 53. MAX(age)

Returns the largest value.

```sql
SELECT MAX(age)
FROM students;
```

### Output

| MAX(age) |
| -------- |
| 23       |

---

# 54. MAX(age) with Alias

```sql
SELECT MAX(age) AS OldestStudent
FROM students;
```

### Output

| OldestStudent |
| ------------- |
| 23            |

---

# 55. Aggregate Function with WHERE

Count students from Department 1.

```sql
SELECT COUNT(*)
FROM students
WHERE dept_id = 1;
```

### Output

| COUNT(*) |
| -------- |
| 3        |

---

# 56. Aggregate Function with Alias

```sql
SELECT COUNT(*) AS CS_Students
FROM students
WHERE dept_id = 1;
```

### Output

| CS_Students |
| ----------- |
| 3           |

---

# 57. SUM with WHERE

Calculate the total age of students in Department 1.

```sql
SELECT SUM(age)
FROM students
WHERE dept_id = 1;
```

### Output

| SUM(age) |
| -------- |
| 43       |

### Calculation

```text
20 + 23 = 43
```

Aman's age is NULL, so it is ignored.

---

# 58. AVG with WHERE

Calculate the average age of students in Department 1.

```sql
SELECT AVG(age)
FROM students
WHERE dept_id = 1;
```

### Output

| AVG(age) |
| -------- |
| 21.50    |

---

# 59. MAX with WHERE

Find the oldest student in Department 1.

```sql
SELECT MAX(age)
FROM students
WHERE dept_id = 1;
```

### Output

| MAX(age) |
| -------- |
| 23       |

---

# 60. MIN with WHERE

Find the youngest student in Department 1.

```sql
SELECT MIN(age)
FROM students
WHERE dept_id = 1;
```

### Output

| MIN(age) |
| -------- |
| 20       |

---

# Quick Interview Notes

| Function      | Counts NULL Values? |
| ------------- | ------------------- |
| COUNT(*)      | Yes (counts rows)   |
| COUNT(column) | No                  |
| SUM()         | No                  |
| AVG()         | No                  |
| MIN()         | No                  |
| MAX()         | No                  |

## Most Asked Interview Question

### Query 1

```sql
SELECT COUNT(*)
FROM students;
```

Counts all rows in the table.

### Query 2

```sql
SELECT COUNT(age)
FROM students;
```

Counts only non-NULL age values.

### Difference

| Query      | Result             |
| ---------- | ------------------ |
| COUNT(*)   | Total rows         |
| COUNT(age) | Non-NULL ages only |

This is one of the most common SQL interview questions and is very useful for understanding how aggregate functions handle NULL values.


-
