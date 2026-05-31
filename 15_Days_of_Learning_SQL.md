# 📍 SQL Challenge: 15 Days of Learning SQL

## 📝 Problem Statement

Julia conducted a **15 Days of Learning SQL** contest from:

```text
2016-03-01 → 2016-03-15
```

Write a query to print:

```text
submission_date total_unique_hackers hacker_id name
```

for each day of the contest.

---

# 📊 Input Format

The following tables contain contest data:

---

## 👨‍💻 Hackers Table

| Column | Type | Description |
|--------|------|-------------|
| hacker_id | Integer | Hacker ID |
| name | String | Hacker Name |

---

## 📝 Submissions Table

| Column | Type | Description |
|--------|------|-------------|
| submission_date | Date | Submission Date |
| submission_id | Integer | Submission ID |
| hacker_id | Integer | Hacker ID |
| score | Integer | Submission Score |

---

## 📌 Requirements

For each contest day:

### 1️⃣ Count Unique Consistent Hackers

Count hackers who made at least one submission on:

- Day 1
- Day 2
- ...
- Current day

continuously without missing any day.

---

### 2️⃣ Find Top Hacker of the Day

Find the hacker who made the maximum number of submissions on that day.

If multiple hackers have the same maximum submissions:

- Choose the hacker with the smaller `hacker_id`.

---

## 📤 Expected Output

Print:

```text
submission_date total_unique_hackers hacker_id name
```

ordered by:

```text
submission_date
```

---

## 📥 Sample Output

```text
2016-03-01 4 20703 Angela
2016-03-02 2 79722 Michael
2016-03-03 2 20703 Angela
2016-03-04 2 20703 Angela
2016-03-05 1 36396 Frank
2016-03-06 1 20703 Angela
```

---

## 💡 Explanation

### 📌 March 01, 2016

Hackers who submitted:

```text
20703, 36396, 53473, 79722
```

All submitted on Day 1, so:

```text
total_unique_hackers = 4
```

Each made one submission, therefore the smallest hacker_id is chosen:

```text
20703 Angela
```

---

### 📌 March 02, 2016

Only hackers who submitted on both:

```text
March 01 and March 02
```

are counted.

Thus:

```text
total_unique_hackers = 2
```

Michael made the highest submissions that day.

---

# 🐬 MySQL Solution

```sql
WITH daily_submissions AS (
    SELECT
        submission_date,
        hacker_id,
        COUNT(*) AS submissions_count
    FROM Submissions
    GROUP BY submission_date, hacker_id
),

consistent_hackers AS (
    SELECT
        ds1.submission_date,
        ds1.hacker_id
    FROM daily_submissions ds1
    WHERE (
        SELECT COUNT(DISTINCT ds2.submission_date)
        FROM daily_submissions ds2
        WHERE ds2.hacker_id = ds1.hacker_id
          AND ds2.submission_date <= ds1.submission_date
    ) = DATEDIFF(ds1.submission_date, '2016-03-01') + 1
),

daily_top_hacker AS (
    SELECT
        submission_date,
        hacker_id,
        submissions_count,
        ROW_NUMBER() OVER (
            PARTITION BY submission_date
            ORDER BY submissions_count DESC, hacker_id
        ) AS rn
    FROM daily_submissions
)

SELECT
    ch.submission_date,
    COUNT(DISTINCT ch.hacker_id) AS total_unique_hackers,
    dth.hacker_id,
    h.name
FROM consistent_hackers ch
JOIN daily_top_hacker dth
    ON ch.submission_date = dth.submission_date
   AND dth.rn = 1
JOIN Hackers h
    ON dth.hacker_id = h.hacker_id
GROUP BY
    ch.submission_date,
    dth.hacker_id,
    h.name
ORDER BY ch.submission_date;
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

WITH daily_submissions AS (
    SELECT
        submission_date,
        hacker_id,
        COUNT(*) AS submissions_count
    FROM Submissions
    GROUP BY submission_date, hacker_id
),

consistent_hackers AS (
    SELECT
        ds1.submission_date,
        ds1.hacker_id
    FROM daily_submissions ds1
    WHERE (
        SELECT COUNT(DISTINCT ds2.submission_date)
        FROM daily_submissions ds2
        WHERE ds2.hacker_id = ds1.hacker_id
          AND ds2.submission_date <= ds1.submission_date
    ) = ds1.submission_date - DATE '2016-03-01' + 1
),

daily_top_hacker AS (
    SELECT
        submission_date,
        hacker_id,
        submissions_count,
        ROW_NUMBER() OVER (
            PARTITION BY submission_date
            ORDER BY submissions_count DESC, hacker_id
        ) AS rn
    FROM daily_submissions
)

SELECT
    ch.submission_date,
    COUNT(DISTINCT ch.hacker_id) AS total_unique_hackers,
    dth.hacker_id,
    h.name
FROM consistent_hackers ch
JOIN daily_top_hacker dth
    ON ch.submission_date = dth.submission_date
   AND dth.rn = 1
JOIN Hackers h
    ON dth.hacker_id = h.hacker_id
GROUP BY
    ch.submission_date,
    dth.hacker_id,
    h.name
ORDER BY ch.submission_date;

exit;
```

---

# ✅ Query Breakdown

## 🔹 `daily_submissions`

```sql
COUNT(*)
```

Calculates how many submissions each hacker made per day.

---

## 🔹 `consistent_hackers`

Checks whether a hacker submitted every single day from:

```text
2016-03-01 → current submission_date
```

Logic:

```sql
COUNT(DISTINCT submission_date)
=
number_of_days_since_start
```

---

## 🔹 `daily_top_hacker`

Uses:

```sql
ROW_NUMBER()
```

to rank hackers daily based on:

1. Highest submission count
2. Lowest hacker_id (tie breaker)

---

## 🔹 `ROW_NUMBER() OVER`

```sql
PARTITION BY submission_date
```

Creates rankings separately for each contest day.

---

## 🔹 `ORDER BY submissions_count DESC`

Selects the hacker with maximum submissions for that day.

---

## 🔹 `COUNT(DISTINCT ch.hacker_id)`

Counts hackers who consistently submitted every day up to that date.

---

## 🔹 Final Ordering

```sql
ORDER BY ch.submission_date
```

Displays results chronologically.

---

## ✅ Final Output Example

```text
2016-03-01 4 20703 Angela
2016-03-02 2 79722 Michael
2016-03-03 2 20703 Angela
```

Meaning:

- The second column shows consistent daily participants.
- The last two columns show the top submitter for that day.

---