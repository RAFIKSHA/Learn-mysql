# 🚀 MySQL Indexing Practical Flow Explanation

This practical demonstrates **why indexing is needed, how it works, and how to verify it using EXPLAIN**.

---

# Step 1: Create Database

```sql
CREATE DATABASE hospital_db;
USE hospital_db;
```

### What is happening?

```sql
CREATE DATABASE hospital_db;
```

Creates a new database named **hospital_db**.

```sql
USE hospital_db;
```

Selects the database so that all tables and queries will be executed inside it.

---

# Step 2: Create Table

```sql
CREATE TABLE patients(
    patient_id INT PRIMARY KEY,
    patient_name VARCHAR(100),
    city VARCHAR(50)
);
```

### What is happening?

We are creating a table named **patients**.

| Column       | Purpose           |
| ------------ | ----------------- |
| patient_id   | Unique Patient ID |
| patient_name | Patient Name      |
| city         | Patient City      |

---

### Important Point

```sql
patient_id INT PRIMARY KEY
```

A **PRIMARY KEY automatically creates an index** in MySQL.

Therefore, searching by patient_id is already optimized.

Example:

```sql
SELECT * FROM patients
WHERE patient_id = 1;
```

MySQL can find the record quickly because the primary key is indexed.

---

# Step 3: Insert Records

```sql
INSERT INTO patients VALUES
(1,'Rahul','Pune'),
(2,'Priya','Mumbai'),
(3,'Amit','Delhi'),
(4,'Rohit','Pune');
```

### Current Table Data

| patient_id | patient_name | city   |
| ---------- | ------------ | ------ |
| 1          | Rahul        | Pune   |
| 2          | Priya        | Mumbai |
| 3          | Amit         | Delhi  |
| 4          | Rohit        | Pune   |

Suppose a doctor wants to find all patients from Pune.

---

# Step 4: Query Before Creating an Index

```sql
EXPLAIN
SELECT *
FROM patients
WHERE city='Pune';
```

---

# What is EXPLAIN?

EXPLAIN does not execute the query.

It shows:

```text
How MySQL plans to execute the query
```

Database administrators use EXPLAIN to analyze query performance.

---

# How Does MySQL Search Without an Index?

Since the **city column is not indexed**, MySQL checks every row.

Internally:

```text
Row 1 → Pune ✓
Row 2 → Mumbai
Row 3 → Delhi
Row 4 → Pune ✓
```

This process is called:

# Full Table Scan

Because MySQL scans the entire table.

---

# Possible EXPLAIN Output

| type |
| ---- |
| ALL  |

### Meaning

```text
ALL = Full Table Scan
```

MySQL is reading all rows in the table.

With 4 rows this is not a problem.

But with:

```text
100,000 rows
1,000,000 rows
10,000,000 rows
```

the query becomes much slower.

---

# Step 5: Create an Index

```sql
CREATE INDEX idx_city
ON patients(city);
```

---

# What is happening?

MySQL creates a special data structure for the city column.

Conceptually:

```text
Index

Delhi  → Row 3
Mumbai → Row 2
Pune   → Row 1, Row 4
```

Now MySQL knows exactly where "Pune" records are located.

It no longer needs to scan every row.

---

# Real-Life Example

### Without Index

Imagine a 1000-page book.

To find the topic "Database", you must check page by page.

```text
Page 1
Page 2
Page 3
...
Page 1000
```

Slow process.

---

### With Index

Open the index section of the book.

```text
Database → Page 350
```

Go directly to page 350.

Much faster.

---

# Step 6: Run the Same Query Again

```sql
EXPLAIN
SELECT *
FROM patients
WHERE city='Pune';
```

---

# What happens now?

MySQL uses the index.

Instead of scanning all rows, it looks inside the index.

Conceptually:

```text
Index Lookup

Pune → Row 1, Row 4
```

Direct access to matching records.

---

# Possible EXPLAIN Output

| type |
| ---- |
| ref  |

### Meaning

```text
ref = Index is being used
```

This is much better than ALL.

---

# Step 7: View Existing Indexes

```sql
SHOW INDEX FROM patients;
```

---

# Purpose

Displays all indexes available in the table.

Possible Output:

| Key_name | Column_name |
| -------- | ----------- |
| PRIMARY  | patient_id  |
| idx_city | city        |

---

# Explanation

### PRIMARY

Automatically created because:

```sql
PRIMARY KEY
```

was defined on patient_id.

---

### idx_city

Manually created because:

```sql
CREATE INDEX idx_city
ON patients(city);
```

was executed.

---

# Complete Performance Story

## Before Index

Query:

```sql
SELECT * FROM patients
WHERE city='Pune';
```

MySQL Process:

```text
Check Row 1
Check Row 2
Check Row 3
Check Row 4
```

Execution Type:

```text
ALL
```

Meaning:

```text
Full Table Scan
```

---

## After Index

Query:

```sql
SELECT * FROM patients
WHERE city='Pune';
```

MySQL Process:

```text
Check Index
Find Pune
Retrieve Rows 1 and 4
```

Execution Type:

```text
ref
```

Meaning:

```text
Index Lookup
```

---

# Key Learning

**An index does not change the data.**

**An index does not change the query result.**

**An index only makes searching faster by helping MySQL locate records efficiently.**

---

# Interview Question

### Why did we create an index on the city column?

Because city is frequently used in the WHERE clause:

```sql
SELECT *
FROM patients
WHERE city='Pune';
```

Frequently searched columns are good candidates for indexing.

---

# Final Definition

**Indexing is a database optimization technique that improves query performance by creating a fast lookup structure for one or more columns, reducing the need for full table scans.**
