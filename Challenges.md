# 📍 SQL Challenge: Challenges

## 📝 Problem Statement

Julia asked her students to create some coding challenges.

Write a query to print:

```text
hacker_id name total_challenges
```

for each student who created challenges.

---

## 📊 Input Format

The following tables contain challenge data:

---

### 👨‍💻 Hackers Table

| Column | Type | Description |
|--------|------|-------------|
| hacker_id | Integer | Hacker ID |
| name | String | Hacker Name |

---

### 🧩 Challenges Table

| Column | Type | Description |
|--------|------|-------------|
| challenge_id | Integer | Challenge ID |
| hacker_id | Integer | Hacker ID of challenge creator |

---

## 📌 Sorting Rules

1. Sort results by the total number of challenges created in descending order.
2. If more than one student created the same number of challenges:
   - Sort by `hacker_id`.
3. If multiple students created the same number of challenges **and** that count is less than the maximum number of challenges created:
   - Exclude those students from the result.

---

## 📤 Expected Output

Print:

```text
hacker_id name total_challenges
```

---

## 📥 Sample Output

```text
21283 Angela 6
88255 Patrick 5
96196 Lisa 1
```

---

## 💡 Explanation

The query:

- Counts how many challenges each hacker created
- Identifies repeated challenge counts
- Excludes duplicated counts unless the count equals the maximum challenge count
- Sorts results according to the problem rules

---

# 🐬 MySQL Solution

```sql

WITH total_challenges_cte AS (
    SELECT
        hacker_id,
        COUNT(*) AS total_challenge
    FROM challenges
    GROUP BY hacker_id
),
valid_repeated_challenges_cte AS (
    SELECT total_challenge AS n_repeated_challenges
    FROM total_challenges_cte
    GROUP BY total_challenge
    HAVING COUNT(*) = 1
        OR total_challenge >=
            (SELECT MAX(total_challenge)
             FROM total_challenges_cte)
)

SELECT
    hacker_id,
    name,
    tc.total_challenge
FROM total_challenges_cte AS tc
INNER JOIN valid_repeated_challenges_cte AS vrc
    ON tc.total_challenge = vrc.n_repeated_challenges
INNER JOIN hackers
USING(hacker_id)
ORDER BY
    tc.total_challenge DESC,
    hacker_id;

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

WITH total_challenges_cte AS (
    SELECT
        hacker_id,
        COUNT(*) AS total_challenge
    FROM challenges
    GROUP BY hacker_id
),
valid_repeated_challenges_cte AS (
    SELECT
        total_challenge AS n_repeated_challenges
    FROM total_challenges_cte
    GROUP BY total_challenge
    HAVING COUNT(*) = 1
       OR total_challenge = (
            SELECT MAX(total_challenge)
            FROM total_challenges_cte
       )
)

SELECT
    h.hacker_id,
    h.name,
    tc.total_challenge
FROM total_challenges_cte tc
JOIN valid_repeated_challenges_cte vrc
    ON tc.total_challenge = vrc.n_repeated_challenges
JOIN hackers h
    ON h.hacker_id = tc.hacker_id
ORDER BY
    tc.total_challenge DESC,
    h.hacker_id;

exit;

```

---

## ✅ Query Breakdown

### 🔹 `COUNT(*)`

Counts the total number of challenges created by each hacker.

---

### 🔹 `GROUP BY hacker_id`

Groups records by hacker to calculate individual challenge counts.

---

### 🔹 `HAVING COUNT(*) = 1`

Keeps challenge counts that appear only once.

---

### 🔹 `MAX(total_challenge)`

Finds the highest number of challenges created by any hacker.

---

### 🔹 Duplicate Count Rule

If multiple hackers share the same challenge count:

- Include them only if that count equals the maximum challenge count
- Otherwise exclude them

---

### 🔹 `ORDER BY tc.total_challenge DESC`

Sorts hackers by total challenges in descending order.

---

### 🔹 `h.hacker_id`

If counts are equal, sorts by hacker ID in ascending order.

---

## ✅ Final Output Example

```text
21283 Angela 6
88255 Patrick 5
96196 Lisa 1
```

Meaning:

- Angela created `6` challenges
- Patrick created `5` challenges
- Lisa created `1` challenge

---