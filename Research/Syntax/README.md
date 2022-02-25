## Syntax

SELECT Expressions
FROM Table-Name
JOIN Table-Name ON Clause
JOIN ...
WHERE Clause
GROUP BY Expressions
HAVING Clause
ORDER BY Expressions
LIMIT Number

### SELECT

Define what columns will be displayed, renamed or aggregated:
* SELECT *
* SELECT Table-Name.Column-Name AS Alias-Name
* SELECT Aggregate-Function(Column-Name) AS Alias-name
* SELECT CASE ... END
* SELECT 50 + 2, 51 * 2

### FROM

Specifies from which table you are querying:
* FROM Table-Name

### JOIN

Joins two tables:
* Table-A JOIN Table-B ON Clause
* Table-A AS A1 JOIN Table-A AS A2 ON Clause
* ... OUTER JOIN ... ON ... LEFT JOIN Table-C ON Clause

The clause in the JOIN is similar to a clause in WHERE.  

Types:
* INNER: drop unmatched rows from both tables; the default
* LEFT/RIGHT: preserve unmatched rows from either left or right table
* OUTER: preserve unmatched rows from both tables
* self JOIN is where a table JOIN onto itself

If the clause condition is not met, the unmatched rows are dropped.  
If there are multiple matches, enough rows are created so that each matching row gets its own partner.  

The LEFT and OUTER JOINs are stronger then the clause: even if the clause is FALSE or the rows don't match, the rows will stil be kept.  

### WHERE

Filter rows with a clause:
* WHERE Clause

### GROUP BY

Split and then apply an aggregate function within each group specified in SELECT to create a row per group:
* SELECT Non-Aggregate-Column, COUNT(`*`) GROUP BY Non-Aggregate-Column

Grouping columns are the only columns allowed to be non-aggregate.  

### HAVING

Like WHERE but after grouping and aggregations:
* HAVING COUNT(`*`) > 2

### ORDER BY

Sort rows:
* ORDER BY Column-Name, ..., Column-Name
* ORDER BY Column-Name DESC

### LIMIT

Limits the number of output rows:
* LIMIT 3
* LIMIT 100

### Comments

* `--`
* `/* */`

### Strings

SQL strings are enclosed with single quote marks ''.  

### Boolean

Depends on the SQL dialect, but generally:
* TRUE: TRUE, 't', 'true', 'y', 'yes', 'on', '1'
* FALSE: FALSE, 'f', 'false', 'n', 'no', 'off', '0'

### Dates

Each SQL dialect has functions that operate on dates.  

### NULL

Null is a special value that isn't an empty string '' or a zero.  
It is treated differently from all other values.  

### Expressions

Expression is a combination of one or more values, operators and SQL functions that evaluate to a value.  

* `*`
* Aggregate-Function(Column-Name)
* 50 + 2

### Operators

* Arithmatic: `< > <= >= = !=`
* Boolean: NOT, AND, OR
* String: LIKE and wildcards `+ % _`
* Null: IS NULL and IS NOT NULL gives binary output 0 or 1

### Clauses

Boolean statements that evaluate to TRUE or FALSE.  
Most often used in WHERE and HAVING:
* WHERE last_name = 'Beazley'
* WHERE last_name LIKE '%Landry%'
* JOIN ... ON executions.ex_number = previous.ex_number

### Aggregate functions

Think about them top-down and how rows need to be transformed to allow aggregate functions to work.  

COUNT: does not count NULLs. Count NULLs with `*`
SUM
MIN, MAX
AVG
DISTINCT: not a true aggregate function

### CASE WHEN blocks

It is able to transform the row into a different value.  

```
CASE 
    WHEN Clause THEN Value
    WHEN Clause THEN Value
    ELSE Value
END
```

### Nesting queries

```
Find the first and last name of the inmate with the longest last statement:
SELECT first_name, last_name
FROM executions
WHERE LENGTH(last_statement) =
    (SELECT MAX(LENGTH(last_statement))
	 FROM executions)
```

```
Find the percentage of executions from each county:
SELECT
  county,
  100.0 * COUNT(*) / (SELECT COUNT(*) FROM executions)
    AS percentage
FROM executions
GROUP BY county
ORDER BY percentage DESC
```

```
SELECT
  last_ex_date AS start,
  ex_date AS end,
  JULIANDAY(ex_date) - JULIANDAY(last_ex_date)
    AS day_difference
FROM executions
JOIN (SELECT ex_prev.ex_number, ex_current.ex_date AS last_ex_date
      FROM executions AS ex_prev
      JOIN executions AS ex_current
      ON ex_prev.ex_number = ex_current.ex_number + 1) previous
  ON executions.ex_number = previous.ex_number
ORDER BY day_difference DESC
LIMIT 10
```
