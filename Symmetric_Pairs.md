# 📍 SQL Challenge: Symmetric Pairs

## 📝 Problem Statement

You are given a table named `Functions` containing two columns:

| Column | Type | Description |
|--------|------|-------------|
| X | Integer | X coordinate |
| Y | Integer | Y coordinate |

---

Two pairs:

```text
(X1, Y1) and (X2, Y2)
```

are considered symmetric if:

```text
X1 = Y2
X2 = Y1
```

Write a query to output all symmetric pairs in ascending order by the value of `X`.

---

## 📌 Conditions

- Print only pairs where:

```text
X <= Y
```

- Order the result by `X` in ascending order.

---

## 📥 Sample Input

| X | Y |
|---|---|
| 20 | 20 |
| 20 | 20 |
| 20 | 21 |
| 21 | 20 |
| 22 | 23 |
| 23 | 22 |

---

## 📤 Expected Output

```text
20 20
20 21
22 23
```

---

## 💡 Explanation

### 📌 Symmetric Pair Logic

A pair is symmetric when:

```text
(X, Y) exists
and
(Y, X) also exists
```

Examples:

| Pair 1 | Pair 2 | Symmetric? |
|--------|--------|-------------|
| (20,21) | (21,20) | ✅ Yes |
| (22,23) | (23,22) | ✅ Yes |
| (10,15) | (15,20) | ❌ No |

---

### 📌 Special Case

For pairs like:

```text
(20,20)
```

the pair is symmetric with itself.

To include such values, the pair must appear more than once in the table.

---

# 🐬 MySQL Solution

```sql

SELECT f1.X, f1.Y
FROM Functions f1
JOIN Functions f2
    ON f1.X = f2.Y 
   AND f1.Y = f2.X
WHERE f1.X <= f1.Y
GROUP BY f1.X, f1.Y
HAVING COUNT(*) > 1 
    OR f1.X <> f1.Y
ORDER BY f1.X;

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

SELECT f1.X, f1.Y
FROM Functions f1
JOIN Functions f2
    ON f1.X = f2.Y
   AND f1.Y = f2.X
WHERE f1.X <= f1.Y
GROUP BY f1.X, f1.Y
HAVING COUNT(*) > 1
    OR f1.X <> f1.Y
ORDER BY f1.X;

exit;

```

---

## ✅ Query Breakdown

### 🔹 Self Join

```sql
JOIN Functions f2
ON f1.X = f2.Y
AND f1.Y = f2.X
```

Matches each pair with its symmetric counterpart.

---

### 🔹 `WHERE f1.X <= f1.Y`

Ensures only one version of the symmetric pair is displayed.

Example:

Instead of printing both:

```text
20 21
21 20
```

only:

```text
20 21
```

is shown.

---

### 🔹 `GROUP BY f1.X, f1.Y`

Groups identical pairs together.

---

### 🔹 `HAVING COUNT(*) > 1`

Handles cases like:

```text
20 20
```

which must appear multiple times to be considered symmetric.

---

### 🔹 `OR f1.X <> f1.Y`

Allows normal symmetric pairs such as:

```text
20 21
21 20
```

---

### 🔹 `ORDER BY f1.X`

Sorts the output by `X` in ascending order.

---

## ✅ Final Output Example

```text
20 20
20 21
22 23
```

Meaning:

- `(20,20)` appears multiple times and is symmetric.
- `(20,21)` and `(21,20)` form a symmetric pair.
- `(22,23)` and `(23,22)` form another symmetric pair.

---