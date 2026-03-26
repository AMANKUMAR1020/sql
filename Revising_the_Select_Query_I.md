# 🏙️ SQL Challenge: Revising the Select Query I

## 📝 Problem Statement
Query **all columns** for all American cities in the **CITY** table that meet the following criteria:
1.  **Population** must be greater than **100,000**.
2.  **CountryCode** must be **'USA'**.

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
WHERE POPULATION > 100000 
  AND COUNTRYCODE = 'USA';

###⭕ OracleSQL

```sql
SELECT * FROM CITY 
WHERE POPULATION > 100000 
  AND COUNTRYCODE = 'USA';


