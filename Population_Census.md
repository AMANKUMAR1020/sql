# 📍 SQL Challenge: Population Census

## 📝 Problem Statement

Given the `CITY` and `COUNTRY` tables, query the sum of the populations of all cities where the `CONTINENT` is `'Asia'`.

> **Note:** `CITY.CountryCode` and `COUNTRY.Code` are matching key columns.

---

## 📊 Input Format

### 🌆 CITY Table

| Column | Type | Description |
|--------|------|-------------|
| ID | Integer | City ID |
| NAME | String | City Name |
| COUNTRYCODE | String | Country Code |
| DISTRICT | String | District Name |
| POPULATION | Integer | City Population |

---

### 🌍 COUNTRY Table

| Column | Type | Description |
|--------|------|-------------|
| CODE | String | Country Code |
| NAME | String | Country Name |
| CONTINENT | String | Continent Name |
| REGION | String | Region Name |
| POPULATION | Integer | Country Population |

---

## 📤 Expected Output

Print the total population of all cities located in the continent:

```text
Asia
```

---

## 💡 Explanation

The query:

- Joins the `CITY` and `COUNTRY` tables using matching country codes
- Filters records where the continent is `'Asia'`
- Calculates the total population using:

```text
SUM(population)
```

---

# 🐬 MySQL Solution

```sql

SELECT sum(ci.population) as population_
from city ci
inner join country co
on ci.CountryCode = co.Code
where co.CONTINENT = 'Asia';

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

SELECT sum(ci.population) as population_
from city ci
inner join country co
on ci.CountryCode = co.Code
where co.CONTINENT = 'Asia';

exit;

```

---

## ✅ Query Breakdown

### 🔹 `INNER JOIN`

Combines rows from both tables where:

```text
CITY.CountryCode = COUNTRY.Code
```

---

### 🔹 `WHERE co.CONTINENT = 'Asia'`

Filters only countries located in Asia.

---

### 🔹 `SUM(ci.population)`

Calculates the total population of all matching cities.

Example:

```text
SUM(1000 + 2000 + 3000) = 6000
```

---

## ✅ Final Output Example

```text
27028484
```

Meaning:

- Total population of all Asian cities = `27028484`

---