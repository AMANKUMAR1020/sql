# 🏙️ SQL Challenge: Weather Observation Station 10

## 📝 Problem Statement
Query the list of **CITY names NOT END with vowels (i.e., a, e, i, o, or u) from STATION**. Your **result cannot contain duplicates**.
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

SELECT DISTINCT CITY
FROM STATION
WHERE CITY LIKE '%A' 
   AND CITY LIKE '%E' 
   AND CITY LIKE '%I' 
   AND CITY LIKE '%O' 
   AND CITY LIKE '%U';

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

SELECT DISTINCT CITY
FROM STATION
WHERE UPPER(SUBSTR(CITY, LENGTH(CITY), 1)) NOT IN ('A','E','I','O','U');


exit;

```












