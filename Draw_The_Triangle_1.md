# 📍 SQL Challenge: Draw The Triangle 1

## 📝 Problem Statement

`P(R)` represents a pattern drawn by Julia in `R` rows.

The following pattern represents `P(5)`:

```text
* * * * *
* * * *
* * *
* *
*
```

## Write a query to print the pattern P(20).

# 📌 Expected Output

```

The output should contain:

* * * * * * * * * * * * * * * * * * * *
* * * * * * * * * * * * * * * * * * *
* * * * * * * * * * * * * * * * * *
* * * * * * * * * * * * * * * * * 
* * * * * * * * * * * * * * * * 
...
* *
*
```

*A total of 20 rows where each row contains stars separated by spaces.*

# 🐬 MySQL Solution

```sql
WITH RECURSIVE pattern AS (
    SELECT 20 AS n

    UNION ALL

    SELECT n - 1
    FROM pattern
    WHERE n > 1
)

SELECT REPEAT('* ', n) AS pattern_now
FROM pattern;

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

SELECT
    RPAD('* ', LEVEL * 2, '* ') AS pattern_now
FROM dual
CONNECT BY LEVEL <= 20;
exit;
```

# ✅ Query Breakdown

## 🔹 MySQL Recursive CTE

```
WITH RECURSIVE pattern AS (...)
```
Creates numbers from:

20 → 1

using recursion.

## 🔹 Recursive Step
```
SELECT n - 1
FROM pattern
WHERE n > 1
```

*Reduces the value of n by 1 until it reaches 1.*

## 🔹 REPEAT('* ', n)


```
Prints:

* * * ...

exactly n times.
```


```
Example:

REPEAT('* ', 3)
```

```
Output:

* * *
```

## 🔹 Oracle CONNECT BY

*CONNECT BY LEVEL <= 20
Generates rows from:
1 → 20*

## 🔹 RPAD('* ', LEVEL * 2, '* ')

*Builds the star pattern dynamically.*

```
Example:

LEVEL = 3
```

Output:

* * *
## 🔹 ORDER BY LEVEL DESC

Prints rows in descending order:

20 → 1

# ✅ Final Output Example

```

* * * * *
* * * *
* * *
* *
*

```