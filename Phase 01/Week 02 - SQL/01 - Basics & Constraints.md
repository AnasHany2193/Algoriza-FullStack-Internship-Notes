## ✅ Installing SQL Server & SSMS

- Install **SQL Server** to create/manage databases and **SQL Server Management Studio (SSMS)** to interact with SQL Server via GUI and queries.
- Real-World Use Case: Developers use SSMS to connect to the local SQL Server instance and manage production or development databases.

---

## 🏗️ Create, Alter, Delete Database

```sql
-- Create a new database
CREATE DATABASE Sample2;

-- Rename a database (using ALTER)
ALTER DATABASE Sample2 MODIFY NAME = Sample3;

-- Rename using system stored procedure
EXEC sp_renamedb 'Sample3', 'Sample4';

-- Drop (delete) a database
DROP DATABASE Sample4;
```

> 💡 `ALTER DATABASE ... MODIFY NAME` works only when no one is connected to the database. Use `sp_renamedb` for broader compatibility.

---
## 📋 Creating and Working with Tables

```sql
-- Create a lookup table for genders
CREATE TABLE tblGender (
	ID INT NOT NULL PRIMARY KEY,
	Gender NVARCHAR(50) NOT NULL
);

-- Create a person table
CREATE TABLE tblPerson (
	ID INT PRIMARY KEY,
	Name NVARCHAR(100) NOT NULL,
	Email NVARCHAR(100),
	GenderId INT,
	Age INT
);

-- Add a foreign key constraint to reference Gender table
ALTER TABLE tblPerson 
ADD CONSTRAINT FK_tblPerson_GenderId 
FOREIGN KEY (GenderId) REFERENCES tblGender(ID);
```

> 💡 Foreign keys enforce **referential integrity**. A `GenderId` in `tblPerson` must exist in `tblGender`.

---
## 🛠️ DEFAULT Constraint

```sql
-- Add default GenderId value (e.g., 3 = 'Unknown')
ALTER TABLE tblPerson 
ADD CONSTRAINT DF_tblPerson_GenderId DEFAULT 3 FOR GenderId;

-- Insert without GenderId (it will default to 3)
INSERT INTO tblPerson (ID, Name, Email) 
VALUES (4, 'Harry', 'harry@gmail.com');

-- Drop the default constraint
ALTER TABLE tblPerson 
DROP CONSTRAINT DF_tblPerson_GenderId;
```

> 💡 Use DEFAULT to reduce NULLs or manual entry for commonly-used values (e.g., default status = 'active').

---
## ✅ CHECK Constraint

```sql
-- Add constraint to ensure age is realistic
ALTER TABLE tblPerson 
ADD CONSTRAINT CK_tblPerson_Age CHECK (Age > 0 AND Age < 150);

-- Example that violates the constraint
INSERT INTO tblPerson VALUES (5, 'Sarah', 'sarah@gmail.com', 2, -90); -- ❌ Fails

-- Remove the check constraint
ALTER TABLE tblPerson 
DROP CONSTRAINT CK_tblPerson_Age;
```

> 💡 Use CHECK to enforce **business logic**, like valid ranges for age, salary, or dates.

---
## 🔢 IDENTITY Columns

```sql
-- Create a table with IDENTITY auto-increment
CREATE TABLE Person (
	ID INT IDENTITY(1,1), 
	Value NVARCHAR(20)
);

-- Insert values (ID auto-generated)
INSERT INTO Person (Value) VALUES ('Anas'), ('Hany');

-- Reset identity value
DBCC CHECKIDENT(Person, RESEED, 0); -- Next insert will be 1

-- Get last inserted ID in current session/scope
SELECT SCOPE_IDENTITY() AS LastInsertedID;

-- Also available:
SELECT @@IDENTITY; -- Not scope-specific (⚠️ can be unsafe)
```

> 🧠 Use `SCOPE_IDENTITY()` for safe identity tracking within current scope (e.g., after a trigger or stored procedure insert).

---
## 🔐 UNIQUE Constraint

```sql
-- Add unique constraint on Gender column
ALTER TABLE tblGender 
ADD CONSTRAINT UQ_tblGender_Gender UNIQUE(Gender);

-- Try inserting a duplicate Gender (will fail)
INSERT INTO tblGender VALUES (3, 'Male'); -- ❌ Fails if 'Male' already exists

-- Drop the unique constraint
ALTER TABLE tblGender 
DROP CONSTRAINT UQ_tblGender_Gender;
```

> 💡 Use UNIQUE when a column value should never repeat (e.g., email, username). It allows one NULL by default.

---
## 🔁 Real-World Use Cases Recap

|Constraint Type|Example Use Case|
|---|---|
|`DEFAULT`|Default status = 'Active'|
|`CHECK`|Age must be between 18 and 60|
|`PRIMARY KEY`|Uniquely identify a person|
|`FOREIGN KEY`|Link employee to department|
|`UNIQUE`|Prevent duplicate emails|
|`IDENTITY`|Auto-generate user IDs|

---
**إِنَّ اللَّهَ وَمَلَائِكَتَهُ يُصَلُّونَ عَلَى النَّبِيِّ ۚ يَا أَيُّهَا الَّذِينَ آمَنُوا صَلُّوا عَلَيْهِ وَسَلِّمُوا تَسْلِيمًا (56)**
