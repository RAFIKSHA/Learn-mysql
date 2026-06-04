# 1NF (First Normal Form)

### Rule:

✅ Each column contains atomic values.

✅ No repeating groups.

### ❌ Wrong Example

| Student_ID | Name  | Skills            |
| ---------- | ----- | ----------------- |
| 101        | Rafik | Python, SQL, Java |

Problem:

* Skills column mein multiple values hain.
* One Cell ≠ One Value

### ✅ Correct Example

| Student_ID | Name  | Skill  |
| ---------- | ----- | ------ |
| 101        | Rafik | Python |
| 101        | Rafik | SQL    |
| 101        | Rafik | Java   |

### Definition

> Every column should contain atomic (single) values and each row should be unique.

### Shortcut

**One Cell = One Value**

---

# 2NF (Second Normal Form)

### Rule:

✅ Table should already be in 1NF.

✅ No Partial Dependency.

### What is Partial Dependency?

Jab non-key column sirf primary key ke ek part par depend kare, poori key par nahi.

### ❌ Wrong Example

| Student_ID | Course_ID | Student_Name | Course_Name |
| ---------- | --------- | ------------ | ----------- |
| 101        | C1        | Rafik        | Python      |
| 101        | C2        | Rafik        | SQL         |

Composite Primary Key = (Student_ID, Course_ID)

Problem:

* Student_Name sirf Student_ID par depend karta hai.
* Course_Name sirf Course_ID par depend karta hai.

Ye Partial Dependency hai.

---

### ✅ Correct Example

### Students

| Student_ID | Student_Name |
| ---------- | ------------ |
| 101        | Rafik        |

### Courses

| Course_ID | Course_Name |
| --------- | ----------- |
| C1        | Python      |
| C2        | SQL         |

### Enrollment

| Student_ID | Course_ID |
| ---------- | --------- |
| 101        | C1        |
| 101        | C2        |

### Definition

> Every non-key attribute must depend on the whole primary key.

### Shortcut

**Depend on Full Key, Not Part of Key**

---

# 3NF (Third Normal Form)

### Rule:

✅ Table should already be in 2NF.

✅ No Transitive Dependency.

### What is Transitive Dependency?

Jab ek non-key column doosre non-key column par depend kare.

### ❌ Wrong Example

| Emp_ID | Emp_Name | Dept_ID | Dept_Name |
| ------ | -------- | ------- | --------- |
| 1      | Ali      | D1      | HR        |
| 2      | Sara     | D2      | IT        |

Problem:

* Emp_ID → Dept_ID
* Dept_ID → Dept_Name

Yani Dept_Name indirectly Emp_ID par depend kar raha hai.

Ye Transitive Dependency hai.

---

### ✅ Correct Example

### Employees

| Emp_ID | Emp_Name | Dept_ID |
| ------ | -------- | ------- |
| 1      | Ali      | D1      |
| 2      | Sara     | D2      |

### Departments

| Dept_ID | Dept_Name |
| ------- | --------- |
| D1      | HR        |
| D2      | IT        |

Ab redundancy remove ho gayi.

### Definition

> Non-key attributes should depend only on the primary key and not on other non-key attributes.

### Shortcut

**Non-Key should not depend on Non-Key**

---

# One-Line Interview Revision

### 1NF

**One Cell = One Value**

### 2NF

**Depend on Full Key**

### 3NF

**Non-Key should not depend on Non-Key**

---

### Easy Memory Trick

**1NF → Atomic Values**
**2NF → Remove Partial Dependency**
**3NF → Remove Transitive Dependency**

Yaad rakhne ka formula:

**Atomic → Partial → Transitive**

(1NF → 2NF → 3NF) 🚀
