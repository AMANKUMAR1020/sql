# 📍 SQL Challenge: Weather Observation Station 13

## 📝 Problem Statement

Query the sum of Northern Latitudes (`LAT_N`) from the `STATION` table having values greater than `38.7880` and less than `137.2345`.

Truncate your answer to `4` decimal places.

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

Print the sum of all `LAT_N` values between:

```text
38.7880 < LAT_N < 137.2345
```

The result must be displayed up to `4` decimal places.

---

## 💡 Explanation

The query:

- Filters latitude values using the `WHERE` clause
- Calculates the total using:

```text
SUM(LAT_N)
```

- Rounds the result to `4` decimal places using:

```text
ROUND(value, 4)
```

---

# 🐬 MySQL Solution

```sql

select round(sum(LAT_N),4)
from STATION
where LAT_N > 38.7880 
AND LAT_N < 137.2345;

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

select round(sum(LAT_N),4)
from STATION
where LAT_N > 38.7880 
AND LAT_N < 137.2345;

exit;

```

---

## ✅ Query Breakdown

### 🔹 `WHERE LAT_N > 38.7880`

Filters latitude values greater than `38.7880`.

---

### 🔹 `AND LAT_N < 137.2345`

Filters latitude values less than `137.2345`.

---

### 🔹 `SUM(LAT_N)`

Calculates the total sum of the filtered latitude values.

---

### 🔹 `ROUND(sum(LAT_N),4)`

Rounds the final result to `4` decimal places.

Example:

```text
ROUND(123.456789, 4) = 123.4568
```

---

## ✅ Final Output Example

```text
36354.8135
```

Meaning:

- Total latitude sum between the given range = `36354.8135`

---