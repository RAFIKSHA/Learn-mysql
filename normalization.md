# Normalization Practical Guide (Using Hospital Database)
---

# What is Normalization?

**Normalization is the process of organizing data into multiple related tables to reduce data redundancy and improve data consistency.**

### Goal

✅ Remove duplicate data

✅ Avoid update problems

✅ Improve database design

✅ Maintain data integrity

---

# Step 1: Create Database

```sql
CREATE DATABASE hospital_db;

USE hospital_db;
```

---

# Step 2: Create a Bad Table (Without Normalization)

```sql
CREATE TABLE patient_records(
    patient_id INT,
    patient_name VARCHAR(100),
    doctor_name VARCHAR(100),
    specialization VARCHAR(100)
);
```

---

# Step 3: Insert Data

```sql
INSERT INTO patient_records
VALUES
(1,'Rahul','Dr. Mehta','Cardiologist'),
(2,'Priya','Dr. Khan','Neurologist'),
(3,'Amit','Dr. Mehta','Cardiologist'),
(4,'Rohit','Dr. Patel','Orthopedic');
```

---

# Current Data

| patient_id | patient_name | doctor_name | specialization |
| ---------- | ------------ | ----------- | -------------- |
| 1          | Rahul        | Dr. Mehta   | Cardiologist   |
| 2          | Priya        | Dr. Khan    | Neurologist    |
| 3          | Amit         | Dr. Mehta   | Cardiologist   |
| 4          | Rohit        | Dr. Patel   | Orthopedic     |

---

# Step 4: Identify the Problem

Notice:

```text
Dr. Mehta appears multiple times.
Cardiologist appears multiple times.
```

Duplicate data exists.

This is called:

# Data Redundancy

---

# Problem 1: Update Anomaly

Suppose Dr. Mehta becomes:

```text
Heart Specialist
```

Now we must update multiple rows.

```sql
UPDATE patient_records
SET specialization='Heart Specialist'
WHERE doctor_name='Dr. Mehta';
```

---

### Risk

If one row is updated and another is forgotten:

| patient_name | doctor_name | specialization   |
| ------------ | ----------- | ---------------- |
| Rahul        | Dr. Mehta   | Heart Specialist |
| Amit         | Dr. Mehta   | Cardiologist     |

Now data becomes inconsistent.

---

# Problem 2: Insert Anomaly

Suppose a new doctor joins.

```text
Dr. Sharma
Dermatologist
```

But no patient has visited yet.

Can we insert only doctor information?

❌ No

Because patient details are required.

---

# Problem 3: Delete Anomaly

Suppose:

```sql
DELETE FROM patient_records
WHERE patient_id=2;
```

Priya was the only patient of Dr. Khan.

After deletion:

```text
Dr. Khan information is lost.
```

This is called:

# Delete Anomaly

---

# Conclusion

Current design has:

❌ Data Redundancy

❌ Update Anomaly

❌ Insert Anomaly

❌ Delete Anomaly

Need a better design.

---

# Step 5: Apply Normalization

Separate data into logical tables.

---

# Create Patients Table

```sql
CREATE TABLE patients(
    patient_id INT PRIMARY KEY,
    patient_name VARCHAR(100)
);
```

---

# Create Doctors Table

```sql
CREATE TABLE doctors(
    doctor_id INT PRIMARY KEY,
    doctor_name VARCHAR(100),
    specialization VARCHAR(100)
);
```

---

# Create Appointments Table

```sql
CREATE TABLE appointments(
    appointment_id INT PRIMARY KEY,
    patient_id INT,
    doctor_id INT
);
```

---

# Insert Patients

```sql
INSERT INTO patients
VALUES
(1,'Rahul'),
(2,'Priya'),
(3,'Amit'),
(4,'Rohit');
```

---

# Insert Doctors

```sql
INSERT INTO doctors
VALUES
(101,'Dr. Mehta','Cardiologist'),
(102,'Dr. Khan','Neurologist'),
(103,'Dr. Patel','Orthopedic');
```

---

# Insert Appointments

```sql
INSERT INTO appointments
VALUES
(1001,1,101),
(1002,2,102),
(1003,3,101),
(1004,4,103);
```

---

# New Structure

### Patients

| patient_id | patient_name |
| ---------- | ------------ |
| 1          | Rahul        |
| 2          | Priya        |

---

### Doctors

| doctor_id | doctor_name | specialization |
| --------- | ----------- | -------------- |
| 101       | Dr. Mehta   | Cardiologist   |

---

### Appointments

| appointment_id | patient_id | doctor_id |
| -------------- | ---------- | --------- |
| 1001           | 1          | 101       |

---

# Why is this Better?

### Doctor Information Stored Once

Before:

```text
Dr. Mehta repeated many times
```

After:

```text
Dr. Mehta stored only once
```

No redundancy.

---

# Update Example

Suppose specialization changes.

Only one row needs updating.

```sql
UPDATE doctors
SET specialization='Heart Specialist'
WHERE doctor_id=101;
```

Done.

Every appointment automatically reflects the change.

---

# Insert Example

New doctor joins.

```sql
INSERT INTO doctors
VALUES
(104,'Dr. Sharma','Dermatologist');
```

Possible even if no patient exists.

---

# Delete Example

Delete patient:

```sql
DELETE FROM patients
WHERE patient_id=2;
```

Doctor information remains safe.

---

# Viewing Complete Data

Use JOIN

```sql
SELECT
p.patient_name,
d.doctor_name,
d.specialization
FROM patients p
INNER JOIN appointments a
ON p.patient_id=a.patient_id
INNER JOIN doctors d
ON a.doctor_id=d.doctor_id;
```

---

# Output

| patient_name | doctor_name | specialization |
| ------------ | ----------- | -------------- |
| Rahul        | Dr. Mehta   | Cardiologist   |
| Priya        | Dr. Khan    | Neurologist    |
| Amit         | Dr. Mehta   | Cardiologist   |
| Rohit        | Dr. Patel   | Orthopedic     |

Students will notice:

**Output is the same as the original table, but the database design is much better.**

---

# Explain 1NF, 2NF, 3NF in This Example

## 1NF (First Normal Form)

Rule:

```text
No repeating groups
No multiple values in one column
```

Bad:

| patient_id | doctor_names        |
| ---------- | ------------------- |
| 1          | Dr. Mehta, Dr. Khan |

Good:

| patient_id | doctor_name |
| ---------- | ----------- |
| 1          | Dr. Mehta   |

---

## 2NF (Second Normal Form)

Rule:

```text
Remove partial dependency
```

Doctor details should not depend on patient information.

Create separate Doctors table.

---

## 3NF (Third Normal Form)

Rule:

```text
Remove transitive dependency
```

Specialization depends on Doctor.

Store it in Doctors table, not Patients table.

---

# Final Summary

### Before Normalization

One table

```text
patient_records
```

Problems:

❌ Duplicate Data

❌ Update Anomaly

❌ Insert Anomaly

❌ Delete Anomaly

---

### After Normalization

Three tables

```text
patients
doctors
appointments
```

Benefits:

✅ No redundancy

✅ Better consistency

✅ Easy maintenance

✅ Industry-standard design

✅ Supports JOIN operations

This flow works very well in class because students first **see the problem**, then understand **why normalization is required**, and finally implement the **normalized design** themselves.
