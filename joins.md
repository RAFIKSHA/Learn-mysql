# SQL JOINs Complete Practical Guide (Healthcare Management System)

This project is much closer to real industry use because hospitals store data in multiple tables and JOINs are used daily to generate reports.

---

# Project: Healthcare Management System

## Database Tables

1. Patients
2. Doctors
3. Appointments

Relationship:

```
Patients
    |
    |
Appointments
    |
    |
Doctors
```

A patient books an appointment with a doctor.

---

# Step 1: Create Database

```sql
CREATE DATABASE healthcare_db;
```

```sql
USE healthcare_db;
```

---

# Step 2: Create Patients Table

```sql
CREATE TABLE patients (
    patient_id INT PRIMARY KEY,
    patient_name VARCHAR(50),
    city VARCHAR(50)
);
```

---

# Step 3: Create Doctors Table

```sql
CREATE TABLE doctors (
    doctor_id INT PRIMARY KEY,
    doctor_name VARCHAR(50),
    specialization VARCHAR(50)
);
```

---

# Step 4: Create Appointments Table

```sql
CREATE TABLE appointments (
    appointment_id INT PRIMARY KEY,
    patient_id INT,
    doctor_id INT,
    appointment_date DATE
);
```

---

# Step 5: Insert Data

## Patients

```sql
INSERT INTO patients VALUES
(1,'Rohan','Pune'),
(2,'Priya','Mumbai'),
(3,'Amit','Delhi'),
(4,'Sneha','Bangalore'),
(5,'Rahul','Hyderabad');
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

## Doctors

```sql
INSERT INTO doctors VALUES
(101,'Dr. Sharma','Cardiologist'),
(102,'Dr. Khan','Dermatologist'),
(103,'Dr. Mehta','Orthopedic'),
(104,'Dr. Patel','Neurologist');
```

### Output

| doctor_id | doctor_name | specialization |
| --------- | ----------- | -------------- |
| 101       | Dr. Sharma  | Cardiologist   |
| 102       | Dr. Khan    | Dermatologist  |
| 103       | Dr. Mehta   | Orthopedic     |
| 104       | Dr. Patel   | Neurologist    |

---

## Appointments

```sql
INSERT INTO appointments VALUES
(1,1,101,'2026-06-01'),
(2,2,102,'2026-06-02'),
(3,3,103,'2026-06-03'),
(4,4,101,'2026-06-04');
```

### Output

| appointment_id | patient_id | doctor_id | appointment_date |
| -------------- | ---------- | --------- | ---------------- |
| 1              | 1          | 101       | 2026-06-01       |
| 2              | 2          | 102       | 2026-06-02       |
| 3              | 3          | 103       | 2026-06-03       |
| 4              | 4          | 101       | 2026-06-04       |

Notice:

* Rahul (Patient ID 5) has no appointment.
* Dr. Patel (104) has no patients.

These unmatched records help explain JOINs.

---

# INNER JOIN

### Business Requirement

Show patients along with the doctor they consulted.

### Query

```sql
SELECT
p.patient_name,
d.doctor_name,
d.specialization,
a.appointment_date
FROM patients p
INNER JOIN appointments a
ON p.patient_id = a.patient_id
INNER JOIN doctors d
ON a.doctor_id = d.doctor_id;
```

### Expected Output

| patient_name | doctor_name | specialization | appointment_date |
| ------------ | ----------- | -------------- | ---------------- |
| Rohan        | Dr. Sharma  | Cardiologist   | 2026-06-01       |
| Priya        | Dr. Khan    | Dermatologist  | 2026-06-02       |
| Amit         | Dr. Mehta   | Orthopedic     | 2026-06-03       |
| Sneha        | Dr. Sharma  | Cardiologist   | 2026-06-04       |

**Explanation:** Only matching records are shown.

---

# LEFT JOIN

### Business Requirement

Show all patients, even if they have not booked an appointment.

### Query

```sql
SELECT
p.patient_name,
d.doctor_name,
a.appointment_date
FROM patients p
LEFT JOIN appointments a
ON p.patient_id = a.patient_id
LEFT JOIN doctors d
ON a.doctor_id = d.doctor_id;
```

### Expected Output

| patient_name | doctor_name | appointment_date |
| ------------ | ----------- | ---------------- |
| Rohan        | Dr. Sharma  | 2026-06-01       |
| Priya        | Dr. Khan    | 2026-06-02       |
| Amit         | Dr. Mehta   | 2026-06-03       |
| Sneha        | Dr. Sharma  | 2026-06-04       |
| Rahul        | NULL        | NULL             |

**Explanation:** All patients are displayed. Rahul has no appointment.

---

# RIGHT JOIN

### Business Requirement

Show all doctors, even if they have no appointments.

### Query

```sql
SELECT
p.patient_name,
d.doctor_name,
a.appointment_date
FROM patients p
RIGHT JOIN appointments a
ON p.patient_id = a.patient_id
RIGHT JOIN doctors d
ON a.doctor_id = d.doctor_id;
```

### Expected Output

| patient_name | doctor_name | appointment_date |
| ------------ | ----------- | ---------------- |
| Rohan        | Dr. Sharma  | 2026-06-01       |
| Sneha        | Dr. Sharma  | 2026-06-04       |
| Priya        | Dr. Khan    | 2026-06-02       |
| Amit         | Dr. Mehta   | 2026-06-03       |
| NULL         | Dr. Patel   | NULL             |

**Explanation:** Dr. Patel appears even though no patient has booked an appointment.

---

# FULL OUTER JOIN

### MySQL Note

MySQL does not support FULL OUTER JOIN directly.

We simulate it using UNION.

### Query

```sql
SELECT
p.patient_name,
d.doctor_name
FROM patients p
LEFT JOIN appointments a
ON p.patient_id=a.patient_id
LEFT JOIN doctors d
ON a.doctor_id=d.doctor_id

UNION

SELECT
p.patient_name,
d.doctor_name
FROM patients p
RIGHT JOIN appointments a
ON p.patient_id=a.patient_id
RIGHT JOIN doctors d
ON a.doctor_id=d.doctor_id;
```

### Expected Output

| patient_name | doctor_name |
| ------------ | ----------- |
| Rohan        | Dr. Sharma  |
| Priya        | Dr. Khan    |
| Amit         | Dr. Mehta   |
| Sneha        | Dr. Sharma  |
| Rahul        | NULL        |
| NULL         | Dr. Patel   |

**Explanation:** All records from both sides are included.

---

# CROSS JOIN

### Business Requirement

Generate every possible Patient–Doctor combination.

### Query

```sql
SELECT
p.patient_name,
d.doctor_name
FROM patients p
CROSS JOIN doctors d;
```

### Expected Output (Partial)

| patient_name | doctor_name |
| ------------ | ----------- |
| Rohan        | Dr. Sharma  |
| Rohan        | Dr. Khan    |
| Rohan        | Dr. Mehta   |
| Rohan        | Dr. Patel   |
| Priya        | Dr. Sharma  |
| Priya        | Dr. Khan    |
| ...          | ...         |

Total Rows:

```
5 Patients × 4 Doctors = 20 Rows
```

---

# Self JOIN (Advanced Interview Question)

Suppose doctors refer patients to other doctors.

### Table

```sql
CREATE TABLE doctor_referrals (
    doctor_id INT,
    referred_by INT
);
```

### Query

```sql
SELECT
d1.doctor_name AS Doctor,
d2.doctor_name AS Referred_By
FROM doctors d1
JOIN doctors d2
ON d1.doctor_id = d2.doctor_id;
```

Used when a table references itself.

---

# Industry-Level Reporting Queries

### Count Patients Per Doctor

```sql
SELECT
d.doctor_name,
COUNT(a.patient_id) AS Total_Patients
FROM doctors d
LEFT JOIN appointments a
ON d.doctor_id=a.doctor_id
GROUP BY d.doctor_name;
```

### Find Doctors With No Appointments

```sql
SELECT
d.doctor_name
FROM doctors d
LEFT JOIN appointments a
ON d.doctor_id=a.doctor_id
WHERE a.appointment_id IS NULL;
```

### Find Patients Without Appointment

```sql
SELECT
p.patient_name
FROM patients p
LEFT JOIN appointments a
ON p.patient_id=a.patient_id
WHERE a.appointment_id IS NULL;
```

### Find Most Busy Doctor

```sql
SELECT
d.doctor_name,
COUNT(*) AS Total_Appointments
FROM doctors d
JOIN appointments a
ON d.doctor_id=a.doctor_id
GROUP BY d.doctor_name
ORDER BY Total_Appointments DESC
LIMIT 1;
```

This dataset is excellent for teaching:

* INNER JOIN
* LEFT JOIN
* RIGHT JOIN
* FULL OUTER JOIN
* CROSS JOIN
* SELF JOIN
* GROUP BY with JOIN
* NULL handling
* Real hospital reporting scenarios used in industry.
