---

# **📚 MySQL Full Practical Guide (College Database Example)**

---

## **1️⃣ Create Database**

```sql
CREATE DATABASE college;
USE college;
```

---

## **2️⃣ Create Tables**

```sql
CREATE TABLE departments (
    dept_id INT PRIMARY KEY AUTO_INCREMENT,
    dept_name VARCHAR(50) NOT NULL
);

CREATE TABLE courses (
    course_id INT PRIMARY KEY AUTO_INCREMENT,
    course_name VARCHAR(50) NOT NULL,
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);

CREATE TABLE students (
    student_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL,
    age INT,
    email VARCHAR(100) UNIQUE,
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);
```

---

## **3️⃣ Insert Sample Data**

```sql
INSERT INTO departments (dept_name) VALUES
('Computer Science'),
('Mechanical'),
('Electrical');

INSERT INTO courses (course_name, dept_id) VALUES
('Database Systems', 1),
('Data Structures', 1),
('Thermodynamics', 2),
('Circuit Analysis', 3);

INSERT INTO students (name, age, email, dept_id) VALUES
('Rahul', 20, 'rahul@example.com', 1),
('Priya', 21, 'priya@example.com', 2),
('Aman', 19, 'aman@example.com', 1),
('Sneha', NULL, 'sneha@example.com', 3);
```

---

## **4️⃣ SELECT**

```sql
SELECT * FROM students;
SELECT name, age FROM students;
```

---

## **5️⃣ WHERE**

```sql
SELECT * FROM students WHERE age > 20;
SELECT * FROM students WHERE dept_id = 1;
```

---

## **6️⃣ AND, OR, NOT**

```sql
SELECT * FROM students WHERE age > 18 AND dept_id = 1;
SELECT * FROM students WHERE dept_id = 1 OR dept_id = 2;
SELECT * FROM students WHERE NOT dept_id = 1;
```

---

## **7️⃣ ORDER BY**

```sql
SELECT * FROM students ORDER BY age ASC;
SELECT * FROM students ORDER BY name DESC;
```

---

## **8️⃣ INSERT INTO**

```sql
INSERT INTO students (name, age, email, dept_id)
VALUES ('Ravi', 22, 'ravi@example.com', 2);
```

---

## **9️⃣ NULL Values**

```sql
SELECT * FROM students WHERE age IS NULL;
SELECT * FROM students WHERE age IS NOT NULL;
```

---

## **🔟 UPDATE**

```sql
UPDATE students SET age = 20 WHERE name = 'Sneha';
```

---

## **1️⃣1️⃣ DELETE**

```sql
DELETE FROM students WHERE name = 'Ravi';
```

---

## **1️⃣2️⃣ LIMIT**

```sql
SELECT * FROM students LIMIT 2;
```

---

## **1️⃣3️⃣ MIN and MAX**

```sql
SELECT MIN(age) AS Youngest FROM students;
SELECT MAX(age) AS Oldest FROM students;
```

---

## **1️⃣4️⃣ COUNT, AVG, SUM**

```sql
SELECT COUNT(*) AS Total_Students FROM students;
SELECT AVG(age) AS Average_Age FROM students;
SELECT SUM(age) AS Total_Age FROM students;
```

---

## **1️⃣5️⃣ LIKE**

```sql
SELECT * FROM students WHERE name LIKE 'R%';
SELECT * FROM students WHERE name LIKE '%a';
```

---

## **1️⃣6️⃣ Wildcards**

```sql
SELECT * FROM students WHERE name LIKE '_a%'; -- 2nd letter is 'a'
```

---

## **1️⃣7️⃣ IN**

```sql
SELECT * FROM students WHERE dept_id IN (1, 3);
```

---

## **1️⃣8️⃣ BETWEEN**

```sql
SELECT * FROM students WHERE age BETWEEN 19 AND 21;
```

---

## **1️⃣9️⃣ Aliases**

```sql
SELECT name AS StudentName, age AS StudentAge FROM students;
```

---

## **2️⃣0️⃣ Joins**

```sql
-- INNER JOIN
SELECT students.name, courses.course_name
FROM students
JOIN courses ON students.dept_id = courses.dept_id;

-- LEFT JOIN
SELECT students.name, courses.course_name
FROM students
LEFT JOIN courses ON students.dept_id = courses.dept_id;

-- RIGHT JOIN
SELECT students.name, courses.course_name
FROM students
RIGHT JOIN courses ON students.dept_id = courses.dept_id;

-- CROSS JOIN
SELECT students.name, courses.course_name
FROM students CROSS JOIN courses;

-- SELF JOIN (Example: students with same department)
SELECT a.name AS Student1, b.name AS Student2
FROM students a
JOIN students b ON a.dept_id = b.dept_id AND a.student_id < b.student_id;
```

---

## **2️⃣1️⃣ UNION & UNION ALL**

```sql
SELECT name FROM students
UNION
SELECT course_name FROM courses;

SELECT name FROM students
UNION ALL
SELECT course_name FROM courses;
```

---

## **2️⃣2️⃣ GROUP BY & HAVING**

```sql
SELECT dept_id, COUNT(*) AS TotalStudents
FROM students
GROUP BY dept_id;

SELECT dept_id, COUNT(*) AS TotalStudents
FROM students
GROUP BY dept_id
HAVING COUNT(*) > 1;
```

---

## **2️⃣3️⃣ EXISTS**

```sql
SELECT name FROM students s
WHERE EXISTS (
    SELECT * FROM courses c WHERE s.dept_id = c.dept_id
);
```

---

## **2️⃣4️⃣ ANY, ALL**

```sql
SELECT * FROM students WHERE age > ANY (SELECT age FROM students WHERE dept_id = 1);
SELECT * FROM students WHERE age > ALL (SELECT age FROM students WHERE dept_id = 1);
```

---

## **2️⃣5️⃣ INSERT SELECT**

```sql
INSERT INTO students (name, age, email, dept_id)
SELECT 'Test', 25, 'test@example.com', dept_id
FROM departments WHERE dept_id = 1;
```

---

## **2️⃣6️⃣ CASE**

```sql
SELECT name,
CASE
    WHEN age >= 21 THEN 'Senior'
    WHEN age >= 18 THEN 'Junior'
    ELSE 'Minor'
END AS Category
FROM students;
```

---

## **2️⃣7️⃣ Null Functions**

```sql
SELECT name, IFNULL(age, 0) AS Age FROM students;
```

---

## **2️⃣8️⃣ Comments**

```sql
-- This is a single-line comment
/* This is 
   a multi-line comment */
```

---

## **2️⃣9️⃣ Constraints Examples**

```sql
CREATE TABLE test (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE
);
```

---

## **3️⃣0️⃣ Alter Table**

```sql
ALTER TABLE students ADD phone VARCHAR(15);
ALTER TABLE students DROP COLUMN phone;
ALTER TABLE students MODIFY name VARCHAR(100);
```

---

Sir, if you want,
I can put **all these queries + explanations into a neat PDF with diagrams** so you can **directly give it to students as their MySQL handbook**.
Do you want me to prepare that PDF?
