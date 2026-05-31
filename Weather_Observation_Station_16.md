# 📍 SQL Challenge: Weather Observation Station 16

## 📝 Problem Statement

Query the smallest Northern Latitude (`LAT_N`) from the `STATION` table that is greater than `38.7780`.

Round your answer to `4` decimal places.

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

Print the smallest `LAT_N` value that satisfies:

```text
LAT_N > 38.7780
```

The result must be displayed up to `4` decimal places.

---

## 💡 Explanation

The query:

- Filters latitude values greater than `38.7780`
- Finds the minimum latitude value using:

```text
MIN(LAT_N)
```

- Rounds the result to `4` decimal places using:

```text
ROUND(value, 4)
```

---

# 🐬 MySQL Solution

```sql

select round(min(LAT_N),4)
from STATION
where LAT_N > 38.7780;

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

select round(min(LAT_N),4)
from STATION
where LAT_N > 38.7780;

exit;

```

---

## ✅ Query Breakdown

### 🔹 `WHERE LAT_N > 38.7780`

Filters latitude values greater than `38.7780`.

---

### 🔹 `MIN(LAT_N)`

Finds the smallest latitude value from the filtered records.

---

### 🔹 `ROUND(MIN(LAT_N),4)`

Rounds the final result to `4` decimal places.

Example:

```text
ROUND(38.852613, 4) = 38.8526
```

---

## ✅ Final Output Example

```text
38.8526
```

Meaning:

- Smallest latitude value greater than `38.7780` = `38.8526`

---