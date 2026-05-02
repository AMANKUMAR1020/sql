# 🏙️ SQL Challenge: Employee Names

## 📝 Problem Statement
Write a query that **prints a list of employee names** (i.e., the `name` attribute) from the **Employee** table in **alphabetical order**.

---

## 📊 Input Format

The `Employee` table contains the following columns:

| Column       | Type    | Description                                      |
|--------------|---------|--------------------------------------------------|
| employee_id  | Integer | Employee's unique ID                             |
| name         | String  | Employee's name                                  |
| months       | Integer | Number of months worked at the company           |
| salary       | Integer | Monthly salary of the employee                   |

---

## 📥 Sample Input

| employee_id | name     | months | salary |
|------------|----------|--------|--------|
| 12228      | Rose     | 15     | 1968   |
| 33645      | Angela   | 1      | 3443   |
| 45692      | Frank    | 17     | 1608   |
| 56118      | Patrick  | 7      | 1345   |
| 59725      | Lisa     | 11     | 2330   |
| 74197      | Kimberly | 16     | 4372   |
| 78454      | Bonnie   | 8      | 1771   |
| 83565      | Michael  | 6      | 2017   |
| 98607      | Todd     | 5      | 3396   |
| 99989      | Joe      | 9      | 3573   |

---

## 📤 Sample Output
Angela
Bonnie
Frank
Joe
Kimberly
Lisa
Michael
Patrick
Rose
Todd


---

## 🐬 MySQL Solution

```sql
SELECT name
FROM Employee
ORDER BY name;
```

## ⭕ Oracle SQL Solution
```sql
SET FEEDBACK OFF;
SET ECHO OFF;
SET HEADING OFF;
SET WRAP OFF;
SET LINESIZE 10000;
SET TAB OFF;

SELECT name
FROM Employee
ORDER BY name;

EXIT;