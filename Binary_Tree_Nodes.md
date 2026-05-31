# 🏙️ SQL Challenge: The PADS

## 📝 Problem Statement
Generate the following two result sets from the `OCCUPATIONS` table:


Pivot the Occupation column in `OCCUPATIONS` so that each  `Name is sorted alphabetically` and displayed underneath its corresponding Occupation. The output should consist of four columns (Doctor, Professor, Singer, and Actor) in that specific order, with their respective names listed alphabetically under each column.

### Note: Print NULL when there are no more names corresponding to an occupation.

---

## 📊 Input Format

The `OCCUPATIONS` table contains:

| Column     | Type   | Description                      |
|------------|--------|----------------------------------|
| name       | String | Name of the person              |
| occupation | String | Profession of the person        |

> Occupation will only contain: **Doctor, Professor, Singer, Actor**

---

## 📥 Sample Input

| name      | occupation |
|-----------|------------|
| Samantha  | Doctor     |
| Julia     | Actor      |
| Maria     | Actor      |
| Meera     | Singer     |
| Ashely    | Professor  |
| Ketty     | Professor  |
| Christeen | Professor  |
| Jane      | Actor      |
| Jenny     | Doctor     |
| Priya     | Singer     |

---

## 📤 Sample Output

`
Jenny    Ashley     Meera  Jane
Samantha Christeen  Priya  Julia
NULL     Ketty      NULL   Maria
Explanation
`
---

---
The first column is an alphabetically ordered list of Doctor names.
The second column is an alphabetically ordered list of Professor names.
The third column is an alphabetically ordered list of Singer names.
The fourth column is an alphabetically ordered list of Actor names.
The empty cell data for columns with less than the maximum number of names per occupation (in this case, the Professor and Actor columns) are filled with ***NULL*** values.

---


## 🐬 MySQL Solution

```sql

SELECT     
    O.N,
    CASE
        WHEN O.P IS NULL THEN 'Root'
        WHEN O.N IN (SELECT distinct I.P FROM BST I WHERE I.P = O.N) THEN 'Inner'
        --  WHEN O.N IN (SELECT DISTINCT P FROM BST WHERE P IS NOT NULL) THEN 'Inner'
        ELSE 'Leaf'
    END AS BST_
FROM BST O
ORDER BY O.N;

```


## ⭕ Oracle SQL Solution
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

/*
Enter your query here.
Please append a semicolon ";" at the end of the query and enter your query in a single line to avoid error.
*/

SELECT     
    O.N,
    CASE
        WHEN O.P IS NULL THEN 'Root'
        WHEN O.N IN (SELECT distinct I.P FROM BST I WHERE I.P = O.N) THEN 'Inner'
        --  WHEN O.N IN (SELECT DISTINCT P FROM BST WHERE P IS NOT NULL) THEN 'Inner'
        ELSE 'Leaf'
    END AS BST_
FROM BST O
ORDER BY O.N;

exit;

```









---

❌ What’s wrong in your query
1. ❌ CASE syntax is incorrect

You wrote:

CASE
    WHERE SELECT ...

👉 Problem:

CASE does NOT use WHERE
It uses WHEN + THEN

Correct structure:

CASE 
    WHEN condition THEN result
END
2. ❌ You cannot use SELECT * inside CASE like that

This is invalid:

WHEN SELECT * FROM BST ...

👉 In CASE, you only write conditions, not subqueries like that.

3. ❌ Wrong way to compare NULL

You wrote:

O.N = NULL

👉 Wrong in SQL.

Correct:

O.N IS NULL
4. ❌ Logic of BST problem is incorrect

To classify nodes in a Binary Search Tree:

Root → node where P IS NULL
Leaf → node not present as any parent
Inner → node that appears as a parent
✅ Correct Query
SELECT 
    O.N,
    CASE
        WHEN O.P IS NULL THEN 'Root'
        WHEN O.N NOT IN (SELECT DISTINCT P FROM BST WHERE P IS NOT NULL) THEN 'Leaf'
        ELSE 'Inner'
    END AS BST_
FROM BST O;
🧠 Explanation
🔹 Root
WHEN O.P IS NULL
Parent is NULL → root node
🔹 Leaf
WHEN O.N NOT IN (SELECT DISTINCT P FROM BST)
Node never appears as a parent → no children → leaf
🔹 Inner
ELSE 'Inner'
Node appears as a parent → has children
💡 Simple intuition
Node type   Meaning
Root    has no parent
Leaf    has no children
Inner   has both connections

---

