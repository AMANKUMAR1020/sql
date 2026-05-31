# 📍 SQL Challenge: Population Census


## 📝 Problem Statement
Given the `CITY` and `COUNTRY tables`, `query the names of all cities` where the `CONTINENT is 'Africa'`.

**Note**: CITY.CountryCode and COUNTRY.Code are matching key columns.

📌 Note:
- `CITY.CountryCode` and `COUNTRY.Code` are matching key columns.

---

## 📊 Input Format

### 🌆 CITY Table

| Column       | Type    | Description                     |
|--------------|---------|---------------------------------|
| ID           | Integer | Unique city ID                  |
| NAME         | String  | Name of the city                |
| COUNTRYCODE  | String  | Country code                    |
| DISTRICT     | String  | District/State                  |
| POPULATION   | Integer | Population of the city          |

---

### 🌍 COUNTRY Table

| Column     | Type   | Description                |
|------------|--------|----------------------------|
| CODE       | String | Country code (Primary Key) |
| NAME       | String | Country name               |
| CONTINENT  | String | Continent name             |
| REGION     | String | Region                     |
| POPULATION | Integer | Country population        |

---

## 📤 Expected Output

A single integer representing the **total population of all cities in Asia**.

---

## 🐬 MySQL Solution

```sql

SELECT c.NAME
FROM CITY c
INNER JOIN COUNTRY co
    ON c.COUNTRYCODE = co.CODE
WHERE co.CONTINENT = 'Africa';

```

## ⭕ Oracle SQL Solution

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


SELECT c.NAME
FROM CITY c
INNER JOIN COUNTRY co
    ON c.COUNTRYCODE = co.CODE
WHERE co.CONTINENT = 'Africa';

EXIT;
```
---

## 🔍 Key Concept

- Use **JOIN** to connect `CITY` and `COUNTRY`
- Filter using:

```sql
WHERE CONTINENT = 'Asia'

Then apply:
SUM(POPULATION)
```