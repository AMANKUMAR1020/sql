# 📍 SQL Challenge: Top Earners

## 📝 Problem Statement

We define an employee's total earnings as:

```text
Salary × Months
```

Write a query to find:

1. The **maximum total earnings** for all employees.
2. The **total number of employees** who have the maximum earnings.

---

## 🔗 HackerRank Problem Link

https://www.hackerrank.com/challenges/earnings-of-employees/problem?isFullScreen=true

---

## 📊 Input Format

### 👨‍💼 EMPLOYEE Table

| Column      | Type    | Description                  |
|-------------|---------|------------------------------|
| employee_id | Integer | Employee ID                  |
| name        | String  | Employee Name                |
| months      | Integer | Number of months worked      |
| salary      | Integer | Monthly salary               |

---

## 📤 Expected Output

Print:

```text
maximum_total_earnings employee_count
```

Where:

- `maximum_total_earnings` → Highest earnings among all employees
- `employee_count` → Number of employees having that earning

---

## 💡 Explanation

The query calculates:

```text
salary * months
```

for each employee.

Then:

- Finds the **maximum earning**
- Counts how many employees earned that amount

---

# 🐬 MySQL Solution

```sql
SELECT 
    MAX(salary * months) AS max_earnings,
    COUNT(*) AS employee_count
FROM employee
WHERE salary * months = (
    SELECT MAX(salary * months)
    FROM employee
);
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

SELECT 
    MAX(salary * months) AS max_earnings,
    COUNT(*) AS employee_count
FROM employee
WHERE salary * months = (
    SELECT MAX(salary * months)
    FROM employee
);

exit;
```

---

## ✅ Query Breakdown

### 🔹 `salary * months`

Calculates the total earnings for each employee.

Example:

| Salary | Months | Earnings |
|--------|--------|----------|
| 2000   | 10     | 20000    |

---

### 🔹 `MAX(salary * months)`

Finds the highest earning among all employees.

---

### 🔹 `COUNT(*)`

Counts how many employees have the highest earning.

---

## ✅ Final Output Example

```text
69952 1
```

Meaning:

- Highest earning = `69952`
- Number of employees with this earning = `1`

---