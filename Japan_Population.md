# 🏙️ SQL Challenge: Japan Population


## 📝 Problem Statement
Query the **sum of the populations** for all cities in the `CITY` table where the `COUNTRYCODE` is **'JPN'** (Japan).

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

A single integer representing the **total population of all Japanese cities**.

---

## 🐬 MySQL Solution

```sql
SELECT SUM(population)
FROM CITY
WHERE countrycode = 'JPN';
```


## ⭕ Oracle SQL Solution

```sql
SET FEEDBACK OFF;
SET ECHO OFF;
SET HEADING OFF;
SET WRAP OFF;
SET LINESIZE 10000;
SET TAB OFF;

SELECT SUM(population)
FROM CITY
WHERE countrycode = 'JPN';

EXIT;
```