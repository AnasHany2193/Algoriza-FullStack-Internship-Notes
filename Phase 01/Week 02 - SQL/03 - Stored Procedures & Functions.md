## 1️⃣ Stored Procedures

### 🔹 What Are They?

> Reusable groups of T‑SQL statements compiled and executed on the server. Great for encapsulating logic, reusability, and reducing network traffic.

### ⚡ Simple Stored Procedure (no parameters)

```sql
CREATE PROCEDURE spGetEmployees
AS
BEGIN
    SELECT Name, Gender FROM Employees;
END;
GO

EXEC spGetEmployees;
```

### 🔹 With Input Parameters

```sql
CREATE PROCEDURE spGetEmployeesByGenderAndDept
    @Gender NVARCHAR(20),
    @DepartmentId INT
AS
BEGIN
    SELECT Name, Gender, DepartmentID
    FROM Employees
    WHERE Gender = @Gender
      AND DepartmentID = @DepartmentId;
END;
GO

EXEC spGetEmployeesByGenderAndDept 'Male', 1;
EXEC spGetEmployeesByGenderAndDept @DepartmentId = 1, @Gender = 'Female';
```

> 💡 Use named parameters for clarity and flexibility.
### 🔹 With Output Parameters

```sql
CREATE PROCEDURE spGetEmployeeCountByGender
    @Gender NVARCHAR(20),
    @Count INT OUTPUT
AS
BEGIN
    SELECT @Count = COUNT(*)
    FROM Employees
    WHERE Gender = @Gender;
END;
GO

DECLARE @Total INT;
EXEC spGetEmployeeCountByGender 'Male', @Total OUTPUT;
PRINT @Total;
```

### 🔹 With Return Value

Use integer return for status codes, not data.

```sql
CREATE PROCEDURE spGetTotalEmployees
AS
BEGIN
    RETURN (SELECT COUNT(*) FROM Employees);
END;
GO

DECLARE @Total INT;
EXEC @Total = spGetTotalEmployees;
PRINT @Total;
```

### 🛠️ Real-World Use Case

- Use SPs to centralize business logic (e.g., `spCreateOrder`) that updates multiple tables and performs validations.

### ✅ Best Practices for Stored Procedures

|Tip|Why|
|---|---|
|Use meaningful names (`spGet…`, `uspGet…`)|Improves readability|
|Validate input parameters early|Prevents SQL injection and invalid data|
|Avoid excessive length or complexity|Easier to maintain and test|
|Consider transaction scope within SP|Ensures data consistency|

---

## 2️⃣ Built-in SQL Functions

### 🔹 String Functions

```sql
SELECT
    ASCII('A'),
    CHAR(65),
    LTRIM('  Hello'),
    RTRIM('World  '),
    LOWER('ABC'),
    UPPER('abc'),
    REVERSE('abc'),
    LEN('Hello'),
    LEFT('Hello', 2),
    RIGHT('World', 3),
    CHARINDEX('l', 'Hello', 1),
    SUBSTRING('Hello', 2, 3),
    REPLICATE('Ha', 3),
    SPACE(5),
    PATINDEX('%@example.com', Email),
    REPLACE(Email, 'example', 'gmail'),
    STUFF(Email, 2, 5, '*****')
FROM Customers;
```

> 🔍 Practical: Use `STUFF` or `REPLACE` to mask sensitive data (e.g., hide part of Social Security numbers).

### 🔹 Date/Time Functions

```sql
SELECT
    GETDATE(),
    CURRENT_TIMESTAMP,
    SYSDATETIME(),
    SYSDATETIMEOFFSET(),
    GETUTCDATE(),
    SYSUTCDATETIME(),
    ISDATE('2021-01-01'),
    DAY(GETDATE()),
    MONTH(GETDATE()),
    YEAR(GETDATE()),
    DATENAME(WEEKDAY, '2003-09-21'),
    DATEADD(DAY, 40, '2003-09-21'),
    DATEDIFF(YEAR, '2003-09-21', '2013-09-01');
```

> 🔍 Real-world: Calculating employee anniversaries, due dates, etc.

### 🔹 CAST vs CONVERT

```sql
SELECT 
  CAST(HireDate AS DATE) AS HireDateOnly,
  CAST(Salary AS DECIMAL(10,3)) AS SalaryDecimal,
  CONVERT(VARCHAR(10), HireDate, 120) AS ISODate,
  CONVERT(VARCHAR(10), HireDate, 101) AS USDate,
  CONVERT(DECIMAL(10,3), Salary) AS ConvSalary
FROM Employees;
```

> 💡 Use `CONVERT` when specific output format is needed (use style codes).

### 🔹 Math Functions

```sql
SELECT
    ABS(val),
    CEILING(val),
    FLOOR(val),
    POWER(val, 2),
    SQUARE(val),
    SQRT(ABS(val)),
    ROUND(val, 1)
FROM Numbers;
```

---

## 3️⃣ User-Defined Functions (UDFs)

### 🔹 Scalar UDF

Returns a single scalar value.

```sql
CREATE FUNCTION dbo.CtoF(@Celsius FLOAT)
RETURNS FLOAT
AS
BEGIN
    RETURN (@Celsius * 9.0 / 5.0 + 32);
END;
GO

SELECT n AS Celsius, dbo.CtoF(n) AS Fahrenheit
FROM Numbers;
```

### 🔹 Inline Table-Valued UDF (TVF)

Returns a table; optimal for performance.

```sql
CREATE FUNCTION dbo.GetDepartmentSalaries(@DeptID INT)
RETURNS TABLE
AS
RETURN
(
    SELECT EmpID, Name, Salary
    FROM Employees
    WHERE DeptID = @DeptID
);
GO

SELECT * FROM dbo.GetDepartmentSalaries(2);
```

### 🔹 Multi-Statement TVF

```sql
CREATE FUNCTION dbo.DeptSalarySummary()
RETURNS @Summary TABLE
(
    DeptID INT,
    DeptName VARCHAR(50),
    AvgSalary DECIMAL(10,2),
    TotalSalary DECIMAL(18,2),
    EmpCount INT
)
AS
BEGIN
    INSERT INTO @Summary
    SELECT d.DeptID, d.DeptName,
           AVG(e.Salary), SUM(e.Salary), COUNT(e.EmpID)
    FROM Departments d
    LEFT JOIN Employees e ON e.DeptID = d.DeptID
    GROUP BY d.DeptID, d.DeptName;

    RETURN;
END;
GO

SELECT * FROM dbo.DeptSalarySummary();
```

---

## 4️⃣ SP vs UDF Comparison

|Feature|Stored Procedure|User-Defined Function|
|---|---|---|
|Returns data|Yes (via result set/output)|Scalar or table result|
|Can be used in SELECT|No|Yes (inline in queries)|
|Supports transactions|Yes|No|
|Can change data|Yes|No (mostly read-only)|
|Performance considerations|Precompiled|Inline TVFs are faster; multi-statement may sponsor temp tables|
### 🧩 Use Cases

- **Stored Procedures**: Handling complex business logic, chaining inserts/updates, login processes, ETL routines.
- **Scalar Functions**: Reusable calculations, e.g., currency conversion.
- **Inline TVFs**: Lightweight wrapper over joins or views for querying.
- **Multi-statement TVFs**: Complex data shape building not doable with inline TVFs.

---

## ✅ Performance & Best Practices

- Prefer **inline TVFs** over multi-statement UDFs for performance.
- Avoid scalar UDFs inside large result-sets — they are row-by-row and cause slowdowns. 
- Minimize context switches — move non-T‑SQL logic to SPs or external application.
- For heavy logic, consider using stored procedures with table-valued parameters instead.

---
**إِنَّ اللَّهَ وَمَلَائِكَتَهُ يُصَلُّونَ عَلَى النَّبِيِّ ۚ يَا أَيُّهَا الَّذِينَ آمَنُوا صَلُّوا عَلَيْهِ وَسَلِّمُوا تَسْلِيمًا (56)**