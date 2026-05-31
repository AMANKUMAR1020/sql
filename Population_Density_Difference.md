# 🏙️ SQL Challenge: Population Density Difference


## 📝 Problem Statement
Query the `difference` between the `maximum and minimum` `populations` in `CITY`.

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

select max(population) - min(population)
from city;


```


## ⭕ Oracle SQL Solution

```sql
SET FEEDBACK OFF;
SET ECHO OFF;
SET HEADING OFF;
SET WRAP OFF;
SET LINESIZE 10000;
SET TAB OFF;

select max(population) - min(population)
from city;

EXIT;
```