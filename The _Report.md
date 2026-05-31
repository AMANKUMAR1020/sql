# 📍 SQL Challenge: The Report

## 📝 Problem Statement

You are given two tables: `Students` and `Grades`.

### 👨‍🎓 Students Table

| Column | Type | Description |
|--------|------|-------------|
| ID | Integer | Student ID |
| Name | String | Student Name |
| Marks | Integer | Student Marks |

---

### 📊 Grades Table

| Column | Type | Description |
|--------|------|-------------|
| Grade | Integer | Grade Number |
| Min_Mark | Integer | Minimum Marks |
| Max_Mark | Integer | Maximum Marks |

---

Ketty gives Eve a task to generate a report containing three columns:

```text
Name Grade Marks
```

### 📌 Conditions

- Students receiving grades **8 to 10** should display their actual names.
- Students receiving grades **lower than 8** should display:

```text
NULL
```

instead of their names.

### 📌 Sorting Rules

1. Sort by `Grade` in descending order.
2. For grades `8-10`:
   - Sort students alphabetically by `Name`.
3. For grades `1-7`:
   - Sort students by `Marks` in ascending order.

Write a query to generate the required report.

---

## 📥 Sample Input

### Students

| ID | Name | Marks |
|----|------|-------|
| 1 | Julia | 88 |
| 2 | Samantha | 68 |
| 3 | Maria | 99 |
| 4 | Scarlet | 78 |
| 5 | Ashley | 63 |
| 6 | Jane | 81 |

---

### Grades

| Grade | Min_Mark | Max_Mark |
|------|----------|----------|
| 1 | 0 | 9 |
| 2 | 10 | 19 |
| 3 | 20 | 29 |
| 4 | 30 | 39 |
| 5 | 40 | 49 |
| 6 | 50 | 59 |
| 7 | 60 | 69 |
| 8 | 70 | 79 |
| 9 | 80 | 89 |
| 10 | 90 | 100 |

---

## 📤 Expected Output

```text
Maria 10 99
Jane 9 81
Julia 9 88
Scarlet 8 78
NULL 7 63
NULL 7 68
```

---

## 💡 Explanation

Students with grades:

- `8 - 10` → display actual names
- `1 - 7` → display `NULL`

The query:

- Matches marks with grade ranges
- Uses conditional formatting with `CASE`
- Applies different sorting conditions based on grade

---

# 🐬 MySQL Solution

```sql

SELECT
    CASE 
        WHEN g.Grade < 8 THEN 'NULL'
        ELSE s.Name
    END AS Name,
    g.Grade,
    s.Marks
FROM Students s
JOIN Grades g
    ON s.Marks BETWEEN g.Min_Mark AND g.Max_Mark
ORDER BY 
    g.Grade DESC,
    CASE 
        WHEN g.Grade >= 8 THEN s.Name
        ELSE NULL
    END,
    CASE 
        WHEN g.Grade < 8 THEN s.Marks
        ELSE NULL
    END;

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

SELECT
    CASE 
        WHEN g.Grade < 8 THEN 'NULL'
        ELSE s.Name
    END AS Name,
    g.Grade,
    s.Marks
FROM Students s
JOIN Grades g
    ON s.Marks BETWEEN g.Min_Mark AND g.Max_Mark
ORDER BY 
    g.Grade DESC,
    CASE 
        WHEN g.Grade >= 8 THEN s.Name
        ELSE NULL
    END,
    CASE 
        WHEN g.Grade < 8 THEN s.Marks
        ELSE NULL
    END;

exit;

```

---

## ✅ Query Breakdown

### 🔹 `JOIN Grades g ON s.Marks BETWEEN g.Min_Mark AND g.Max_Mark`

Matches each student's marks with the appropriate grade range.

---

### 🔹 `CASE WHEN g.Grade < 8`

Displays:

```text
NULL
```

for students with grades lower than `8`.

---

### 🔹 `ORDER BY g.Grade DESC`

Sorts all students by grade in descending order.

---

### 🔹 Sorting for Grades `8-10`

```sql
CASE 
    WHEN g.Grade >= 8 THEN s.Name
END
```

Sorts higher-grade students alphabetically by name.

---

### 🔹 Sorting for Grades `1-7`

```sql
CASE 
    WHEN g.Grade < 8 THEN s.Marks
END
```

Sorts lower-grade students by marks in ascending order.

---

## ✅ Final Output Example

```text
Maria 10 99
Jane 9 81
Julia 9 88
Scarlet 8 78
NULL 7 63
NULL 7 68
```

Meaning:

- Students with grade `8+` show names
- Students with grade `< 8` display `NULL`

---