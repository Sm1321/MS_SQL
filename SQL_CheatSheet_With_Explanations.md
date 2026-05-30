
# SQL Learning Cheat Sheet with Simple Explanations

## DDL (Data Definition Language)
Used to create or modify database objects.

### CREATE TABLE
**Purpose:** Create a new table.

```sql
CREATE TABLE employee (
    emp_id INT,
    emp_name VARCHAR(50)
);
```

### ALTER TABLE
**Purpose:** Modify an existing table.

```sql
ALTER TABLE employee ADD salary INT;
```

### DROP TABLE
**Purpose:** Delete a table permanently.

```sql
DROP TABLE employee;
```

---

# Constraints
Rules applied to columns.

| Constraint | Meaning |
|------------|----------|
| PRIMARY KEY | Unique + Not Null |
| FOREIGN KEY | Links two tables |
| NOT NULL | Value is mandatory |
| UNIQUE | No duplicates allowed |
| CHECK | Custom condition |
| DEFAULT | Default value |

Example:

```sql
emp_id INT PRIMARY KEY
```

---

# DML (Data Manipulation Language)
Used to work with data.

### INSERT
Add new rows.

```sql
INSERT INTO employee(emp_id,emp_name)
VALUES(1,'Ramesh');
```

### UPDATE
Modify existing rows.

```sql
UPDATE employee
SET emp_name='Mohan'
WHERE emp_id=1;
```

### DELETE
Remove rows.

```sql
DELETE FROM employee
WHERE emp_id=1;
```

---

# SELECT
Retrieve data from table.

```sql
SELECT * FROM orders;
```

---

# WHERE
Filter rows.

```sql
SELECT *
FROM orders
WHERE sales > 100;
```

Think: "Only show rows matching condition".

---

# DISTINCT
Remove duplicates.

```sql
SELECT DISTINCT category
FROM orders;
```

---

# ORDER BY
Sort records.

```sql
ORDER BY sales DESC
```

DESC = Highest to Lowest

ASC = Lowest to Highest

---

# Aggregate Functions

| Function | Meaning |
|-----------|---------|
| COUNT() | Count rows |
| SUM() | Total |
| AVG() | Average |
| MIN() | Smallest value |
| MAX() | Largest value |

Example:

```sql
SELECT SUM(sales)
FROM orders;
```

---

# GROUP BY

Creates groups before aggregation.

```sql
SELECT category,
       SUM(sales)
FROM orders
GROUP BY category;
```

Think:

"Group similar values together."

---

# HAVING

Filters groups.

```sql
SELECT category,
       SUM(sales)
FROM orders
GROUP BY category
HAVING SUM(sales)>1000;
```

Difference:

- WHERE → Filters rows
- HAVING → Filters groups

---

# JOINS

Combine tables.

## INNER JOIN

Only matching records.

```sql
SELECT *
FROM orders o
INNER JOIN returns r
ON o.order_id=r.order_id;
```

## LEFT JOIN

All rows from left table.

```sql
SELECT *
FROM orders o
LEFT JOIN returns r
ON o.order_id=r.order_id;
```

Interview Pattern:

Find unmatched rows:

```sql
WHERE r.order_id IS NULL
```

---

# SELF JOIN

Join a table with itself.

```sql
employee e1
JOIN employee e2
ON e1.manager_id=e2.emp_id
```

Used for:
- Employee & Manager
- Parent & Child

---

# CASE WHEN

SQL IF-ELSE.

```sql
CASE
WHEN sales>1000 THEN 'High'
ELSE 'Low'
END
```

Conditional Aggregation:

```sql
SUM(
CASE
WHEN r.order_id IS NOT NULL
THEN sales
ELSE 0
END
)
```

---

# Date Functions

## GETDATE()

Current DateTime

```sql
SELECT GETDATE();
```

## DATEDIFF()

Difference between dates.

```sql
DATEDIFF(DAY,order_date,ship_date)
```

## DATEADD()

Add days/months/years.

```sql
DATEADD(DAY,5,order_date)
```

## DATEPART()

Extract year/month/day.

```sql
DATEPART(YEAR,order_date)
```

---

# String Functions

## LEN()

Length of string.

```sql
LEN(customer_name)
```

## LEFT()

Characters from left.

```sql
LEFT(customer_name,5)
```

## RIGHT()

Characters from right.

```sql
RIGHT(customer_name,3)
```

## SUBSTRING()

Extract part of string.

```sql
SUBSTRING(customer_name,1,5)
```

## CHARINDEX()

Find position.

```sql
CHARINDEX(' ',customer_name)
```

Example:

```text
'Mohan Kumar'

Space position = 6
```

## TRIM()

Remove extra spaces.

```sql
TRIM(customer_name)
```

Example:

```text
' Mohan '
```

becomes

```text
'Mohan'
```

---

# First Name / Last Name Logic

```sql
SELECT customer_name,
TRIM(
SUBSTRING(
customer_name,
1,
CHARINDEX(' ',customer_name)
)
) AS first_name,

SUBSTRING(
customer_name,
CHARINDEX(' ',customer_name)+1,
LEN(customer_name)
) AS last_name
FROM orders;
```

Logic:

1. Find first space using CHARINDEX.
2. Take everything before space = First Name.
3. Take everything after space = Last Name.

---

# NULL Handling

## IS NULL

```sql
WHERE city IS NULL
```

## IS NOT NULL

```sql
WHERE city IS NOT NULL
```

## ISNULL()

Replace NULL.

```sql
ISNULL(city,'Unknown')
```

---

# Conversion Functions

## CAST()

Convert datatype.

```sql
CAST(sales AS INT)
```

## CONVERT()

Convert datatype with format.

```sql
CONVERT(DATETIME,date_col,105)
```

105 = DD-MM-YYYY

120 = YYYY-MM-DD HH:MM:SS

---

# Set Operators

## UNION

Combine and remove duplicates.

## UNION ALL

Combine and keep duplicates.

## INTERSECT

Common records.

## EXCEPT

Records in first query but not second.

---

# Important Interview Patterns Learned

### Departments With No Employees

```sql
LEFT JOIN
WHERE e.emp_id IS NULL
```

### Employees With Invalid Department

```sql
LEFT JOIN
WHERE d.dep_id IS NULL
```

### Categories Total Sales & Returned Sales

```sql
SUM(sales)

SUM(
CASE
WHEN r.order_id IS NOT NULL
THEN sales
ELSE 0
END
)
```

### Sub Categories Having All 3 Return Reasons

```sql
HAVING COUNT(DISTINCT return_reason)=3
```

### Cities With No Returned Orders

```sql
HAVING COUNT(r.order_id)=0
```

---

# SQL Execution Order

1. FROM
2. JOIN
3. WHERE
4. GROUP BY
5. HAVING
6. SELECT
7. ORDER BY

Remember:

SQL executes in this order, not in the order we write.

---

# Next Topics To Learn

1. Subqueries
2. CTE
3. Window Functions
   - ROW_NUMBER()
   - RANK()
   - DENSE_RANK()
   - LEAD()
   - LAG()
4. Stored Procedures
5. Triggers
6. Indexes
7. Query Optimization

