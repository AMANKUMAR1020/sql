# 📍 SQL Challenge: Weather Observation Station 15

## 📝 Problem Statement

Query the greatest value of the Northern Latitudes (`LAT_N`) from the `STATION` table that is less than `137.2345`.

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

Print the greatest `LAT_N` value that satisfies:

```text
LAT_N < 137.2345
```

The result must be displayed up to `4` decimal places.

---

## 💡 Explanation

The query:

- Filters latitude values less than `137.2345`
- Finds the maximum latitude value using:

```text
MAX(LAT_N)
```

- Rounds the result to `4` decimal places using:

```text
ROUND(value, 4)
```

---

# 🐬 MySQL Solution

```sql

select round(max(LONG_W),4)
from STATION
where LAT_N = (select max(LAT_N) 
                from station
                where LAT_N < 137.2345);

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

select round(max(LONG_W),4)
from STATION
where LAT_N = (select max(LAT_N) 
                from station
                where LAT_N < 137.2345);
exit;

```

---

## ✅ Query Breakdown

### 🔹 `WHERE LAT_N < 137.2345`

Filters latitude values less than `137.2345`.

---

### 🔹 `MAX(LAT_N)`

Finds the greatest latitude value from the filtered records.

---

### 🔹 `ROUND(MAX(LAT_N),4)`

Rounds the final result to `4` decimal places.

Example:

```text
ROUND(123.456789, 4) = 123.4568
```

---

## ✅ Final Output Example

```text
137.0193
```

Meaning:

- Greatest latitude value below `137.2345` = `137.0193`

---




