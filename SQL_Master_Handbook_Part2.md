# SQL Master Handbook – Part 2 (Intermediate & Interview)

## 1. Subqueries

A query inside another query.

Types:
- Scalar
- Multiple Row
- Correlated
- FROM Subquery

FROM subqueries require aliases.

```sql
SELECT *
FROM(
SELECT dept_id,COUNT(*) total_orders
FROM employee
GROUP BY dept_id
) t;
```

---

## 2. CTE

Common Table Expression.

Temporary named result set.

```sql
WITH emp_cte AS
(
SELECT *
FROM employee
)
SELECT *
FROM emp_cte;
```

Why use?
- Readability
- Break complex queries
- Recursive queries
- Filter window functions

---

## 3. View

Saved SELECT statement.

```sql
CREATE VIEW EmployeeView AS
SELECT * FROM employee;
```

Acts like a virtual table.

---

## 4. Function

Reusable SQL object returning one value or one table.

```sql
CREATE FUNCTION dbo.GetBonus(@salary INT)
RETURNS INT
AS
BEGIN
RETURN @salary*10/100;
END;
```

Use:

```sql
SELECT dbo.GetBonus(salary)
FROM employee;
```

---

## 5. Stored Procedure

Reusable SQL program.

```sql
CREATE PROCEDURE GetEmployees
AS
BEGIN
SELECT * FROM employee;
END;
```

Run:

```sql
EXEC GetEmployees;
```

Can INSERT, UPDATE, DELETE and SELECT.

---

## 6. Window Functions

Unlike GROUP BY, they keep every row.

ROW_NUMBER()

RANK()

DENSE_RANK()

LEAD()

LAG()

SUM() OVER()

AVG() OVER()

Example:

```sql
SELECT emp_name,
salary,
AVG(salary)
OVER(PARTITION BY dept_id) avg_salary
FROM employee;
```

Aggregate:
Many rows → One row

Window:
Many rows → Many rows + calculated column

---

## 7. Aggregate vs Window

GROUP BY

```sql
SELECT dept_id,
SUM(salary)
FROM employee
GROUP BY dept_id;
```

Window

```sql
SELECT emp_name,
salary,
SUM(salary)
OVER(PARTITION BY dept_id)
FROM employee;
```

---

## 8. Comparison

| Feature | CTE | View | Function | Stored Procedure |
|---|---|---|---|---|
| Permanent | No | Yes | Yes | Yes |
| Parameters | No | No | Yes | Yes |
| Reusable | One query | Yes | Yes | Yes |
| Returns | Table | Table | Value/Table | Result sets |
| Modify Data | No | Limited | No | Yes |

---

## 9. Interview Patterns

- Top N per category
- Second highest salary
- Premium customers
- Missing departments
- Invalid department IDs
- Returned sales
- Business days
- First & Last Name extraction
- Conditional aggregation

---

## 10. Data Scientist SQL Roadmap

Master:
SELECT
WHERE
JOIN
GROUP BY
HAVING
CASE
Subqueries
CTEs
Window Functions
Date Functions
String Functions

Good:
Views
Functions
Stored Procedures
Indexes

Rare:
Triggers
Cursors
Transactions

---

## 11. Important Interview Rules

1. FROM subqueries need aliases.
2. Window functions cannot be filtered in the same SELECT.
3. COUNT(column) ignores NULL.
4. LEFT JOIN + IS NULL finds missing rows.
5. CASE inside SUM() is conditional aggregation.
6. Use CTEs for readability.
