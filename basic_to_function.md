# 📚 MySQL Complete Practical Guide with Expected Output

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
# 📚 MySQL Complete Practical Guide with Expected Output

# Part 3 (Query 41–60)

---

# Module 10: Aggregate Functions

## 41. Count Total Students

Total records count karne ke liye.

```sql id="4w0s8v"
SELECT COUNT(*) AS TotalStudents
FROM students;
```

**Output**

| TotalStudents |
| ------------- |
| 5             |

---

## 42. Count Students In Department 1

```sql id="4zcb7g"
SELECT COUNT(*) AS CS_Students
FROM students
WHERE dept_id = 1;
```

**Output**

| CS_Students |
| ----------- |
| 3           |

---

## 43. Sum Of All Ages

```sql id="f8l1yz"
SELECT SUM(age) AS TotalAge
FROM students;
```

**Output**

| TotalAge |
| -------- |
| 105      |

**Calculation**

```text id="mxw9cx"
20 + 21 + 19 + 22 + 23 = 105
```

---

## 44. Average Age

```sql id="t8d7kp"
SELECT AVG(age) AS AverageAge
FROM students;
```

**Output**

| AverageAge |
| ---------- |
| 21.00      |

---

## 45. Minimum Age

```sql id="frq6hb"
SELECT MIN(age) AS YoungestStudent
FROM students;
```

**Output**

| YoungestStudent |
| --------------- |
| 19              |

---

## 46. Maximum Age

```sql id="gztj9j"
SELECT MAX(age) AS OldestStudent
FROM students;
```

**Output**

| OldestStudent |
| ------------- |
| 23            |

---

# Module 11: String Functions

## 47. Convert Names To Uppercase

```sql id="bgx7oe"
SELECT UPPER(name)
FROM students;
```

**Output**

| UPPER(name) |
| ----------- |
| RAHUL       |
| PRIYA       |
| AMAN        |
| SNEHA       |
| KARAN       |

---

## 48. Convert Names To Lowercase

```sql id="sjj75m"
SELECT LOWER(name)
FROM students;
```

**Output**

| LOWER(name) |
| ----------- |
| rahul       |
| priya       |
| aman        |
| sneha       |
| karan       |

---

## 49. Length Of Student Names

```sql id="pobn1i"
SELECT name,
LENGTH(name)
FROM students;
```

**Output**

| name  | LENGTH(name) |
| ----- | ------------ |
| Rahul | 5            |
| Priya | 5            |
| Aman  | 4            |
| Sneha | 5            |
| Karan | 5            |

---

## 50. Concatenate Name And City

```sql id="6i1qvn"
SELECT CONCAT(name,' - ',city)
AS Details
FROM students;
```

**Output**

| Details        |
| -------------- |
| Rahul - Pune   |
| Priya - Mumbai |
| Aman - Nashik  |
| Sneha - Pune   |
| Karan - Nagpur |

---

## 51. Full Student Information

```sql id="6ffwti"
SELECT CONCAT(name,' belongs to ',city)
AS StudentInfo
FROM students;
```

**Output**

| StudentInfo             |
| ----------------------- |
| Rahul belongs to Pune   |
| Priya belongs to Mumbai |
| Aman belongs to Nashik  |
| Sneha belongs to Pune   |
| Karan belongs to Nagpur |

---

# Module 12: NULL Functions

## 52. IFNULL Example

Suppose kisi student ki age NULL hai.

```sql id="8pohfx"
SELECT IFNULL(age,0)
FROM students;
```

**Output**

| IFNULL(age,0) |
| ------------- |
| 20            |
| 21            |
| 19            |
| 22            |
| 23            |

---

## 53. IFNULL With Alias

```sql id="awty3r"
SELECT name,
IFNULL(age,0)
AS StudentAge
FROM students;
```

**Output**

| name  | StudentAge |
| ----- | ---------- |
| Rahul | 20         |
| Priya | 21         |
| Aman  | 19         |
| Sneha | 22         |
| Karan | 23         |

---

# Module 13: ROUND Function

## 54. Round Average Age

```sql id="9hnywa"
SELECT ROUND(AVG(age),2)
AS AverageAge
FROM students;
```

**Output**

| AverageAge |
| ---------- |
| 21.00      |

---

# Module 14: UPDATE

## 55. Update City

```sql id="m7nx7n"
UPDATE students
SET city='Delhi'
WHERE student_id=1;
```

**Output**

```text id="lx6gjt"
Query OK, 1 row affected
```

---

## Verify Update

```sql id="4jjmns"
SELECT *
FROM students
WHERE student_id=1;
```

**Output**

| student_id | name  | city  |
| ---------- | ----- | ----- |
| 1          | Rahul | Delhi |

---

# Module 15: DELETE

## 56. Delete Student

```sql id="9jrqqd"
DELETE FROM students
WHERE student_id=5;
```

**Output**

```text id="pk0eqv"
Query OK, 1 row affected
```

---

## Verify Delete

```sql id="z44rmx"
SELECT *
FROM students;
```

**Output**

| student_id | name  |
| ---------- | ----- |
| 1          | Rahul |
| 2          | Priya |
| 3          | Aman  |
| 4          | Sneha |

---

# Module 16: ALTER TABLE

## 57. Add New Column

```sql id="1jl8o9"
ALTER TABLE students
ADD phone VARCHAR(15);
```

**Output**

```text id="6p0r6v"
Query OK, 0 rows affected
```

---

## 58. View Updated Structure

```sql id="txg4ec"
DESC students;
```

**Output**

| Field      |
| ---------- |
| student_id |
| name       |
| age        |
| email      |
| city       |
| dept_id    |
| phone      |

---

## 59. Drop Column

```sql id="1e5h7k"
ALTER TABLE students
DROP COLUMN phone;
```

**Output**

```text id="hjlwm7"
Query OK, 0 rows affected
```

---

# Module 17: TRUNCATE

## 60. Remove All Records

```sql id="rjdfgd"
TRUNCATE TABLE students;
```

**Output**

```text id="pvt6g6"
Query OK, 0 rows affected
```

---

## Verify

```sql id="7x1a0h"
SELECT *
FROM students;
```

**Output**

```text id="ng6l3t"
Empty set
```

---

# Summary

### Database Commands

✅ CREATE DATABASE

✅ SHOW DATABASES

✅ USE DATABASE

✅ DROP DATABASE

---

### Table Commands

✅ CREATE TABLE

✅ PRIMARY KEY

✅ FOREIGN KEY

✅ UNIQUE

✅ NOT NULL

✅ DEFAULT

✅ AUTO_INCREMENT

✅ ALTER TABLE

---

### DML Commands

✅ INSERT

✅ UPDATE

✅ DELETE

---

### Query Commands

✅ SELECT

✅ DISTINCT

✅ WHERE

✅ AND

✅ OR

✅ NOT

✅ IN

✅ BETWEEN

✅ LIKE

✅ ORDER BY

✅ LIMIT

✅ ALIAS

---

### Functions

✅ COUNT

✅ SUM

✅ AVG

✅ MIN

✅ MAX

✅ UPPER

✅ LOWER

✅ LENGTH

✅ CONCAT

✅ IFNULL

✅ ROUND

---

### Maintenance Commands

✅ ALTER TABLE

✅ TRUNCATE TABLE

✅ DROP TABLE
