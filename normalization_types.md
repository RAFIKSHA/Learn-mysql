# 🚀 Database Normalization Complete Practical Guide

## From Unnormalized Data → 1NF → 2NF → 3NF

### Real Project: Hospital Management System

---

# What is Normalization?

**Normalization** is the process of organizing data into multiple related tables to:

* Reduce Data Redundancy
* Eliminate Data Anomalies
* Improve Data Consistency
* Improve Database Design
* Make Maintenance Easier

---

# Why Do We Need Normalization?

Suppose a hospital stores all information in one table.

Without normalization:

❌ Duplicate Data

❌ Update Problems

❌ Insert Problems

❌ Delete Problems

---

# Step 1: Create Database

```sql
CREATE DATABASE hospital_db;

USE hospital_db;
```

---

# Understanding UNF (Un-Normalized Form)

Before learning 1NF, we must understand what happens when data is not normalized.

---

## Create Unnormalized Table

```sql
CREATE TABLE patient_records(
    patient_id INT,
    patient_name VARCHAR(100),
    doctors VARCHAR(200)
);
```

---

## Insert Data

```sql
INSERT INTO patient_records
VALUES
(1,'Rahul','Dr. Mehta,Dr. Khan'),
(2,'Priya','Dr. Patel'),
(3,'Amit','Dr. Khan,Dr. Sharma');
```

---

## Current Data

| patient_id | patient_name | doctors              |
| ---------- | ------------ | -------------------- |
| 1          | Rahul        | Dr. Mehta, Dr. Khan  |
| 2          | Priya        | Dr. Patel            |
| 3          | Amit         | Dr. Khan, Dr. Sharma |

---

# Problem

Notice this column:

```text
Dr. Mehta, Dr. Khan
```

Multiple values are stored inside one cell.

This violates database design rules.

This form is called:

# UNF (Un-Normalized Form)

---

# First Normal Form (1NF)

## Definition

A table is in 1NF if:

✅ Each column contains atomic values

✅ No multiple values in one cell

✅ No repeating groups

---

# Convert UNF → 1NF

Instead of:

| patient_id | patient_name | doctors             |
| ---------- | ------------ | ------------------- |
| 1          | Rahul        | Dr. Mehta, Dr. Khan |

Store as:

| patient_id | patient_name | doctor_name |
| ---------- | ------------ | ----------- |
| 1          | Rahul        | Dr. Mehta   |
| 1          | Rahul        | Dr. Khan    |

---

## Create 1NF Table

```sql
CREATE TABLE patient_doctors(
    patient_id INT,
    patient_name VARCHAR(100),
    doctor_name VARCHAR(100)
);
```

---

## Insert Data

```sql
INSERT INTO patient_doctors
VALUES
(1,'Rahul','Dr. Mehta'),
(1,'Rahul','Dr. Khan'),
(2,'Priya','Dr. Patel'),
(3,'Amit','Dr. Khan'),
(3,'Amit','Dr. Sharma');
```

---

## Result

| patient_id | patient_name | doctor_name |
| ---------- | ------------ | ----------- |
| 1          | Rahul        | Dr. Mehta   |
| 1          | Rahul        | Dr. Khan    |
| 2          | Priya        | Dr. Patel   |
| 3          | Amit         | Dr. Khan    |
| 3          | Amit         | Dr. Sharma  |

---

# Is This Fully Normalized?

❌ No

Look carefully:

```text
Rahul repeated
Rahul repeated
Amit repeated
```

Still duplicate data exists.

---

# Second Normal Form (2NF)

## Definition

A table is in 2NF if:

✅ It is already in 1NF

✅ No Partial Dependency exists

---

# What is Partial Dependency?

Suppose table:

| patient_id | patient_name | doctor_name |
| ---------- | ------------ | ----------- |
| 1          | Rahul        | Dr. Mehta   |
| 1          | Rahul        | Dr. Khan    |

Here:

```text
patient_name depends only on patient_id
```

But patient_name is repeated in every row.

This is called:

# Partial Dependency

---

# Convert 1NF → 2NF

Separate patient information.

---

## Patients Table

```sql
CREATE TABLE patients(
    patient_id INT PRIMARY KEY,
    patient_name VARCHAR(100)
);
```

---

## Patient_Doctor Table

```sql
CREATE TABLE patient_doctor(
    patient_id INT,
    doctor_name VARCHAR(100)
);
```

---

## Insert Data

### Patients

```sql
INSERT INTO patients
VALUES
(1,'Rahul'),
(2,'Priya'),
(3,'Amit');
```

---

### Patient_Doctor

```sql
INSERT INTO patient_doctor
VALUES
(1,'Dr. Mehta'),
(1,'Dr. Khan'),
(2,'Dr. Patel'),
(3,'Dr. Khan'),
(3,'Dr. Sharma');
```

---

## Now Data Looks Better

### Patients

| patient_id | patient_name |
| ---------- | ------------ |
| 1          | Rahul        |
| 2          | Priya        |
| 3          | Amit         |

---

### Patient_Doctor

| patient_id | doctor_name |
| ---------- | ----------- |
| 1          | Dr. Mehta   |
| 1          | Dr. Khan    |
| 2          | Dr. Patel   |

---

# Is This Fully Normalized?

Still ❌ No

Because:

```text
Doctor Name is repeated
```

---

# Third Normal Form (3NF)

## Definition

A table is in 3NF if:

✅ It is already in 2NF

✅ No Transitive Dependency exists

---

# What is Transitive Dependency?

Suppose we have:

| doctor_name | specialization |
| ----------- | -------------- |
| Dr. Mehta   | Cardiologist   |
| Dr. Khan    | Neurologist    |

Relationship:

```text
doctor_name → specialization
```

Specialization depends on doctor.

Not on patient.

Therefore it should be stored separately.

---

# Create Final 3NF Design

---

## Patients Table

```sql
CREATE TABLE patients(
    patient_id INT PRIMARY KEY,
    patient_name VARCHAR(100)
);
```

---

## Doctors Table

```sql
CREATE TABLE doctors(
    doctor_id INT PRIMARY KEY,
    doctor_name VARCHAR(100),
    specialization VARCHAR(100)
);
```

---

## Appointments Table

```sql
CREATE TABLE appointments(
    appointment_id INT PRIMARY KEY,
    patient_id INT,
    doctor_id INT
);
```

---

# Insert Data

## Patients

```sql
INSERT INTO patients
VALUES
(1,'Rahul'),
(2,'Priya'),
(3,'Amit');
```

---

## Doctors

```sql
INSERT INTO doctors
VALUES
(101,'Dr. Mehta','Cardiologist'),
(102,'Dr. Khan','Neurologist'),
(103,'Dr. Patel','Orthopedic'),
(104,'Dr. Sharma','Dermatologist');
```

---

## Appointments

```sql
INSERT INTO appointments
VALUES
(1001,1,101),
(1002,1,102),
(1003,2,103),
(1004,3,102),
(1005,3,104);
```

---

# Final Database Structure

### Patients

| patient_id | patient_name |
| ---------- | ------------ |
| 1          | Rahul        |
| 2          | Priya        |
| 3          | Amit         |

---

### Doctors

| doctor_id | doctor_name | specialization |
| --------- | ----------- | -------------- |
| 101       | Dr. Mehta   | Cardiologist   |
| 102       | Dr. Khan    | Neurologist    |

---

### Appointments

| appointment_id | patient_id | doctor_id |
| -------------- | ---------- | --------- |
| 1001           | 1          | 101       |

---

# Benefits of 3NF

### No Data Redundancy

Before:

```text
Dr. Mehta repeated many times
```

After:

```text
Stored only once
```

---

### Easy Updates

Change specialization:

```sql
UPDATE doctors
SET specialization='Heart Specialist'
WHERE doctor_id=101;
```

Only one row updated.

---

### No Insert Anomaly

Add new doctor:

```sql
INSERT INTO doctors
VALUES
(105,'Dr. Roy','ENT');
```

Possible even without patients.

---

### No Delete Anomaly

Delete patient:

```sql
DELETE FROM patients
WHERE patient_id=1;
```

Doctor information remains safe.

---

# View Complete Data Using JOIN

```sql
SELECT
p.patient_name,
d.doctor_name,
d.specialization
FROM patients p
INNER JOIN appointments a
ON p.patient_id = a.patient_id
INNER JOIN doctors d
ON a.doctor_id = d.doctor_id;
```

---

# Output

| patient_name | doctor_name | specialization |
| ------------ | ----------- | -------------- |
| Rahul        | Dr. Mehta   | Cardiologist   |
| Rahul        | Dr. Khan    | Neurologist    |
| Priya        | Dr. Patel   | Orthopedic     |
| Amit         | Dr. Khan    | Neurologist    |
| Amit         | Dr. Sharma  | Dermatologist  |

---

# Quick Revision

| Form | Rule                              |
| ---- | --------------------------------- |
| UNF  | Multiple values allowed in a cell |
| 1NF  | Atomic values only                |
| 2NF  | Remove partial dependency         |
| 3NF  | Remove transitive dependency      |

---

# Interview Questions

### What is Normalization?

A process of organizing data to reduce redundancy and improve consistency.

---

### What is 1NF?

Each column contains only a single value.

---

### What is 2NF?

1NF + No Partial Dependency.

---

### What is 3NF?

2NF + No Transitive Dependency.

---

### What are the advantages of Normalization?

* Reduced Redundancy
* Better Consistency
* Easier Maintenance
* Improved Data Integrity
* Better Database Design

---

# Final Flow to Teach in Class

```text
UNF
 ↓
1NF
 ↓
2NF
 ↓
3NF
 ↓
Final Hospital Database Design
 ↓
JOIN Queries
```
