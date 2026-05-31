# 🏙️ SQL Challenge: Average Population


## 📝 Problem Statement
Query the average population for all cities in `CITY`, `rounded down` to the `nearest integer`.

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

SELECT round(avg(population),0)
FROM CITY;

```

## ⭕ Oracle SQL Solution
```sql
SET FEEDBACK OFF;
SET ECHO OFF;
SET HEADING OFF;
SET WRAP OFF;
SET LINESIZE 10000;
SET TAB OFF;

SELECT round(avg(population),0)
FROM CITY;


EXIT;
```