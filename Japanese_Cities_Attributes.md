# 🏙️ SQL Challenge: query city with ID

## 📝 Problem Statement
Query all attributes of every Japanese city in the **CITY** table. The **COUNTRYCODE** for Japan is **JPN**:

### Database Schema: CITY


| Field | Type | Description |
| :--- | :--- | :--- |
| **ID** | `NUMBER` | Primary Key |
| **NAME** | `VARCHAR2(17)` | City Name |
| **COUNTRYCODE** | `VARCHAR2(3)` | 3-letter Country Code |
| **DISTRICT** | `VARCHAR2(20)` | District/State Name |
| **POPULATION** | `NUMBER` | Total Residents |

---

## 🐘 Solutions

### 🐬 MySQL

```sql
SELECT * FROM CITY
WHERE COUNTRYCODE='JPN';

```


###⭕ OracleSQL

```sql
SET FEEDBACK OFF;
SET ECHO OFF;
SET HEADING OFF;
SET WRAP OFF;
SET LINESIZE 10000;
SET TAB OFF;


SELECT * FROM CITY
WHERE COUNTRYCODE='JPN';


exit;
```


