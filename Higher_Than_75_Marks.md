
# 🏙️ SQL Challenge: Higher Than 75 Marks

## 📝 Problem Statement
Query the Name of any student in STUDENTS who **scored higher than  Marks 75**. Order your output by **the last three characters of each name**. **If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID**.



### Database Schema: STUDENTS


| Column | Type    |
|--------|---------|
| ID     | Integer |
| Name   | String  |
| Marks  | Integer |

---

## 🐘 Solutions

### 🐬 MySQL

```sql

SELECT NAME 
FROM STUDENTS
WHERE MARKS > 75
ORDER BY RIGHT(NAME,3), ID ASC;


```

###⭕ OracleSQL

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


--SELECT NAME 
--FROM STUDENTS
--WHERE MARKS > 75
--ORDER BY UPPER(SUBSTR(NAME,LENGTH(NAME)-2,3)), ID ASC;

--OR

SELECT NAME 
FROM STUDENTS
WHERE MARKS > 75
ORDER BY UPPER(SUBSTR(NAME,-3)), ID ASC;

exit;
```

explaination

SUBSTR(NAME,LENGTH(NAME)-2,3)
SUBSTR(NAME,LENGTH(NAME),3)
SUBSTR(NAME,-3)

Good question—these two are **not equivalent**, and they behave quite differently in Oracle SQL.

---

### 🔹 1. `SUBSTR(NAME, -3)`

* Starts **3 characters from the end** of the string
* Returns the **last 3 characters**

✅ Example:

```sql
SUBSTR('Bobby', -3)
```

Result: `'bby'`

✔ This is the **correct way** to get the last 3 characters.

---

### 🔹 2. `SUBSTR(NAME, LENGTH(NAME), 3)`

* `LENGTH(NAME)` gives the **position of the last character**
* So this starts at the **last character**, then tries to take 3 characters

✅ Example:

```sql
SUBSTR('Bobby', LENGTH('Bobby'), 3)
```

Result: `'y'`

❗ Why?

* It starts at position 5 (`'y'`)
* Only **1 character exists after that**, so Oracle returns just `'y'`

---

### 🔥 Key Difference

| Expression                      | Start Position | Result (for "Bobby") | Meaning               |
| ------------------------------- | -------------- | -------------------- | --------------------- |
| `SUBSTR(NAME, -3)`              | 3rd from end   | `bby`                | Last 3 characters ✅   |
| `SUBSTR(NAME, LENGTH(NAME), 3)` | Last character | `y`                  | Only last character ❌ |

---

### ✅ If you *don’t* want negative indexing

Use:

```sql
SUBSTR(NAME, LENGTH(NAME) - 2, 3)
```

---

### ✔ Final takeaway

* Use `SUBSTR(NAME, -3)` → **best and simplest**
* Avoid `SUBSTR(NAME, LENGTH(NAME), 3)` for this purpose—it does **not** return the last 3 characters

---

If you want, I can show edge cases (like names shorter than 3 characters) 👍

