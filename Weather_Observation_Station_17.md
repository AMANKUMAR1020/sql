# 📍 SQL Challenge: Weather Observation Station 17

## 📝 Problem Statement

Query the Western Longitude (`LONG_W`) where the smallest Northern Latitude (`LAT_N`) in the `STATION` table is greater than `38.7780`.

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

Print the `LONG_W` value corresponding to the smallest `LAT_N` that satisfies:

```text
LAT_N > 38.7780
```

The result must be displayed up to `4` decimal places.

---

## 💡 Explanation

The query:

- Finds the smallest latitude value greater than `38.7780`
- Retrieves the corresponding western longitude
- Rounds the result to `4` decimal places

The smallest latitude is calculated using:

```text
MIN(LAT_N)
```

Then the corresponding longitude is selected.

---

# 🐬 MySQL Solution

```sql

select round(min(LONG_W),4)
from STATION
where LAT_N = (
    select min(LAT_N)
    from STATION
    where LAT_N > 38.7780
);

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

select round(min(LONG_W),4)
from STATION
where LAT_N = (
    select min(LAT_N)
    from STATION
    where LAT_N > 38.7780
);

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

### 🔹 `WHERE LAT_N = (...)`

Selects the row having the smallest qualifying latitude.

---

### 🔹 `MIN(LONG_W)`

Retrieves the western longitude corresponding to that latitude.

---

### 🔹 `ROUND(MIN(LONG_W),4)`

Rounds the final longitude value to `4` decimal places.

Example:

```text
ROUND(77.123456, 4) = 77.1235
```

---

## ✅ Final Output Example

```text
77.1235
```

Meaning:

- Western Longitude corresponding to the smallest latitude greater than `38.7780` = `77.1235`

---