# 🏙️ SQL Challenge: Weather Observation Station 4

## 📝 Problem Statement
Find the **difference** between the **total number of CITY entries** in the table and the **number of distinct CITY entries** in the table.
The **STATION** table is described as follows:

### Database Schema: STATION


| Field  | Type         |
|--------|--------------|
| ID     | NUMBER       |
| CITY   | VARCHAR2(21) |
| STATE  | VARCHAR2(2)  |
| LAT_N  | NUMBER       |
| LONG_W | NUMBER       |

---

## 🐘 Solutions

### 🐬 MySQL

```sql

SELECT COUNT(CITY) - COUNT(DISTINCT CITY) FROM STATION;

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

/*
Enter your query here.
Please append a semicolon ";" at the end of the query and enter your query in a single line to avoid error.
*/

SELECT COUNT(CITY) - COUNT(DISTINCT CITY) FROM STATION;

exit;
```












