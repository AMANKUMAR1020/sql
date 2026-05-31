# 📍 SQL Challenge: Placements

## 📝 Problem Statement

You are given three tables:

- `Students`
- `Friends`
- `Packages`

---

### 👨‍🎓 Students Table

| Column | Type | Description |
|--------|------|-------------|
| ID | Integer | Student ID |
| Name | String | Student Name |

---

### 🤝 Friends Table

| Column | Type | Description |
|--------|------|-------------|
| ID | Integer | Student ID |
| Friend_ID | Integer | Best Friend's ID |

> Each student has only one best friend.

---

### 💰 Packages Table

| Column | Type | Description |
|--------|------|-------------|
| ID | Integer | Student ID |
| Salary | Decimal | Salary offered in $ thousands per month |

---

Write a query to output the names of students whose best friends received a higher salary package than them.

---

## 📌 Sorting Rules

- Order the result by the salary offered to the best friends in ascending order.

---

## 📥 Sample Output

```text
Samantha
Julia
Scarlet
```

---

## 💡 Explanation

Consider the salary comparison:

| Student | Student Salary | Friend Salary | Result |
|---------|----------------|---------------|--------|
| Samantha | 10.06 | 11.55 | Included |
| Julia | 8.15 | 12.12 | Included |
| Scarlet | 9.18 | 15.20 | Included |
| Ashley | 13.15 | 12.12 | Excluded |

Since the best friends of Samantha, Julia, and Scarlet received higher salary offers, their names are displayed.

The output is sorted according to the friend's salary.

---

# 🐬 MySQL Solution

```sql

SELECT s.Name
FROM Students s
JOIN Friends f 
    ON s.ID = f.ID
JOIN Packages p1 
    ON s.ID = p1.ID
JOIN Packages p2 
    ON f.Friend_ID = p2.ID
WHERE p2.Salary > p1.Salary
ORDER BY p2.Salary;

```

---

# ⭕ Oracle SQL Solution

```sql

SET NULL "NULL";
SET FEEDBACK OFF;
SET ECHO OFF;
SET HEADING OFF;
SET WRAP OFF;
SET LINESIZE 10000;
SET TAB OFF;
SET PAGES 0;
SET DEFINE OFF;

SELECT s.Name
FROM Students s
JOIN Friends f 
    ON s.ID = f.ID
JOIN Packages p1 
    ON s.ID = p1.ID
JOIN Packages p2 
    ON f.Friend_ID = p2.ID
WHERE p2.Salary > p1.Salary
ORDER BY p2.Salary;

exit;

```

---

## ✅ Query Breakdown

### 🔹 `JOIN Friends`

```sql
ON s.ID = f.ID
```

Matches each student with their best friend.

---

### 🔹 `JOIN Packages p1`

```sql
ON s.ID = p1.ID
```

Gets the salary package of the student.

---

### 🔹 `JOIN Packages p2`

```sql
ON f.Friend_ID = p2.ID
```

Gets the salary package of the student's best friend.

---

### 🔹 `WHERE p2.Salary > p1.Salary`

Filters students whose best friend received a higher salary.

---

### 🔹 `ORDER BY p2.Salary`

Sorts results by the friend's salary offer in ascending order.

---

## ✅ Final Output Example

```text
Samantha
Julia
Scarlet
```

Meaning:

- Samantha's best friend received a higher salary
- Julia's best friend received a higher salary
- Scarlet's best friend received a higher salary

---