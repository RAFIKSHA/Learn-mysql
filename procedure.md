# 🚀 MySQL Stored Procedures Complete Practical Guide

## From Beginner to Industry Level

---

# What is a Stored Procedure?

A **Stored Procedure** is a collection of SQL statements stored inside the database that can be executed whenever needed.

Think of it like a **function in programming**.

Instead of writing the same SQL query again and again, we save it as a procedure and call it whenever required.

---

# Why Use Stored Procedures?

Without Procedure:

```sql
SELECT * FROM patients;

SELECT * FROM patients;

SELECT * FROM patients;
```

Same query written multiple times.

---

With Procedure:

```sql
CALL GetAllPatients();
```

Reusable and cleaner.

---

# Real-Life Example

Suppose a hospital receptionist wants patient information.

Instead of writing:

```sql
SELECT *
FROM patients;
```

every time,

they simply execute:

```sql
CALL GetAllPatients();
```

---

# Step 1: Create Database

```sql
CREATE DATABASE hospital_db;

USE hospital_db;
```

---

# Step 2: Create Table

```sql
CREATE TABLE patients(
    patient_id INT PRIMARY KEY,
    patient_name VARCHAR(100),
    city VARCHAR(50)
);
```

---

# Step 3: Insert Data

```sql
INSERT INTO patients
VALUES
(1,'Rahul','Pune'),
(2,'Priya','Mumbai'),
(3,'Amit','Delhi'),
(4,'Rohit','Pune');
```

---

# Check Data

```sql
SELECT * FROM patients;
```

Output

| patient_id | patient_name | city   |
| ---------- | ------------ | ------ |
| 1          | Rahul        | Pune   |
| 2          | Priya        | Mumbai |
| 3          | Amit         | Delhi  |
| 4          | Rohit        | Pune   |

---

# Procedure 1: Get All Patients

## Create Procedure

```sql
DELIMITER $$

CREATE PROCEDURE GetAllPatients()
BEGIN

    SELECT *
    FROM patients;

END $$

DELIMITER ;
```

---

# Understanding the Syntax

### DELIMITER $$

```sql
DELIMITER $$
```

Temporarily changes the statement terminator.

Normally MySQL ends statements with:

```sql
;
```

But procedures contain multiple SQL statements.

So we use:

```sql
$$
```

---

### CREATE PROCEDURE

```sql
CREATE PROCEDURE GetAllPatients()
```

Creates a procedure named:

```text
GetAllPatients
```

---

### BEGIN ... END

```sql
BEGIN

END
```

Everything inside runs when the procedure is called.

---

# Execute Procedure

```sql
CALL GetAllPatients();
```

Output

| patient_id | patient_name | city   |
| ---------- | ------------ | ------ |
| 1          | Rahul        | Pune   |
| 2          | Priya        | Mumbai |
| 3          | Amit         | Delhi  |
| 4          | Rohit        | Pune   |

---

# View Procedures

```sql
SHOW PROCEDURE STATUS
WHERE Db='hospital_db';
```

Shows all procedures in the database.

---

# Procedure 2: Procedure with Input Parameter

Suppose we want details of only one patient.

---

## Create Procedure

```sql
DELIMITER $$

CREATE PROCEDURE GetPatientById(
    IN pid INT
)

BEGIN

    SELECT *
    FROM patients
    WHERE patient_id = pid;

END $$

DELIMITER ;
```

---

# Execute

```sql
CALL GetPatientById(2);
```

Output

| patient_id | patient_name | city   |
| ---------- | ------------ | ------ |
| 2          | Priya        | Mumbai |

---

# Understanding IN Parameter

```sql
IN pid INT
```

User sends value into procedure.

Example:

```sql
CALL GetPatientById(3);
```

Then:

```text
pid = 3
```

---

# Procedure 3: Search Patients by City

## Create Procedure

```sql
DELIMITER $$

CREATE PROCEDURE GetPatientsByCity(
    IN p_city VARCHAR(50)
)

BEGIN

    SELECT *
    FROM patients
    WHERE city = p_city;

END $$

DELIMITER ;
```

---

# Execute

```sql
CALL GetPatientsByCity('Pune');
```

Output

| patient_id | patient_name | city |
| ---------- | ------------ | ---- |
| 1          | Rahul        | Pune |
| 4          | Rohit        | Pune |

---

# Procedure 4: Insert Data Using Procedure

Instead of writing INSERT every time.

---

## Create Procedure

```sql
DELIMITER $$

CREATE PROCEDURE AddPatient(
    IN p_id INT,
    IN p_name VARCHAR(100),
    IN p_city VARCHAR(50)
)

BEGIN

    INSERT INTO patients
    VALUES(
        p_id,
        p_name,
        p_city
    );

END $$

DELIMITER ;
```

---

# Execute

```sql
CALL AddPatient(
    5,
    'Neha',
    'Delhi'
);
```

---

# Verify

```sql
SELECT * FROM patients;
```

New patient added.

---

# Procedure 5: Update Patient

## Create Procedure

```sql
DELIMITER $$

CREATE PROCEDURE UpdateCity(
    IN p_id INT,
    IN p_city VARCHAR(50)
)

BEGIN

    UPDATE patients
    SET city = p_city
    WHERE patient_id = p_id;

END $$

DELIMITER ;
```

---

# Execute

```sql
CALL UpdateCity(
    1,
    'Mumbai'
);
```

---

# Verify

```sql
SELECT *
FROM patients
WHERE patient_id=1;
```

Output

| patient_id | patient_name | city   |
| ---------- | ------------ | ------ |
| 1          | Rahul        | Mumbai |

---

# Procedure 6: Delete Patient

## Create Procedure

```sql
DELIMITER $$

CREATE PROCEDURE DeletePatient(
    IN p_id INT
)

BEGIN

    DELETE FROM patients
    WHERE patient_id=p_id;

END $$

DELIMITER ;
```

---

# Execute

```sql
CALL DeletePatient(4);
```

Patient deleted.

---

# Procedure with OUT Parameter

Used when procedure returns a value.

---

# Create Procedure

```sql
DELIMITER $$

CREATE PROCEDURE TotalPatients(
    OUT total INT
)

BEGIN

    SELECT COUNT(*)
    INTO total
    FROM patients;

END $$

DELIMITER ;
```

---

# Execute

```sql
CALL TotalPatients(@count);

SELECT @count;
```

Output

```text
4
```

---

# Understanding OUT

Procedure sends data back.

```text
Database → User
```

---

# Procedure with INOUT Parameter

Can receive and return values.

---

## Create Procedure

```sql
DELIMITER $$

CREATE PROCEDURE IncreaseNumber(
    INOUT num INT
)

BEGIN

    SET num = num + 10;

END $$

DELIMITER ;
```

---

# Execute

```sql
SET @x = 5;

CALL IncreaseNumber(@x);

SELECT @x;
```

Output

```text
15
```

---

# Modify Procedure

MySQL doesn't support:

```sql
ALTER PROCEDURE
```

for changing logic.

Usually:

```sql
DROP PROCEDURE
```

then recreate.

---

# Delete Procedure

```sql
DROP PROCEDURE GetAllPatients;
```

Procedure removed.

---

# Real Industry Uses

### Banking

```text
Transfer Money
```

---

### Hospital

```text
Patient Registration
```

---

### E-Commerce

```text
Order Processing
```

---

### Payroll

```text
Salary Calculation
```

---

# Advantages of Stored Procedures

### Reusability

Write once, use many times.

---

### Better Security

Users execute procedures instead of direct table access.

---

### Faster Execution

Procedure is stored and optimized by MySQL.

---

### Reduced Network Traffic

Instead of sending multiple SQL statements, send:

```sql
CALL ProcedureName();
```

---

# Procedure vs Function

| Feature                      | Procedure      | Function     |
| ---------------------------- | -------------- | ------------ |
| Can return multiple values   | Yes            | No           |
| Can use INSERT/UPDATE/DELETE | Yes            | Limited      |
| Called using                 | CALL           | SELECT       |
| Main Use                     | Business Logic | Calculations |

---

# Interview Questions

### What is a Stored Procedure?

A stored collection of SQL statements that can be executed repeatedly.

---

### Why use Stored Procedures?

* Reusability
* Security
* Performance
* Maintainability

---

### Types of Parameters?

1. IN
2. OUT
3. INOUT

---

### Command to Execute a Procedure?

```sql
CALL ProcedureName();
```

---

### Command to Delete a Procedure?

```sql
DROP PROCEDURE ProcedureName;
```

---

# Best Classroom Flow

```text
1. Create Database
2. Create Table
3. Insert Data
4. Create Simple Procedure
5. CALL Procedure
6. IN Parameter
7. OUT Parameter
8. INOUT Parameter
9. INSERT Procedure
10. UPDATE Procedure
11. DELETE Procedure
12. Industry Use Cases
```

This sequence covers about **90% of what students and interviewers expect regarding MySQL Stored Procedures**.
