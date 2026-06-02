# 📚 MySQL Practical Guide (Module 1–5)

## Module 1: Database Basics

### 1. Create Database

Database create karne ke liye use hota hai.

```sql
CREATE DATABASE college;
```

### 2. Show Databases

Server me available databases dekhne ke liye.

```sql
SHOW DATABASES;
```

### 3. Select Database

Kaam karne ke liye database choose karte hain.

```sql
USE college;
```

### 4. Drop Database

Database permanently delete karne ke liye.

```sql
DROP DATABASE college;
```

---

## Module 2: Table Operations

### 5. Create Department Table

```sql
CREATE TABLE departments(
dept_id INT PRIMARY KEY AUTO_INCREMENT,
dept_name VARCHAR(50) NOT NULL
);
```

### 6. Create Student Table

```sql
CREATE TABLE students(
student_id INT PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(50) NOT NULL,
age INT,
email VARCHAR(100) UNIQUE,
dept_id INT
);
```

### 7. Add Foreign Key

```sql
ALTER TABLE students
ADD CONSTRAINT fk_dept
FOREIGN KEY(dept_id)
REFERENCES departments(dept_id);
```

### 8. Show Tables

```sql
SHOW TABLES;
```

### 9. Describe Table

```sql
DESC students;
```

### 10. Data Type Example INT

```sql
CREATE TABLE test1(
id INT
);
```

### 11. Data Type Example VARCHAR

```sql
CREATE TABLE test2(
name VARCHAR(50)
);
```

### 12. Data Type Example FLOAT

```sql
CREATE TABLE test3(
percentage FLOAT
);
```

### 13. Data Type Example DATE

```sql
CREATE TABLE test4(
joining_date DATE
);
```

### 14. PRIMARY KEY Example

```sql
CREATE TABLE demo1(
id INT PRIMARY KEY
);
```

### 15. UNIQUE Example

```sql
CREATE TABLE demo2(
email VARCHAR(100) UNIQUE
);
```

### 16. NOT NULL Example

```sql
CREATE TABLE demo3(
name VARCHAR(50) NOT NULL
);
```

### 17. DEFAULT Example

```sql
CREATE TABLE demo4(
city VARCHAR(50) DEFAULT 'Pune'
);
```

### 18. AUTO_INCREMENT Example

```sql
CREATE TABLE demo5(
id INT AUTO_INCREMENT PRIMARY KEY
);
```

### 19. Add New Column

```sql
ALTER TABLE students
ADD phone VARCHAR(15);
```

### 20. Modify Column

```sql
ALTER TABLE students
MODIFY name VARCHAR(100);
```

### 21. Rename Column

```sql
ALTER TABLE students
RENAME COLUMN phone TO mobile;
```

### 22. Drop Column

```sql
ALTER TABLE students
DROP COLUMN mobile;
```

### 23. Truncate Table

```sql
TRUNCATE TABLE students;
```

### 24. Drop Table

```sql
DROP TABLE demo5;
```

---

## Module 3: DML Commands

### 25. Insert Department

```sql
INSERT INTO departments(dept_name)
VALUES('Computer Science');
```

### 26. Insert Multiple Departments

```sql
INSERT INTO departments(dept_name)
VALUES
('Mechanical'),
('Electrical'),
('Civil');
```

### 27. Insert Student

```sql
INSERT INTO students(name,age,email,dept_id)
VALUES
('Rahul',20,'rahul@gmail.com',1);
```

### 28. Insert Multiple Students

```sql
INSERT INTO students(name,age,email,dept_id)
VALUES
('Aman',21,'aman@gmail.com',1),
('Priya',22,'priya@gmail.com',2),
('Sneha',20,'sneha@gmail.com',3);
```

### 29. Insert Select

```sql
INSERT INTO students(name,age,email,dept_id)
SELECT
'Test',
25,
'test@gmail.com',
dept_id
FROM departments
WHERE dept_id=1;
```

### 30. Update Student Age

```sql
UPDATE students
SET age=23
WHERE student_id=1;
```

### 31. Update Multiple Columns

```sql
UPDATE students
SET age=24,
name='Ravi'
WHERE student_id=2;
```

### 32. Delete One Record

```sql
DELETE FROM students
WHERE student_id=3;
```

### 33. Delete All Records

```sql
DELETE FROM students;
```

---

## Module 4: Querying Data

### 34. Select All Records

```sql
SELECT * FROM students;
```

### 35. Select Specific Columns

```sql
SELECT name,age
FROM students;
```

### 36. DISTINCT

```sql
SELECT DISTINCT dept_id
FROM students;
```

### 37. WHERE Condition

```sql
SELECT *
FROM students
WHERE age > 20;
```

### 38. AND Operator

```sql
SELECT *
FROM students
WHERE age > 20
AND dept_id=1;
```

### 39. OR Operator

```sql
SELECT *
FROM students
WHERE dept_id=1
OR dept_id=2;
```

### 40. NOT Operator

```sql
SELECT *
FROM students
WHERE NOT dept_id=1;
```

### 41. IN Operator

```sql
SELECT *
FROM students
WHERE dept_id IN(1,2);
```

### 42. NOT IN

```sql
SELECT *
FROM students
WHERE dept_id NOT IN(1,2);
```

### 43. BETWEEN

```sql
SELECT *
FROM students
WHERE age BETWEEN 20 AND 22;
```

### 44. NOT BETWEEN

```sql
SELECT *
FROM students
WHERE age NOT BETWEEN 20 AND 22;
```

### 45. LIKE Starts With

```sql
SELECT *
FROM students
WHERE name LIKE 'R%';
```

### 46. LIKE Ends With

```sql
SELECT *
FROM students
WHERE name LIKE '%a';
```

### 47. LIKE Contains

```sql
SELECT *
FROM students
WHERE name LIKE '%an%';
```

### 48. Wildcard _

```sql
SELECT *
FROM students
WHERE name LIKE '_a%';
```

### 49. ORDER BY ASC

```sql
SELECT *
FROM students
ORDER BY age ASC;
```

### 50. ORDER BY DESC

```sql
SELECT *
FROM students
ORDER BY age DESC;
```

### 51. LIMIT

```sql
SELECT *
FROM students
LIMIT 5;
```

### 52. Alias Example

```sql
SELECT name AS StudentName
FROM students;
```

---

## Module 5: Functions

### 53. COUNT

```sql
SELECT COUNT(*) AS TotalStudents
FROM students;
```

### 54. SUM

```sql
SELECT SUM(age)
FROM students;
```

### 55. AVG

```sql
SELECT AVG(age)
FROM students;
```

### 56. MIN

```sql
SELECT MIN(age)
FROM students;
```

### 57. MAX

```sql
SELECT MAX(age)
FROM students;
```

### 58. UPPER

```sql
SELECT UPPER(name)
FROM students;
```

### 59. LOWER

```sql
SELECT LOWER(name)
FROM students;
```

### 60. LENGTH

```sql
SELECT LENGTH(name)
FROM students;
```

### 61. CONCAT

```sql
SELECT CONCAT(name,' - ',email)
FROM students;
```

### 62. IFNULL

```sql
SELECT IFNULL(age,0)
FROM students;
```

### 63. ROUND

```sql
SELECT ROUND(AVG(age),2)
FROM students;
```
