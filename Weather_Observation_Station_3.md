# 🏙️ SQL Challenge: Weather Observation Station 3

## 📝 Problem Statement
Query a list of **CITY** names from **STATION** for cities that have an even ID number. Print the results in any order, but **exclude duplicates from the answer**.
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

SELECT DISTINCT CITY FROM STATION
WHERE ID%2=0;

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

SELECT DISTINCT CITY FROM STATION
WHERE MOD(ID,2)=0;

exit;

```












