# 🏙️ SQL Challenge: Revising Aggregation - The Count Function


## 📝 Problem Statement
Query the **number of cities** in the `CITY` table having a **population greater than 100000**.

---

## 📊 Input Format

The `CITY` table contains the following columns:

| Column       | Type    | Description                     |
|--------------|---------|---------------------------------|
| ID           | Integer | Unique city ID                 |
| NAME         | String  | Name of the city               |
| COUNTRYCODE  | String  | Country code (3-letter)        |
| DISTRICT     | String  | District/State                |
| POPULATION   | Integer | Population of the city         |

---

## 📤 Expected Output

A single integer representing the **count of cities** with population greater than **100000**.

---

## 🐬 MySQL Solution

```sql
SELECT COUNT(*)
FROM CITY
WHERE population > 100000;
```

## ⭕ Oracle SQL Solution
```sql
SET FEEDBACK OFF;
SET ECHO OFF;
SET HEADING OFF;
SET WRAP OFF;
SET LINESIZE 10000;
SET TAB OFF;

SELECT COUNT(*)
FROM CITY
WHERE population > 100000;

EXIT;
```