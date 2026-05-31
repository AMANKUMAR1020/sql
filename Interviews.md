# 📍 SQL Challenge: Interviews

## 📝 Problem Statement

Samantha interviews many candidates from different colleges using coding challenges and contests.

Write a query to print:

```text
contest_id hacker_id name total_submissions total_accepted_submissions total_views total_unique_views
```

for each contest sorted by `contest_id`.

---

# 📊 Input Format

The following tables contain interview data:

---

## 🏆 Contests Table

| Column | Type | Description |
|--------|------|-------------|
| contest_id | Integer | Contest ID |
| hacker_id | Integer | Hacker ID |
| name | String | Hacker Name |

---

## 🏫 Colleges Table

| Column | Type | Description |
|--------|------|-------------|
| college_id | Integer | College ID |
| contest_id | Integer | Contest ID used by the college |

---

## 🧩 Challenges Table

| Column | Type | Description |
|--------|------|-------------|
| challenge_id | Integer | Challenge ID |
| college_id | Integer | College ID |

---

## 👀 View_Stats Table

| Column | Type | Description |
|--------|------|-------------|
| challenge_id | Integer | Challenge ID |
| total_views | Integer | Total views |
| total_unique_views | Integer | Unique views |

---

## 📝 Submission_Stats Table

| Column | Type | Description |
|--------|------|-------------|
| challenge_id | Integer | Challenge ID |
| total_submissions | Integer | Total submissions |
| total_accepted_submissions | Integer | Accepted submissions |

---

## 📌 Conditions

Exclude contests where all of these values are `0`:

- total_submissions
- total_accepted_submissions
- total_views
- total_unique_views

Sort results by:

```text
contest_id
```

---

## 📤 Expected Output

Print:

```text
contest_id hacker_id name total_submissions total_accepted_submissions total_views total_unique_views
```

---

## 📥 Sample Output

```text
66406 17973 Rose 111 39 156 56
66556 79153 Angela 0 0 11 10
94828 80275 Frank 150 38 41 15
```

---

## 💡 Explanation

The query:

- Connects contests with colleges and challenges
- Aggregates submission statistics
- Aggregates view statistics
- Calculates totals for each contest
- Excludes contests with all totals equal to `0`

---

# 🐬 MySQL Solution

```sql
SELECT 
    c.contest_id,
    c.hacker_id,
    c.name,
    SUM(IFNULL(ss.total_submissions, 0)) AS total_submissions,
    SUM(IFNULL(ss.total_accepted_submissions, 0)) AS total_accepted_submissions,
    SUM(IFNULL(vs.total_views, 0)) AS total_views,
    SUM(IFNULL(vs.total_unique_views, 0)) AS total_unique_views
FROM Contests c
JOIN Colleges co
    ON c.contest_id = co.contest_id
JOIN Challenges ch
    ON co.college_id = ch.college_id
LEFT JOIN (
    SELECT
        challenge_id,
        SUM(total_views) AS total_views,
        SUM(total_unique_views) AS total_unique_views
    FROM View_Stats
    GROUP BY challenge_id
) vs
    ON ch.challenge_id = vs.challenge_id
LEFT JOIN (
    SELECT
        challenge_id,
        SUM(total_submissions) AS total_submissions,
        SUM(total_accepted_submissions) AS total_accepted_submissions
    FROM Submission_Stats
    GROUP BY challenge_id
) ss
    ON ch.challenge_id = ss.challenge_id
GROUP BY
    c.contest_id,
    c.hacker_id,
    c.name
HAVING
    SUM(IFNULL(ss.total_submissions, 0)) > 0
    OR SUM(IFNULL(ss.total_accepted_submissions, 0)) > 0
    OR SUM(IFNULL(vs.total_views, 0)) > 0
    OR SUM(IFNULL(vs.total_unique_views, 0)) > 0
ORDER BY c.contest_id;
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
    c.contest_id,
    c.hacker_id,
    c.name,
    SUM(NVL(ss.total_submissions, 0)) AS total_submissions,
    SUM(NVL(ss.total_accepted_submissions, 0)) AS total_accepted_submissions,
    SUM(NVL(vs.total_views, 0)) AS total_views,
    SUM(NVL(vs.total_unique_views, 0)) AS total_unique_views
FROM Contests c
JOIN Colleges co
    ON c.contest_id = co.contest_id
JOIN Challenges ch
    ON co.college_id = ch.college_id
LEFT JOIN (
    SELECT
        challenge_id,
        SUM(total_views) AS total_views,
        SUM(total_unique_views) AS total_unique_views
    FROM View_Stats
    GROUP BY challenge_id
) vs
    ON ch.challenge_id = vs.challenge_id
LEFT JOIN (
    SELECT
        challenge_id,
        SUM(total_submissions) AS total_submissions,
        SUM(total_accepted_submissions) AS total_accepted_submissions
    FROM Submission_Stats
    GROUP BY challenge_id
) ss
    ON ch.challenge_id = ss.challenge_id
GROUP BY
    c.contest_id,
    c.hacker_id,
    c.name
HAVING
    SUM(NVL(ss.total_submissions, 0)) > 0
    OR SUM(NVL(ss.total_accepted_submissions, 0)) > 0
    OR SUM(NVL(vs.total_views, 0)) > 0
    OR SUM(NVL(vs.total_unique_views, 0)) > 0
ORDER BY c.contest_id;

exit;
```

---

# ✅ Query Breakdown

## 🔹 `JOIN Colleges`

```sql
ON c.contest_id = co.contest_id
```

Links contests with colleges using the contest ID.

---

## 🔹 `JOIN Challenges`

```sql
ON co.college_id = ch.college_id
```

Gets all challenges conducted in each college.

---

## 🔹 Aggregating View Statistics

```sql
SUM(total_views)
SUM(total_unique_views)
```

Calculates total views and unique views for each challenge.

---

## 🔹 Aggregating Submission Statistics

```sql
SUM(total_submissions)
SUM(total_accepted_submissions)
```

Calculates total submissions and accepted submissions.

---

## 🔹 `LEFT JOIN`

Ensures contests are included even if some statistics are missing.

---

## 🔹 `NVL()` / `IFNULL()`

Replaces `NULL` values with `0`.

Example:

```sql
NVL(value, 0)
```

---

## 🔹 `HAVING`

Filters out contests where all totals are `0`.

---

## 🔹 `ORDER BY c.contest_id`

Sorts the final output by contest ID in ascending order.

---

## ✅ Final Output Example

```text
66406 17973 Rose 111 39 156 56
66556 79153 Angela 0 0 11 10
94828 80275 Frank 150 38 41 15
```

Meaning:

Contest `66406` had:

- `111` submissions
- `39` accepted submissions
- `156` views
- `56` unique views

---



