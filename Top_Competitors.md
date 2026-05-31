# 📍 SQL Challenge: Top Competitors

## 📝 Problem Statement

Julia just finished conducting a coding contest, and she needs your help assembling the leaderboard!

Write a query to print the respective `hacker_id` and `name` of hackers who achieved full scores for more than one challenge.

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

### 📈 Difficulty Table

| Column | Type | Description |
|--------|------|-------------|
| difficulty_level | Integer | Difficulty Level |
| score | Integer | Maximum Score for that difficulty |

---

### 🧩 Challenges Table

| Column | Type | Description |
|--------|------|-------------|
| challenge_id | Integer | Challenge ID |
| hacker_id | Integer | Creator Hacker ID |
| difficulty_level | Integer | Difficulty Level of challenge |

---

### 📝 Submissions Table

| Column | Type | Description |
|--------|------|-------------|
| submission_id | Integer | Submission ID |
| hacker_id | Integer | Hacker ID |
| challenge_id | Integer | Challenge ID |
| score | Integer | Submission Score |

---

## 📤 Expected Output

Print:

```text
hacker_id name
```

for hackers who achieved full scores in more than one challenge.

### 📌 Sorting Rules

1. Order by the total number of full-score challenges in descending order.
2. If multiple hackers have the same count, sort by `hacker_id` in ascending order.

---

## 📥 Sample Output

```text
90411 Joe
```

---

## 💡 Explanation

A hacker achieves a **full score** when:

```text
submission score = maximum score for the challenge difficulty
```

In the sample:

- Hacker `86870` achieved one full score
- Hacker `90411` achieved full scores in more than one challenge

Therefore, only:

```text
90411 Joe
```

is printed.

---

# 🐬 MySQL Solution

```sql

SELECT
    h.hacker_id,
    h.name
FROM Hackers h
JOIN (
    SELECT 
        s.hacker_id,
        COUNT(DISTINCT s.challenge_id) AS full_score_count
    FROM Submissions s
    JOIN Challenges c
        ON s.challenge_id = c.challenge_id
    JOIN Difficulty d
        ON c.difficulty_level = d.difficulty_level
    WHERE s.score = d.score
    GROUP BY s.hacker_id
    HAVING COUNT(DISTINCT s.challenge_id) > 1
) fs
ON h.hacker_id = fs.hacker_id
ORDER BY 
    fs.full_score_count DESC,
    h.hacker_id ASC;

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
    h.name
FROM Hackers h
JOIN (
    SELECT 
        s.hacker_id,
        COUNT(DISTINCT s.challenge_id) AS full_score_count
    FROM Submissions s
    JOIN Challenges c
        ON s.challenge_id = c.challenge_id
    JOIN Difficulty d
        ON c.difficulty_level = d.difficulty_level
    WHERE s.score = d.score
    GROUP BY s.hacker_id
    HAVING COUNT(DISTINCT s.challenge_id) > 1
) fs
ON h.hacker_id = fs.hacker_id
ORDER BY 
    fs.full_score_count DESC,
    h.hacker_id ASC;

exit;

```

---

## ✅ Query Breakdown

### 🔹 `JOIN Challenges`

Matches submissions with their corresponding challenges.

---

### 🔹 `JOIN Difficulty`

Gets the maximum possible score for each challenge difficulty level.

---

### 🔹 `WHERE s.score = d.score`

Filters submissions where the hacker achieved a full score.

---

### 🔹 `COUNT(DISTINCT s.challenge_id)`

Counts the number of unique challenges where a hacker achieved full marks.

---

### 🔹 `HAVING COUNT(DISTINCT s.challenge_id) > 1`

Filters hackers who achieved full scores in more than one challenge.

---

### 🔹 `ORDER BY fs.full_score_count DESC`

Sorts hackers by total full-score challenges in descending order.

---

### 🔹 `h.hacker_id ASC`

If counts are equal, sorts by hacker ID in ascending order.

---

## ✅ Final Output Example

```text
90411 Joe
```

Meaning:

- Hacker `90411` achieved full scores in multiple challenges.

---