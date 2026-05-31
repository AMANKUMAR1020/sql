# 📍 SQL Challenge: Weather Observation Station 18

## 📝 Problem Statement

Consider the following two points on a 2D plane:

- **P1(a, b)**
- **P2(c, d)**

Where:

- `a` = minimum value of Northern Latitude (`LAT_N`) in `STATION`
- `b` = minimum value of Western Longitude (`LONG_W`) in `STATION`
- `c` = maximum value of Northern Latitude (`LAT_N`) in `STATION`
- `d` = maximum value of Western Longitude (`LONG_W`) in `STATION`

Query the **Manhattan Distance** between points `P1` and `P2`.

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

Print the Manhattan Distance between points:

```text
P1(min(LAT_N), min(LONG_W))
P2(max(LAT_N), max(LONG_W))
```

The result must be displayed up to `4` decimal places.

---

## 💡 Explanation

### Manhattan Distance Formula

:contentReference[oaicite:0]{index=0}

For this problem:

```text
|max(LAT_N) - min(LAT_N)| + |max(LONG_W) - min(LONG_W)|
```

The query:

- Finds maximum and minimum latitude values
- Finds maximum and minimum longitude values
- Computes the Manhattan Distance
- Rounds the final result to `4` decimal places

---

# 🐬 MySQL Solution

```sql

select round(
            abs(max(LONG_W) - min(LONG_W)) + 
            abs(max(LAT_N) - min(LAT_N)),
            4
       )
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

select round(
            abs(max(LONG_W) - min(LONG_W)) + 
            abs(max(LAT_N) - min(LAT_N)),
            4
       )
from STATION;

exit;

```

---

## ✅ Query Breakdown

### 🔹 `MAX(LAT_N)`

Finds the maximum northern latitude.

---

### 🔹 `MIN(LAT_N)`

Finds the minimum northern latitude.

---

### 🔹 `MAX(LONG_W)`

Finds the maximum western longitude.

---

### 🔹 `MIN(LONG_W)`

Finds the minimum western longitude.

---

### 🔹 `ABS(value)`

Returns the absolute difference between coordinates.

Example:

```text
ABS(10 - 20) = 10
```

---

### 🔹 `ROUND(value, 4)`

Rounds the final Manhattan Distance to `4` decimal places.

Example:

```text
ROUND(25.678912, 4) = 25.6789
```

---

## ✅ Final Output Example

```text
259.6859
```

Meaning:

- Manhattan Distance between the two points = `259.6859`

---