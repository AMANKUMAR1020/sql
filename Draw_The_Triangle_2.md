# 📍 SQL Challenge: Draw The Triangle 2

## 📝 Problem Statement

`P(R)` represents a pattern drawn by Julia in `R` rows.

The following pattern represents `P(5)`:

```text

* 
* * 
* * * 
* * * * 
* * * * *

```


## Write a query to print the pattern P(20).

# 📌 Expected Output

```

The output should contain:

* 
* * 
* * * 
* * * * 
* * * * *
* * * * * *
* * * * * * *
* * * * * * * *
* * * * * * * * *
* * * * * * * * * *
......
* * * * * * * * * * * * * * * * * * * *
* * * * * * * * * * * * * * * * * * * * *

```

*A total of 20 rows where each row contains stars separated by spaces.*

# 🐬 MySQL Solution

```sql

with recursive pattern as (
    select 1 as n
    union all
    select n + 1
    from pattern
    where n < 20
)
select repeat('* ',n) as pattern_row
from pattern;

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
select n + 1
from pattern
where n < 20

```

*Increse the value of n by 1 until it reaches 20.*

## 🔹 REPEAT('* ', n)


```
Prints:

* * * ...

exactly 1 times.
```


