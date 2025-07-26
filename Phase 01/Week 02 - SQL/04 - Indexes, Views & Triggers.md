## Temporary Tables

```SQL
-- Local Temporary Tables: prefixed with #, visible only to your session.
SELECT	* 
INTO		#TempEmp 
FROM		Employees
WHERE		Dept = 'Engineer';

SELECT * FROM #TempEmp;

-- Global Temporary Tables: prefixed with ##, accessible to all sessions until the session ends and all references drop.
SELECT * 
INTO ##AllSales
FROM Employees
WHERE Dept = 'Engineer';

SELECT * FROM ##AllSales;
```
## Index

```SQL
-- Index is a data structure that speed up data retrival
-- Adventages
-- > Improve SELECT query performance
-- > Help with sorting and JOIN operations
-- DisAdventatges
-- > Each index has a storage and slow down INSERT, UPDATE, DELETE
-- > Requires maintenance

-- Clustered Index
-- > stores table row based on key
CREATE CLUSTERED INDEX IX_Products_Category 
       ON Product(Category);

-- Non‑Clustered Index
-- > Creates a separate structure with pointers to data pages.
CREATE NONCLUSTERED INDEX IX_Products_Price 
       ON Product(Price);

-- Unique Index
-- > Enforces the uniqueness of the indexed column(s).
CREATE UNIQUE INDEX UQ_Products_Name 
       ON Product(Name);
```
