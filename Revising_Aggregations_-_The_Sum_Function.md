# 🏙️ SQL Challenge: Revising Aggregations - The Sum Function


## 📝 Problem Statement
Query the **total population** population of all cities in CITY **where District is California**.

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

SELECT sum(population)
FROM CITY
WHERE District like 'California';

```

## ⭕ Oracle SQL Solution
```sql
SET FEEDBACK OFF;
SET ECHO OFF;
SET HEADING OFF;
SET WRAP OFF;
SET LINESIZE 10000;
SET TAB OFF;

SELECT sum(population)
FROM CITY
WHERE District like 'California';

EXIT;
```