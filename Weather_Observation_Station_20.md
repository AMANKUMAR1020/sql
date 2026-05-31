# 📍 SQL Challenge: Weather Observation Station 20

## 📝 Problem Statement

A **median** is defined as a number separating the higher half of a data set from the lower half.

Query the median of the Northern Latitudes (`LAT_N`) from the `STATION` table and round your answer to `4` decimal places.

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

Print the median value of `LAT_N` rounded to `4` decimal places.

---

## 💡 Explanation

### Median Formula

:contentReference[oaicite:0]{index=0}

The query:

- Sorts all latitude values in ascending order
- Finds the middle value
- Rounds the result to `4` decimal places

---

# 🐬 MySQL Solution

```sql

SELECT ROUND(AVG(LAT_N), 4)
FROM (
    SELECT LAT_N
    FROM (
        SELECT LAT_N,
               ROW_NUMBER() OVER (ORDER BY LAT_N) AS row_num,
               COUNT(*) OVER () AS total_rows
        FROM STATION
    ) AS ranked
    WHERE row_num IN (
        FLOOR((total_rows + 1) / 2),
        FLOOR((total_rows + 2) / 2)
    )
) AS median_table;

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

SELECT ROUND(MEDIAN(LAT_N), 4)
FROM STATION;

exit;

```

---

## ✅ Query Breakdown

### 🔹 `ROW_NUMBER() OVER (ORDER BY LAT_N)`

Assigns row numbers after sorting latitude values in ascending order.

---

### 🔹 `COUNT(*) OVER ()`

Calculates the total number of rows.

---

### 🔹 `FLOOR((total_rows + 1) / 2)`

Finds the middle row position.

---

### 🔹 `AVG(LAT_N)`

Handles both odd and even row counts:

- Odd rows → returns the middle value
- Even rows → returns the average of two middle values

---

### 🔹 `ROUND(value, 4)`

Rounds the median value to `4` decimal places.

Example:

```text
ROUND(45.678912, 4) = 45.6789
```

---

## ✅ Final Output Example

```text
39.1234
```

Meaning:

- Median Northern Latitude = `39.1234`

---