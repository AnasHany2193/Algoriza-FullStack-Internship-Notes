## 📂 Week 02 - SQL (Suggested File Structure)

```text
📁 Week 02 - SQL/
├── 01 - Introduction & DB Basics.md
├── 02 - Constraints & Keys.md
├── 03 - Queries & Joins.md
├── 04 - Stored Procedures.md
├── 05 - Functions.md
├── 06 - Indexes & Views.md
├── 07 - Triggers.md
├── 08 - Subqueries & CTE.md
├── 09 - Date, String & Math Functions.md
├── 10 - Transactions & Error Handling.md
├── 11 - Performance & Advanced Concepts.md
```

---

## ✅ التقسيم التفصيلي حسب الفيديوهات:

| Module                                | Approx Video Numbers    |
| ------------------------------------- | ----------------------- |
| 01. **Introduction & DB Basics**      | 01 to 04                |
| 02. **Constraints & Keys**            | 05 to 10                |
| 03. **Queries & Joins**               | 11 to 15                |
| 04. **Stored Procedures**             | 19 to 22                |
| 05. **Functions**                     | 23 to 34                |
| 06. **Indexes & Views**               | 35 to 43                |
| 07. **Triggers**                      | 44 to 48                |
| 08. **Subqueries & CTE**              | 49 to 53                |
| 09. **Date, String & Math Functions** | 24 to 31 (with overlap) |
| 10. **Transactions & Error Handling** | 56 to 59                |
| 11. **Performance & Advanced**        | 60–71, 92–95, 102       |

---

## 📌 ملاحظات إضافية:

- الملفات متسماة بالأرقام عشان تظهر مرتبة تلقائيًا في Obsidian.
- تقدر تحط في أول كل ملف جدول زي كده:

```markdown
## 🎯 Covered Topics
- Constraints: Default, Check, Unique
- Keys: Primary, Foreign
- Identity Columns
- ...

## 📹 Covered Videos
- Part 05 - Adding a default constraint
- Part 06 - Cascading referential integrity
- Part 07 - Check Constraint
- Part 08 - Identity Column
```

---
## ✅ النسخة المخففة: 6 ملفات رئيسية مقترحة

```text
📁 Week 02 - SQL/
├── 01 - Basics & Constraints.md
├── 02 - Queries & Joins.md
├── 03 - Stored Procedures & Functions.md
├── 04 - Indexes, Views & Triggers.md
├── 05 - Subqueries, CTE & Performance.md
├── 06 - Transactions & Error Handling.md
```

---

### 📁 01 - Basics & Constraints

- Installation & Setup
- CREATE/ALTER/DROP DB & Tables
- Constraints: DEFAULT, CHECK, PRIMARY, FOREIGN, UNIQUE
- Identity Column & Getting last inserted ID

### 📁 02 - Queries & Joins

- SELECT basics
- GROUP BY
- JOINS: Inner, Left, Right, Self
- COALESCE, NULL handling, UNION, UNION ALL


### 📁 03 - Stored Procedures & Functions

- Stored procedures (IN, OUT, RETURN)
- String functions: `LEFT`, `RIGHT`, `SUBSTRING`, etc.
- Date functions: `DATEADD`, `DATEDIFF`, `ISDATE`, etc.
- Mathematical functions
- User-defined functions: Scalar, Table-Valued (inline, multi-statement)

### 📁 04 - Indexes, Views & Triggers

- Indexes: Clustered, Non-clustered, Unique
- Views: Basics, Updatable, Indexed
- Triggers: DML, Instead of, Execution Order, DDL

### 📁 05 - Subqueries, CTE & Performance

- Subqueries & Correlated Subqueries
- CTEs (Normal + Recursive)
- Derived Tables
- PIVOT
- Performance Tips: Joins vs Subqueries, Cursors, Merge, APPLY

### 📁 06 - Transactions & Error Handling

- Transactions, ACID
- TRY...CATCH
- Error handling (SQL Server 2000 vs 2008)
- Optional Params in SPs
- Re-runnable scripts