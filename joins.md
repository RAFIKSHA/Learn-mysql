# SQL JOINs Complete Practical Guide (Healthcare Management System)

## Beginner to Industry Level (Step-by-Step)

---

# Project Overview

Healthcare Management System mein 3 tables hain:

```text
Patients
Appointments
Doctors
```

Relationship:

```text
Patients
   |
patient_id
   |
Appointments
   |
doctor_id
   |
Doctors
```

---

# Step 1: Create Database

```sql
CREATE DATABASE healthcare_db;
```

### Purpose

Healthcare Management System ke liye database create karna.

---

# Step 2: Use Database

```sql
USE healthcare_db;
```

### Purpose

Database ko active banana.

---

# Step 3: Create Patients Table

```sql
CREATE TABLE patients(
    patient_id INT PRIMARY KEY,
    patient_name VARCHAR(50),
    city VARCHAR(50)
);
```

### Check Table

```sql
DESC patients;
```

---

# Step 4: Create Doctors Table

```sql
CREATE TABLE doctors(
    doctor_id INT PRIMARY KEY,
    doctor_name VARCHAR(50),
    specialization VARCHAR(50)
);
```

### Check Table

```sql
DESC doctors;
```

---

# Step 5: Create Appointments Table

```sql
CREATE TABLE appointments(
    appointment_id INT PRIMARY KEY,
    patient_id INT,
    doctor_id INT,
    appointment_date DATE,

    FOREIGN KEY(patient_id)
    REFERENCES patients(patient_id),

    FOREIGN KEY(doctor_id)
    REFERENCES doctors(doctor_id)
);
```

### Check Table

```sql
DESC appointments;
```

---

# Step 6: Insert Data into Patients

```sql
INSERT INTO patients VALUES
(1,'Rohan','Pune'),
(2,'Priya','Mumbai'),
(3,'Amit','Delhi'),
(4,'Sneha','Bangalore'),
(5,'Rahul','Hyderabad');
```

### View Data

```sql
SELECT * FROM patients;
```

### Output

| patient_id | patient_name | city      |
| ---------- | ------------ | --------- |
| 1          | Rohan        | Pune      |
| 2          | Priya        | Mumbai    |
| 3          | Amit         | Delhi     |
| 4          | Sneha        | Bangalore |
| 5          | Rahul        | Hyderabad |

---

# Step 7: Insert Data into Doctors

```sql
INSERT INTO doctors VALUES
(101,'Dr. Sharma','Cardiologist'),
(102,'Dr. Khan','Dermatologist'),
(103,'Dr. Mehta','Orthopedic'),
(104,'Dr. Patel','Neurologist');
```

### View Data

```sql
SELECT * FROM doctors;
```

### Output

| doctor_id | doctor_name | specialization |
| --------- | ----------- | -------------- |
| 101       | Dr. Sharma  | Cardiologist   |
| 102       | Dr. Khan    | Dermatologist  |
| 103       | Dr. Mehta   | Orthopedic     |
| 104       | Dr. Patel   | Neurologist    |

---

# Step 8: Insert Data into Appointments

```sql
INSERT INTO appointments VALUES
(1,1,101,'2026-06-01'),
(2,2,102,'2026-06-02'),
(3,3,103,'2026-06-03'),
(4,4,101,'2026-06-04');
```

### View Data

```sql
SELECT * FROM appointments;
```

### Output

| appointment_id | patient_id | doctor_id | appointment_date |
| -------------- | ---------- | --------- | ---------------- |
| 1              | 1          | 101       | 2026-06-01       |
| 2              | 2          | 102       | 2026-06-02       |
| 3              | 3          | 103       | 2026-06-03       |
| 4              | 4          | 101       | 2026-06-04       |

---

# Understanding the Data

```text
Rohan  → Dr. Sharma
Priya  → Dr. Khan
Amit   → Dr. Mehta
Sneha  → Dr. Sharma

Rahul → No Appointment

Dr. Patel → No Patients
```

---

# JOIN Learning Phase 1

# INNER JOIN (2 Tables)

## Requirement

Show Patient Name and Appointment Date

### Query

```sql
SELECT
patient_name,
appointment_date
FROM patients
INNER JOIN appointments
ON patients.patient_id = appointments.patient_id;
```

### Output

| patient_name | appointment_date |
| ------------ | ---------------- |
| Rohan        | 2026-06-01       |
| Priya        | 2026-06-02       |
| Amit         | 2026-06-03       |
| Sneha        | 2026-06-04       |

### Rule

```text
Only Matching Records
```

---

# LEFT JOIN (2 Tables)

## Requirement

Show All Patients

### Query

```sql
SELECT
patient_name,
appointment_date
FROM patients
LEFT JOIN appointments
ON patients.patient_id = appointments.patient_id;
```

### Output

| patient_name | appointment_date |
| ------------ | ---------------- |
| Rohan        | 2026-06-01       |
| Priya        | 2026-06-02       |
| Amit         | 2026-06-03       |
| Sneha        | 2026-06-04       |
| Rahul        | NULL             |

### Rule

```text
All Records From Left Table
```

---

# RIGHT JOIN (2 Tables)

## Requirement

Show All Appointments

### Query

```sql
SELECT
patient_name,
appointment_date
FROM patients
RIGHT JOIN appointments
ON patients.patient_id = appointments.patient_id;
```

### Output

| patient_name | appointment_date |
| ------------ | ---------------- |
| Rohan        | 2026-06-01       |
| Priya        | 2026-06-02       |
| Amit         | 2026-06-03       |
| Sneha        | 2026-06-04       |

### Rule

```text
All Records From Right Table
```

---

# FULL OUTER JOIN

## MySQL Method

```sql
SELECT
patient_name,
appointment_date
FROM patients
LEFT JOIN appointments
ON patients.patient_id=appointments.patient_id

UNION

SELECT
patient_name,
appointment_date
FROM patients
RIGHT JOIN appointments
ON patients.patient_id=appointments.patient_id;
```

### Output

| patient_name | appointment_date |
| ------------ | ---------------- |
| Rohan        | 2026-06-01       |
| Priya        | 2026-06-02       |
| Amit         | 2026-06-03       |
| Sneha        | 2026-06-04       |
| Rahul        | NULL             |

---

# CROSS JOIN

## Requirement

Generate All Patient-Doctor Combinations

### Query

```sql
SELECT
patient_name,
doctor_name
FROM patients
CROSS JOIN doctors;
```

### Formula

```text
Rows = Patients × Doctors

5 × 4 = 20 Rows
```

### Sample Output

| patient_name | doctor_name |
| ------------ | ----------- |
| Rohan        | Dr. Sharma  |
| Rohan        | Dr. Khan    |
| Rohan        | Dr. Mehta   |
| Rohan        | Dr. Patel   |

---

# JOIN Learning Phase 2

# INNER JOIN (3 Tables)

Now real industry-style JOIN.

## Requirement

Show Patient Name, Doctor Name, Specialization and Appointment Date

### Query

```sql
SELECT
patient_name,
doctor_name,
specialization,
appointment_date
FROM patients
INNER JOIN appointments
ON patients.patient_id = appointments.patient_id
INNER JOIN doctors
ON appointments.doctor_id = doctors.doctor_id;
```

### Output

| patient_name | doctor_name | specialization | appointment_date |
| ------------ | ----------- | -------------- | ---------------- |
| Rohan        | Dr. Sharma  | Cardiologist   | 2026-06-01       |
| Priya        | Dr. Khan    | Dermatologist  | 2026-06-02       |
| Amit         | Dr. Mehta   | Orthopedic     | 2026-06-03       |
| Sneha        | Dr. Sharma  | Cardiologist   | 2026-06-04       |

### Explanation

```text
Step 1:
Patients + Appointments

Step 2:
Result + Doctors

Final Report Generated
```

---

# LEFT JOIN (3 Tables)

## Requirement

Show All Patients Even Without Appointments

### Query

```sql
SELECT
patient_name,
doctor_name,
appointment_date
FROM patients
LEFT JOIN appointments
ON patients.patient_id = appointments.patient_id
LEFT JOIN doctors
ON appointments.doctor_id = doctors.doctor_id;
```

### Output

| patient_name | doctor_name | appointment_date |
| ------------ | ----------- | ---------------- |
| Rohan        | Dr. Sharma  | 2026-06-01       |
| Priya        | Dr. Khan    | 2026-06-02       |
| Amit         | Dr. Mehta   | 2026-06-03       |
| Sneha        | Dr. Sharma  | 2026-06-04       |
| Rahul        | NULL        | NULL             |

---

# RIGHT JOIN (3 Tables)

## Requirement

Show All Doctors

### Query

```sql
SELECT
patient_name,
doctor_name,
appointment_date
FROM patients
RIGHT JOIN appointments
ON patients.patient_id = appointments.patient_id
RIGHT JOIN doctors
ON appointments.doctor_id = doctors.doctor_id;
```

### Output

| patient_name | doctor_name | appointment_date |
| ------------ | ----------- | ---------------- |
| Rohan        | Dr. Sharma  | 2026-06-01       |
| Sneha        | Dr. Sharma  | 2026-06-04       |
| Priya        | Dr. Khan    | 2026-06-02       |
| Amit         | Dr. Mehta   | 2026-06-03       |
| NULL         | Dr. Patel   | NULL             |

---

# GROUP BY + JOIN

## Count Patients Per Doctor

### Query

```sql
SELECT
doctor_name,
COUNT(patient_id) AS Total_Patients
FROM doctors
LEFT JOIN appointments
ON doctors.doctor_id = appointments.doctor_id
GROUP BY doctor_name;
```

### Output

| doctor_name | Total_Patients |
| ----------- | -------------- |
| Dr. Sharma  | 2              |
| Dr. Khan    | 1              |
| Dr. Mehta   | 1              |
| Dr. Patel   | 0              |

---

# NULL Handling + JOIN

## Doctors Without Appointments

### Query

```sql
SELECT
doctor_name
FROM doctors
LEFT JOIN appointments
ON doctors.doctor_id = appointments.doctor_id
WHERE appointment_id IS NULL;
```

### Output

| doctor_name |
| ----------- |
| Dr. Patel   |

---

# Patients Without Appointment

### Query

```sql
SELECT
patient_name
FROM patients
LEFT JOIN appointments
ON patients.patient_id = appointments.patient_id
WHERE appointment_id IS NULL;
```

### Output

| patient_name |
| ------------ |
| Rahul        |

---

# Aggregate Function + JOIN

## Most Busy Doctor

### Query

```sql
SELECT
doctor_name,
COUNT(*) AS Total_Appointments
FROM doctors
JOIN appointments
ON doctors.doctor_id = appointments.doctor_id
GROUP BY doctor_name
ORDER BY Total_Appointments DESC
LIMIT 1;
```

### Output

| doctor_name | Total_Appointments |
| ----------- | ------------------ |
| Dr. Sharma  | 2                  |

---

# Interview Question

## Does JOIN Need Foreign Key?

### Answer

**No.**

JOIN only needs matching columns.

Example:

```sql
SELECT *
FROM patients
JOIN appointments
ON patients.patient_id = appointments.patient_id;
```

Works perfectly.

### Then Why Use Foreign Key?

* Data Integrity
* Prevent Invalid Data
* Maintain Relationships
* Industry Standard Practice

---

# Final JOIN Summary

| JOIN Type            | Purpose                      |
| -------------------- | ---------------------------- |
| INNER JOIN           | Only Matching Records        |
| LEFT JOIN            | All Left Table Records       |
| RIGHT JOIN           | All Right Table Records      |
| FULL OUTER JOIN      | All Records From Both Tables |
| CROSS JOIN           | Every Possible Combination   |
| SELF JOIN            | Table Joined With Itself     |
| GROUP BY + JOIN      | Reporting                    |
| NULL Handling + JOIN | Missing Data Analysis        |

### Teaching Flow

```text
Database Creation
↓
Table Creation
↓
Insert Records
↓
SELECT *
↓
INNER JOIN (2 Tables)
↓
LEFT JOIN
↓
RIGHT JOIN
↓
FULL OUTER JOIN
↓
CROSS JOIN
↓
INNER JOIN (3 Tables)
↓
GROUP BY + JOIN
↓
NULL Handling + JOIN
↓
Industry Reports
```

Ye sequence beginners ko JOINs zero se industry level tak samjha deta hai aur classroom training ke liye kaafi effective rahega.
