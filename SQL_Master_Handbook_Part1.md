# SQL Master Handbook – Part 1 (Fundamentals)

## 1. SQL Categories

| Category | Meaning | Commands |
|---|---|---|
| DDL | Defines database objects | CREATE, ALTER, DROP, TRUNCATE |
| DML | Manipulates data | INSERT, UPDATE, DELETE |
| DQL | Retrieves data | SELECT |
| DCL | Controls permissions | GRANT, REVOKE |
| TCL | Controls transactions | COMMIT, ROLLBACK |

---

## 2. CREATE TABLE

### Definition
Creates a new table in the database.

### Syntax
```sql
CREATE TABLE employee(
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    salary INT
);
```

### When to use
Whenever you need a new table.

---

## 3. INSERT

### Definition
Adds new rows.

```sql
INSERT INTO employee(emp_id,emp_name,salary)
VALUES(1,'Ramesh',50000);
```

---

## 4. UPDATE

Updates existing records.

```sql
UPDATE employee
SET salary=60000
WHERE emp_id=1;
```

Always use WHERE unless updating every row.

---

## 5. DELETE

Deletes rows.

```sql
DELETE FROM employee
WHERE emp_id=1;
```

---

## 6. SELECT

Retrieves data.

```sql
SELECT *
FROM employee;
```

---

## 7. WHERE

Filters rows before grouping.

```sql
SELECT *
FROM employee
WHERE salary>50000;
```

Think: "Only keep rows satisfying the condition."

---

## 8. ORDER BY

Sorts data.

```sql
ORDER BY salary DESC;
```

ASC = Ascending

DESC = Descending

---

## 9. DISTINCT

Removes duplicate values.

```sql
SELECT DISTINCT dept_id
FROM employee;
```

---

## 10. Aggregate Functions

COUNT() → Counts rows

SUM() → Adds values

AVG() → Average

MIN() → Minimum

MAX() → Maximum

Example

```sql
SELECT dept_id,
SUM(salary)
FROM employee
GROUP BY dept_id;
```

Aggregation reduces many rows into fewer rows.

---

## 11. GROUP BY

Groups similar rows.

```sql
SELECT dept_id,
AVG(salary)
FROM employee
GROUP BY dept_id;
```

Use whenever aggregate functions are needed per group.

---

## 12. HAVING

Filters groups after GROUP BY.

```sql
SELECT dept_id,
SUM(salary)
FROM employee
GROUP BY dept_id
HAVING SUM(salary)>100000;
```

WHERE → filters rows

HAVING → filters groups.

---

## 13. JOINS

INNER JOIN → matching rows only

LEFT JOIN → all left rows

RIGHT JOIN → all right rows

FULL JOIN → all rows from both tables

SELF JOIN → table joined with itself.

Interview Pattern:

```sql
LEFT JOIN ...
WHERE right_table.id IS NULL;
```

Finds missing records.

---

## 14. CASE WHEN

SQL IF-ELSE.

```sql
SUM(
CASE
WHEN r.order_id IS NOT NULL
THEN sales
ELSE 0
END)
```

Used for conditional aggregation.

---

## 15. Date Functions

GETDATE() → Current datetime

DATEDIFF() → Difference between dates

DATEADD() → Add days/months/years

DATEPART() → Extract year/month/day

DATENAME() → Month or weekday name

---

## 16. String Functions

LEN() → Length

LEFT() → Left characters

RIGHT() → Right characters

SUBSTRING() → Extract text

CHARINDEX() → Find position

TRIM() → Remove spaces

REPLACE() → Replace text

Example:

```sql
SELECT
LEFT(customer_name,CHARINDEX(' ',customer_name)-1)
FROM orders;
```

---

## 17. NULL Functions

IS NULL

IS NOT NULL

ISNULL()

COALESCE()

COUNT(column) ignores NULL values.

---

## 18. CAST vs CONVERT

CAST() → Simple datatype conversion.

CONVERT() → Datatype conversion with formatting.

---

## 19. SQL Execution Order

FROM
JOIN
WHERE
GROUP BY
HAVING
SELECT
ORDER BY

Remember:
SQL executes in this order, not the order you write.
