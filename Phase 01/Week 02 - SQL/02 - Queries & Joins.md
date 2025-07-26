## 1️⃣ SELECT Basics

```sql
-- Select all or specific columns
SELECT * FROM tblPerson;
SELECT Name, Age, Email FROM tblPerson;

-- Eliminate duplicates
SELECT DISTINCT Age FROM tblPerson;

-- Filtering
SELECT * FROM tblPerson WHERE Age < 25;
SELECT * FROM tblPerson WHERE Age IN (22, 24, 26);
SELECT * FROM tblPerson WHERE Age BETWEEN 22 AND 26;
SELECT * FROM tblPerson WHERE Email LIKE '%@%.com';
SELECT * FROM tblPerson WHERE Email LIKE '[ADF]%';

-- Logical filters
SELECT * FROM tblPerson WHERE GenderID = 1 AND Age > 21;

-- Ordering
SELECT * FROM tblPerson ORDER BY Name ASC;
SELECT * FROM tblPerson ORDER BY Name DESC;

-- Limit results
SELECT TOP 5 * FROM tblPerson;
SELECT TOP 5 PERCENT * FROM tblPerson;
```

**Clarifications:**

- `DISTINCT` filters unique values.
- `LIKE '[ADF]%'` matches names starting with A, D, or F.
- `TOP 5 PERCENT` returns the top N% of rows.

---
## 2️⃣ GROUP BY & Aggregates

```sql
SELECT SUM(Salary) FROM Employee;
SELECT MIN(Salary), MAX(Salary) FROM Employee;

-- Group by department
SELECT Department, SUM(Salary) AS TotalSalary, COUNT(ID) AS TotalEmployees
FROM Employee
GROUP BY Department;

-- Add multiple grouping columns
SELECT Department, JobTitle, SUM(Salary)
FROM Employee
GROUP BY Department, JobTitle;
```

**Notes:**

- Every column selected must be in `GROUP BY` or aggregated.
- Useful for metrics dashboards (e.g., average salary per department).

---

## 3️⃣ JOINS — Explained Clearly

### INNER JOIN

> Returns rows with matching keys in both tables.

```sql
SELECT e.Name, d.DepartmentName
FROM Employees e
JOIN Departments d ON e.DepartmentID = d.DepartmentID;
```

```
 Diagram (A = Employees, B = Departments)
   +---+
   | A |
   +---+
     \
      \
       +---+  <- Intersection = result
       | B |
       +---+
```

([Coding Horror](https://blog.codinghorror.com/a-visual-explanation-of-sql-joins/?utm_source=chatgpt.com "A Visual Explanation of SQL Joins - Coding Horror"), [W3Schools](https://www.w3schools.com/sql/sql_join.asp?utm_source=chatgpt.com "SQL Joins - W3Schools"), [SQL Shack](https://www.sqlshack.com/sql-join-overview-and-tutorial/?utm_source=chatgpt.com "SQL Join types overview and tutorial"))

### LEFT JOIN

> All rows from left (Employees), plus matches from right, others become NULL.

```
+---+     +---+
| A |-----| B |
+---+     +---+
 result: A ∪ (A ∩ B)
```

([SQL Shack](https://www.sqlshack.com/sql-multiple-joins-for-beginners-with-examples/?utm_source=chatgpt.com "SQL multiple joins for beginners with examples - SQLShack"))

### RIGHT JOIN

> All rows from right table, plus matches from left.

```
+---+     +---+
| A |-----| B |
+---+     +---+
 result: B ∪ (A∩B)
```

### FULL JOIN

> All rows from both tables; unmatched sides are `NULL`.

```
+---+     +---+
| A |-----| B |
+---+     +---+
 result: A ∪ B
```

### CROSS JOIN

> Every combination (Cartesian product).

```sql
SELECT e.Name, d.DepartmentName
FROM Employees e
CROSS JOIN Departments d;
```

---

## 4️⃣ Advanced Join Filters

- **Left-only** non-matches:
    
    ```sql
    SELECT e.Name
    FROM Employees e
    LEFT JOIN Departments d ON e.DepartmentID = d.DepartmentID
    WHERE d.DepartmentID IS NULL;
    ```
    
- **Right-only** non-matches using RIGHT JOIN.
- **Non-matching from both:**
    
    ```sql
    SELECT *
    FROM Employees e
    FULL JOIN Departments d ON e.DepartmentID = d.DepartmentID
    WHERE e.DepartmentID IS NULL OR d.DepartmentID IS NULL;
    ```

---

## 5️⃣ SELF JOIN

> Employees referencing managers within same table.

```sql
SELECT e.Name AS Employee, m.Name AS Manager
FROM Employees e
LEFT JOIN Employees m ON e.ManagerID = m.EmployeeID;
```

---

## 6️⃣ Handling NULLs — ISNULL, CASE, COALESCE

### ISNULL

```sql
SELECT e.Name, ISNULL(m.Name, 'No Manager') AS Manager
FROM Employees e
LEFT JOIN Employees m ON e.ManagerID = m.EmployeeID;
```

### CASE equivalent:

```sql
CASE WHEN m.Name IS NULL THEN 'No Manager' ELSE m.Name END
```

### COALESCE

> Returns the first non-NULL value:

```sql
SELECT COALESCE(FirstName, MiddleName, LastName) AS Name
FROM Person;

SELECT COALESCE(FirstName + ' ', '') +
       COALESCE(MiddleName + ' ', '') +
       COALESCE(LastName, '') AS FullName
FROM Person;
```

**Key differences:**

- `ISNULL` uses only two arguments; `COALESCE` allows multiple ([en.wikipedia.org](https://en.wikipedia.org/wiki/Relational_algebra?utm_source=chatgpt.com "Relational algebra"), [W3Schools](https://www.w3schools.com/sql/sql_join.asp?utm_source=chatgpt.com "SQL Joins - W3Schools"), [TechOnTheNet](https://www.techonthenet.com/sql_server/joins.php?utm_source=chatgpt.com "SQL Server: Joins - TechOnTheNet"), [SQL Authority with Pinal Dave](https://blog.sqlauthority.com/2023/06/15/sql-server-difference-between-isnull-and-coalesce/?utm_source=chatgpt.com "SQL SERVER - Difference Between ISNULL and COALESCE"), [C# Corner](https://www.c-sharpcorner.com/UploadFile/rohatash/differences-between-isnull-and-coalesce-functions-in-sql/?utm_source=chatgpt.com "Differences Between IsNull() and Coalesce() Functions in SQL ..."))
- `COALESCE` adheres to ANSI SQL standards; `ISNULL` uses first argument’s type([MSSQLTips](https://www.mssqltips.com/sqlservertip/2689/deciding-between-coalesce-and-isnull-in-sql-server/?utm_source=chatgpt.com "Deciding between COALESCE and ISNULL in SQL Server"))

---
## 7️⃣ UNION vs UNION ALL

> Combine rows from multiple SELECTs:

```sql
SELECT * FROM Customers
UNION
SELECT * FROM NewsletterSubscribers;

-- Include duplicates:
SELECT * FROM Customers
UNION ALL
SELECT * FROM NewsletterSubscribers;
```

- `UNION` removes duplicates.
- `UNION ALL` is faster and preserves duplicates.
- Both require same number of columns and compatible data types.

---

## 🧠 Real-World Scenarios

- **INNER JOIN**: Get orders and related customer info.
- **LEFT JOIN**: List all products, even for those with zero sales.
- **FULL JOIN**: Audit to show missing records in either system.
- **SELF JOIN**: Find managers reporting lines.
- **COALESCE**: Build fallback name display when fields are missing.
- **UNION**: Combine confirmed vs. unconfirmed email lists for marketing (with or without duplicates).

---
**إِنَّ اللَّهَ وَمَلَائِكَتَهُ يُصَلُّونَ عَلَى النَّبِيِّ ۚ يَا أَيُّهَا الَّذِينَ آمَنُوا صَلُّوا عَلَيْهِ وَسَلِّمُوا تَسْلِيمًا (56)**