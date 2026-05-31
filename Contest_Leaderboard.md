# 📍 SQL Challenge: Contest Leaderboard

## 📝 Problem Statement

The total score of a hacker is the sum of their maximum scores for all challenges.

Write a query to print:

```text
hacker_id name total_score
```

for hackers ordered by descending total score.

---

## 📊 Input Format

The following tables contain contest data:

---

### 👨‍💻 Hackers Table

| Column | Type | Description |
|--------|------|-------------|
| hacker_id | Integer | Hacker ID |
| name | String | Hacker Name |

---

### 📝 Submissions Table

| Column | Type | Description |
|--------|------|-------------|
| submission_id | Integer | Submission ID |
| hacker_id | Integer | Hacker ID |
| challenge_id | Integer | Challenge ID |
| score | Integer | Submission Score |

---

## 📌 Rules

1. The total score of a hacker is calculated as:

```text
Sum of maximum scores for each challenge
```

2. Exclude hackers whose total score is:

```text
0
```

3. Sort the result:
   - By `total_score` in descending order
   - If scores are equal, sort by `hacker_id` in ascending order

---

## 📤 Expected Output

Print:

```text
hacker_id name total_score
```

---

## 📥 Sample Output

```text
4071 Rose 191
74842 Lisa 174
84072 Bonnie 100
4806 Angela 89
26071 Frank 85
80305 Kimberly 67
49438 Patrick 43
```

---

## 💡 Explanation

The query:

- Finds the maximum score for each hacker on every challenge
- Sums those maximum scores
- Excludes hackers with total score `0`
- Sorts the leaderboard according to the rules

Example:

If a hacker scores:

| Challenge | Scores Submitted |
|-----------|------------------|
| 1 | 20, 50, 40 |
| 2 | 30, 70 |

Then:

```text
Total Score = 50 + 70 = 120
```

---

# 🐬 MySQL Solution

```sql

SELECT
        hackers.hacker_id,
        hackers.name,
        SUM(subquery1.max_score) AS total_score
FROM hackers
JOIN
(
        SELECT
                hackers.hacker_id,
                MAX(submissions.score) AS max_score
        FROM hackers
        JOIN submissions
            ON hackers.hacker_id = submissions.hacker_id
        GROUP BY hackers.hacker_id, submissions.challenge_id
) AS subquery1
ON subquery1.hacker_id = hackers.hacker_id
GROUP BY hackers.hacker_id, hackers.name
HAVING total_score != 0
ORDER BY total_score DESC, hackers.hacker_id;

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
    h.hacker_id,
    h.name,
    SUM(sq.max_score) AS total_score
FROM hackers h
JOIN (
    SELECT
        s.hacker_id,
        s.challenge_id,
        MAX(s.score) AS max_score
    FROM submissions s
    GROUP BY s.hacker_id, s.challenge_id
) sq
ON sq.hacker_id = h.hacker_id
GROUP BY h.hacker_id, h.name
HAVING SUM(sq.max_score) != 0
ORDER BY total_score DESC, h.hacker_id;

exit;

```

---

## ✅ Query Breakdown

### 🔹 `MAX(s.score)`

Finds the highest score a hacker achieved for each challenge.

---

### 🔹 `GROUP BY s.hacker_id, s.challenge_id`

Groups submissions by hacker and challenge.

---

### 🔹 `SUM(max_score)`

Adds the highest scores from all challenges to calculate the total score.

---

### 🔹 `HAVING SUM(sq.max_score) != 0`

Excludes hackers whose total score is `0`.

---

### 🔹 `ORDER BY total_score DESC`

Sorts hackers by highest total score first.

---

### 🔹 `h.hacker_id ASC`

If total scores are equal, sorts by hacker ID in ascending order.

---

## ✅ Final Output Example

```text
4071 Rose 191
74842 Lisa 174
84072 Bonnie 100
```

Meaning:

- Rose achieved the highest total score = `191`
- Lisa achieved total score = `174`
- Bonnie achieved total score = `100`

---