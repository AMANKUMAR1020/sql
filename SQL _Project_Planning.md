# 📍 SQL Challenge: SQL Project Planning

## 📝 Problem Statement

You are given a table named `Projects` containing the following columns:

| Column | Type | Description |
|--------|------|-------------|
| Task_ID | Integer | Task ID |
| Start_Date | Date | Task Start Date |
| End_Date | Date | Task End Date |

It is guaranteed that:

```text
End_Date - Start_Date = 1 day
```

for every task.

If the `End_Date` values of tasks are consecutive, then those tasks belong to the same project.

Write a query to print:

```text
project_start_date project_end_date
```

for all projects.

---

## 📌 Sorting Rules

1. Sort by the number of days taken to complete the project in ascending order.
2. If multiple projects have the same duration:
   - Sort by the project start date.

---

## 📥 Sample Input

| Task_ID | Start_Date | End_Date |
|---------|------------|----------|
| 1 | 2015-10-01 | 2015-10-02 |
| 2 | 2015-10-02 | 2015-10-03 |
| 3 | 2015-10-03 | 2015-10-04 |
| 4 | 2015-10-13 | 2015-10-14 |
| 5 | 2015-10-14 | 2015-10-15 |
| 6 | 2015-10-28 | 2015-10-29 |
| 7 | 2015-10-30 | 2015-10-31 |

---

## 📤 Expected Output

```text
2015-10-28 2015-10-29
2015-10-30 2015-10-31
2015-10-13 2015-10-15
2015-10-01 2015-10-04
```

---

## 💡 Explanation

The tasks form the following projects:

### 📌 Project 1

Tasks:

```text
1 → 2 → 3
```

Dates:

```text
2015-10-01 → 2015-10-04
```

Duration:

```text
3 days
```

---

### 📌 Project 2

Tasks:

```text
4 → 5
```

Dates:

```text
2015-10-13 → 2015-10-15
```

Duration:

```text
2 days
```

---

### 📌 Project 3

Task:

```text
6
```

Dates:

```text
2015-10-28 → 2015-10-29
```

Duration:

```text
1 day
```

---

### 📌 Project 4

Task:

```text
7
```

Dates:

```text
2015-10-30 → 2015-10-31
```

Duration:

```text
1 day
```

---

# 🐬 MySQL Solution

```sql

WITH numbered AS (
    SELECT 
        Start_Date,
        End_Date,
        ROW_NUMBER() OVER (ORDER BY Start_Date) AS rn
    FROM Projects
),
grouped AS (
    SELECT 
        Start_Date,
        End_Date,
        DATE_SUB(Start_Date, INTERVAL rn DAY) AS grp
    FROM numbered
)
SELECT 
    MIN(Start_Date) AS project_start,
    MAX(End_Date) AS project_end
FROM grouped
GROUP BY grp
ORDER BY 
    DATEDIFF(MAX(End_Date), MIN(Start_Date)) ASC,
    MIN(Start_Date) ASC;

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

WITH numbered AS (
    SELECT 
        Start_Date,
        End_Date,
        ROW_NUMBER() OVER (ORDER BY Start_Date) rn
    FROM Projects
),
grouped AS (
    SELECT 
        Start_Date,
        End_Date,
        Start_Date - rn grp
    FROM numbered
)
SELECT 
    MIN(Start_Date) AS project_start,
    MAX(End_Date) AS project_end
FROM grouped
GROUP BY grp
ORDER BY 
    MAX(End_Date) - MIN(Start_Date),
    MIN(Start_Date);

exit;

```

---

## ✅ Query Breakdown

### 🔹 `ROW_NUMBER() OVER (ORDER BY Start_Date)`

Assigns a sequential row number to each task ordered by start date.

---

### 🔹 Grouping Consecutive Dates

In MySQL:

```sql
DATE_SUB(Start_Date, INTERVAL rn DAY)
```

In Oracle:

```sql
Start_Date - rn
```

This creates the same grouping value for consecutive dates.

---

### 🔹 `GROUP BY grp`

Groups consecutive tasks into a single project.

---

### 🔹 `MIN(Start_Date)`

Finds the start date of the project.

---

### 🔹 `MAX(End_Date)`

Finds the end date of the project.

---

### 🔹 `DATEDIFF(MAX(End_Date), MIN(Start_Date))`

Calculates the project duration in days.

---

### 🔹 `ORDER BY`

Projects are sorted by:

1. Shortest duration first
2. Earliest start date

---

## ✅ Final Output Example

```text
2015-10-28 2015-10-29
2015-10-30 2015-10-31
2015-10-13 2015-10-15
2015-10-01 2015-10-04
```

Meaning:

- Projects with shorter completion times appear first.
- If durations are equal, earlier projects appear first.

---