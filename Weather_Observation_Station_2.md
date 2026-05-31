# 📍 SQL Challenge: Weather Observation Station 2

## 📝 Problem Statement

Query the following two values from the `STATION` table:

1. The sum of all values in `LAT_N` rounded to a scale of `2` decimal places.
2. The sum of all values in `LONG_W` rounded to a scale of `2` decimal places.

---

## 📊 Input Format

### 🌍 STATION Table

| Column | Type | Description |
|--------|------|-------------|
| ID | Number | Station ID |
| CITY | String | City Name |
| STATE | String | State Name |
| LAT_N | Number | Northern Latitude |
| LONG_W | Number | Western Longitude |

> `LAT_N` represents the northern latitude  
> `LONG_W` represents the western longitude

---

## 📤 Expected Output

Your results must be in the following format:

```text
lat lon
```

Where:

- `lat` → Sum of all values in `LAT_N`
- `lon` → Sum of all values in `LONG_W`

Both values must be rounded to `2` decimal places.

---

## 💡 Explanation

The query uses:

```text
SUM()
```

to calculate the total of all latitude and longitude values.

Then:

```text
ROUND(value, 2)
```

is used to round the result to `2` decimal places.

---

# 🐬 MySQL Solution

```sql

select round(sum(LAT_N),2),round(sum(LONG_W),2)
from STATION;

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

select round(sum(LAT_N),2),round(sum(LONG_W),2)
from STATION;

exit;

```

---

## ✅ Query Breakdown

### 🔹 `SUM(LAT_N)`

Calculates the total sum of all northern latitude values.

---

### 🔹 `SUM(LONG_W)`

Calculates the total sum of all western longitude values.

---

### 🔹 `ROUND(value, 2)`

Rounds the calculated result to `2` decimal places.

Example:

```text
ROUND(123.4567, 2) = 123.46
```

---

## ✅ Final Query Output Format

```text
4283.45 4739.82
```

Meaning:

- Total latitude sum = `4283.45`
- Total longitude sum = `4739.82`

---