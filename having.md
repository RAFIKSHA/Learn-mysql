# HAVING Clause in SQL

## What is HAVING?

The `HAVING` clause is used to filter **grouped data** after applying the `GROUP BY` clause.

It is commonly used with aggregate functions such as:

* `COUNT()`
* `SUM()`
* `AVG()`
* `MAX()`
* `MIN()`

---

# Difference Between WHERE and HAVING

| WHERE                                   | HAVING                        |
| --------------------------------------- | ----------------------------- |
| Filters rows before grouping            | Filters groups after grouping |
| Cannot use aggregate functions directly | Can use aggregate functions   |
| Works on individual records             | Works on grouped records      |

---

# Syntax

```sql
SELECT column_name, aggregate_function(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

---

# Example Table: Employees

| Emp_ID | Name  | Department | Salary |
| ------ | ----- | ---------- | ------ |
| 1      | Ali   | IT         | 50000  |
| 2      | Sara  | HR         | 40000  |
| 3      | John  | IT         | 60000  |
| 4      | Emma  | HR         | 45000  |
| 5      | David | Sales      | 55000  |

---

# Example 1: Departments Having More Than One Employee

```sql
SELECT Department, COUNT(*) AS Total_Employees
FROM Employees
GROUP BY Department
HAVING COUNT(*) > 1;
```

### Output

| Department | Total_Employees |
| ---------- | --------------- |
| IT         | 2               |
| HR         | 2               |

---

# Example 2: Departments Having Total Salary Greater Than 100000

```sql
SELECT Department, SUM(Salary) AS Total_Salary
FROM Employees
GROUP BY Department
HAVING SUM(Salary) > 100000;
```

### Output

| Department | Total_Salary |
| ---------- | ------------ |
| IT         | 110000       |

---

# Example 3: Departments Having Average Salary Greater Than 50000

```sql
SELECT Department, AVG(Salary) AS Avg_Salary
FROM Employees
GROUP BY Department
HAVING AVG(Salary) > 50000;
```

### Output

| Department | Avg_Salary |
| ---------- | ---------- |
| IT         | 55000      |

---

# WHERE vs HAVING Example

### Using WHERE

```sql
SELECT *
FROM Employees
WHERE Salary > 50000;
```

**Output:**

| Emp_ID | Name  | Department | Salary |
| ------ | ----- | ---------- | ------ |
| 3      | John  | IT         | 60000  |
| 5      | David | Sales      | 55000  |

This filters individual rows.

---

### Using HAVING

```sql
SELECT Department, AVG(Salary)
FROM Employees
GROUP BY Department
HAVING AVG(Salary) > 50000;
```

**Output:**

| Department | AVG(Salary) |
| ---------- | ----------- |
| IT         | 55000       |

This filters grouped data.

---

# Real-Life Example (Hospital Management System)

### Find Doctors Who Have More Than 5 Appointments

```sql
SELECT doctor_id, COUNT(*) AS total_appointments
FROM appointments
GROUP BY doctor_id
HAVING COUNT(*) > 5;
```

This query displays only those doctors who have more than 5 appointments.

---

# Interview Definition

> The HAVING clause is used to filter groups created by the GROUP BY clause. It is typically used with aggregate functions such as COUNT(), SUM(), AVG(), MAX(), and MIN().

---

# Easy Shortcut

### WHERE

**Filters Rows**

```sql
WHERE Salary > 50000
```

---

### HAVING

**Filters Groups**

```sql
HAVING COUNT(*) > 5
```

---

# SQL Execution Order

```sql
FROM
→ WHERE
→ GROUP BY
→ HAVING
→ SELECT
→ ORDER BY
```

---

# Quick Rule to Remember

✅ **WHERE = Row Filtering**

✅ **HAVING = Group Filtering**

✅ **HAVING is usually used with aggregate functions**

✅ **HAVING comes after GROUP BY** 🚀
