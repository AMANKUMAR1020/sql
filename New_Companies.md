# 🏙️ SQL Challenge: New Companies

## 📝 Problem Statement
Amber's conglomerate corporation just acquired several new companies. Each company follows a hierarchical structure.

Write a query to display:
- `company_code`
- `founder`
- total number of **lead managers**
- total number of **senior managers**
- total number of **managers**
- total number of **employees**

Sort the result in **ascending order of company_code** (string-based sorting).

---

## ⚠️ Notes
- Tables may contain **duplicate records**
- Use **DISTINCT counts** to avoid duplication
- `company_code` is a **string**, so sorting is **lexicographical**, not numeric  
  - Example: `C1, C10, C2`

---

## 📊 Input Format

### 🏢 Company Table
| Column        | Description                  |
|---------------|------------------------------|
| company_code  | Unique company code          |
| founder       | Name of the founder          |

---

### 👨‍💼 Lead_Manager Table
| Column            | Description                  |
|-------------------|------------------------------|
| lead_manager_code | Lead manager code            |
| company_code      | Company code                 |

---

### 👨‍💼 Senior_Manager Table
| Column                | Description                  |
|------------------------|------------------------------|
| senior_manager_code    | Senior manager code          |
| lead_manager_code      | Lead manager code            |
| company_code           | Company code                 |

---

### 👨‍💼 Manager Table
| Column            | Description                  |
|-------------------|------------------------------|
| manager_code      | Manager code                 |
| senior_manager_code | Senior manager code        |
| lead_manager_code | Lead manager code            |
| company_code      | Company code                 |

---

### 👨‍💼 Employee Table
| Column              | Description                  |
|---------------------|------------------------------|
| employee_code       | Employee code                |
| manager_code        | Manager code                 |
| senior_manager_code | Senior manager code          |
| lead_manager_code   | Lead manager code            |
| company_code        | Company code                 |

---

## 📥 Sample Input

**Company Table**

| company_code | founder  |
|--------------|----------|
| C1           | Monika   |
| C2           | Samantha |

---

**Lead_Manager Table**

| lead_manager_code | company_code |
|-------------------|--------------|
| LM1               | C1           |
| LM2               | C2           |

---

**Senior_Manager Table**

| senior_manager_code | lead_manager_code | company_code |
|---------------------|------------------|--------------|
| SM1                 | LM1              | C1           |
| SM2                 | LM1              | C1           |
| SM3                 | LM2              | C2           |

---

**Manager Table**

| manager_code | senior_manager_code | lead_manager_code | company_code |
|--------------|---------------------|------------------|--------------|
| M1           | SM1                 | LM1              | C1           |
| M2           | SM3                 | LM2              | C2           |
| M3           | SM3                 | LM2              | C2           |

---

**Employee Table**

| employee_code | manager_code | senior_manager_code | lead_manager_code | company_code |
|---------------|-------------|---------------------|------------------|--------------|
| E1            | M1          | SM1                 | LM1              | C1           |
| E2            | M1          | SM1                 | LM1              | C1           |
| E3            | M2          | SM3                 | LM2              | C2           |
| E4            | M3          | SM3                 | LM2              | C2           |

---

## 📤 Sample Output


C1 Monika 1 2 1 2
C2 Samantha 1 1 2 2


---

## 🧠 Explanation

### 🔹 Company C1
- Lead Managers: 1 (LM1)
- Senior Managers: 2 (SM1, SM2)
- Managers: 1 (M1)
- Employees: 2 (E1, E2)

### 🔹 Company C2
- Lead Managers: 1 (LM2)
- Senior Managers: 1 (SM3)
- Managers: 2 (M2, M3)
- Employees: 2 (E3, E4)

---

## 🐬 MySQL Solution


```sql
SELECT 
    e.company_code, 
    c.founder, 
    COUNT(DISTINCT e.lead_manager_code), 
    COUNT(DISTINCT e.senior_manager_code), 
    COUNT(DISTINCT e.manager_code), 
    COUNT(DISTINCT e.employee_code)
FROM Employee e 
INNER JOIN Company c
    ON c.company_code = e.company_code
GROUP BY e.company_code, c.founder
ORDER BY e.company_code;

```

## ⭕ Oracle SQL Solution

```sql id="company-final-sql"
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
    e.company_code, 
    c.founder, 
    COUNT(DISTINCT e.lead_manager_code), 
    COUNT(DISTINCT e.senior_manager_code), 
    COUNT(DISTINCT e.manager_code), 
    COUNT(DISTINCT e.employee_code)
FROM Employee e 
INNER JOIN Company c
    ON c.company_code = e.company_code
GROUP BY e.company_code, c.founder
ORDER BY e.company_code;

EXIT;
```