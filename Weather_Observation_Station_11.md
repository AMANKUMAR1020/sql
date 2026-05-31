# 🏙️ SQL Challenge: Weather Observation Station 11

## 📝 Problem Statement
Query the list of **either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.**. Your **result cannot contain duplicates**.
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
WHERE (CITY NOT LIKE '%A' 
   AND CITY NOT LIKE '%E' 
   AND CITY NOT LIKE '%I' 
   AND CITY NOT LIKE '%O' 
   AND CITY NOT LIKE '%U')
   OR (CITY NOT LIKE 'A%' 
   AND CITY NOT LIKE 'E%' 
   AND CITY NOT LIKE 'I%' 
   AND CITY NOT LIKE 'O%' 
   AND CITY NOT LIKE 'U%');

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
WHERE UPPER(SUBSTR(CITY, LENGTH(CITY), 1)) NOT IN ('A','E','I','O','U') OR UPPER(SUBSTR(CITY, 1, 1)) NOT IN ('A','E','I','O','U');



exit;

```












