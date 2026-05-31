# 📍 SQL Challenge: Weather Observation Station 19

## 📝 Problem Statement

Consider two points on a 2D plane:

- **P1(a, b)**
- **P2(c, d)**

Where:

- `a` and `c` are the respective minimum and maximum values of Northern Latitude (`LAT_N`)
- `b` and `d` are the respective minimum and maximum values of Western Longitude (`LONG_W`)

from the `STATION` table.

Query the **Euclidean Distance** between points `P1` and `P2` and format your answer to display `4` decimal digits.

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

Print the Euclidean Distance between:

```text
P1(min(LAT_N), min(LONG_W))
P2(max(LAT_N), max(LONG_W))
```

The result must be displayed up to `4` decimal places.

---

## 💡 Explanation

### Euclidean Distance Formula

:contentReference[oaicite:0]{index=0}

For this problem:

```text
√((max(LAT_N) - min(LAT_N))² + (max(LONG_W) - min(LONG_W))²)
```

The query:

- Finds minimum and maximum latitude values
- Finds minimum and maximum longitude values
- Applies the Euclidean Distance formula
- Rounds the result to `4` decimal places

---

# 🐬 MySQL Solution

```sql

select round(
        sqrt(
            pow(max(LAT_N) - min(LAT_N),2) +
            pow(max(LONG_W) - min(LONG_W),2)
        ),
         4)
from station;

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
        sqrt(
            power(max(LAT_N) - min(LAT_N),2) +
            power(max(LONG_W) - min(LONG_W),2)
        ),
         4)
from station;

exit;

```

---

## ✅ Query Breakdown

### 🔹 `MAX(LAT_N)` and `MIN(LAT_N)`

Find the maximum and minimum northern latitude values.

---

### 🔹 `MAX(LONG_W)` and `MIN(LONG_W)`

Find the maximum and minimum western longitude values.

---

### 🔹 `POW(value, 2)` / `POWER(value, 2)`

Calculates the square of a number.

Example:

```text
POWER(5,2) = 25
```

---

### 🔹 `SQRT(value)`

Calculates the square root.

Example:

```text
SQRT(25) = 5
```

---

### 🔹 `ROUND(value, 4)`

Rounds the final Euclidean Distance to `4` decimal places.

Example:

```text
ROUND(25.678912, 4) = 25.6789
```

---

## ✅ Final Output Example

```text
184.1616
```

Meaning:

- Euclidean Distance between the two points = `184.1616`

---