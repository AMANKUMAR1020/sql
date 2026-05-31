# 📍 SQL Challenge: Print Prime Numbers

## 📝 Problem Statement

Write a query to print all prime numbers less than or equal to `1000`.

Print the result on a single line using the ampersand (`&`) character as the separator instead of spaces.

Example:

```text
2&3&5&7
```

# 📌 Expected Output
`2&3&5&7&11&13&17&19&23&29...`

All prime numbers less than or equal to 1000 should appear in a single line separated by &.

# 🐬 MySQL Solution
```sql
WITH RECURSIVE base AS (
    SELECT 2 AS num

    UNION ALL

    SELECT num + 1
    FROM base
    WHERE num < 1000
),

filters AS (
    SELECT 2 AS filter

    UNION ALL

    SELECT filter + 1
    FROM filters
    WHERE filter < FLOOR(SQRT(1000))
)

SELECT GROUP_CONCAT(num ORDER BY num SEPARATOR '&')
FROM (
    SELECT
        b.num,
        SUM(
            b.num % f.filter = 0
            AND b.num != f.filter
        ) AS modulo
    FROM base b
    CROSS JOIN filters f
    GROUP BY b.num
    HAVING modulo = 0
) AS result;

```

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

WITH numbers AS (
    SELECT LEVEL + 1 AS num
    FROM dual
    CONNECT BY LEVEL <= 999
)

SELECT LISTAGG(num, '&')
       WITHIN GROUP (ORDER BY num)
FROM (
    SELECT n1.num
    FROM numbers n1
    WHERE NOT EXISTS (
        SELECT 1
        FROM numbers n2
        WHERE n2.num <= SQRT(n1.num)
          AND n2.num > 1
          AND n2.num < n1.num
          AND MOD(n1.num, n2.num) = 0
    )
);

EXIT;
```

# ✅ Query Breakdown

## 🔹 Generate Numbers

```
MySQL WITH RECURSIVE base AS (...)

Creates numbers from:

2 → 1000
```

using recursion.


*Oracle
CONNECT BY LEVEL <= 999
Generates numbers from:
2 → 1000*

using hierarchical queries.

## 🔹 Prime Number Logic

A number is prime if:

It has no divisors other than 1 and itself

## 🔹 MySQL Filtering
`b.num % f.filter = 0`

Checks whether the current number is divisible by another number.

If divisible:

Not Prime

If no divisors exist:

Prime

## 🔹 Oracle NOT EXISTS
NOT EXISTS (...)

Ensures there is no smaller number that divides the current number evenly.

## 🔹 String Aggregation

`MySQL
GROUP_CONCAT(... SEPARATOR '&')`

Combines all prime numbers into a single line separated by &.

`Oracle
LISTAGG(num, '&')
WITHIN GROUP (ORDER BY num)`

Concatenates prime numbers into one row.

--- 

# ✅ Final Output Example
`2&3&5&7&11&13&17&19&23&29`

---

Meaning:

Only prime numbers are printed.
All numbers are separated using &.
The result appears on a single line.

---

