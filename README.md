## SQL

SQL (Structured Query Language) is used to manage relational databases. View it as a specification, rather then a language.  

Each database has its own flavour of SQL called a dialect.  
The tutorial assumes you are using SQLite as a database and [DB Browser for SQLite](https://github.com/MislavJaksic/Knowledge-Repository/tree/master/Technology/Storage/Embedded/SQLite) as a tool.  

Practice examples are stored in [SQL Notebook](https://github.com/MislavJaksic/Knowledge-Repository/tree/master/Technology/Storage/Inspector/SQLNotebook), a [Jupyter](https://jupyter.org/)-style notebook.  

### Create a Database

SQLite:
```
$: sqlite3 Database-Name.sqlite
```
DB Browser for SQLite:
```
File -> New Database -> name and save it
```

### Create a Table

```
CREATE TABLE "Table-Name" (
	"int_field"	    INTEGER CHECK(int_field >= 10),
	"numeric_field"	NUMERIC NOT NULL,
	"real_field"	REAL UNIQUE,
	"text_field"	TEXT DEFAULT '',
	"blob_field"	BLOB,
	FOREIGN KEY("numeric_field") REFERENCES "Another-Table"("Another-Table-Column"),
	PRIMARY KEY("int_field" AUTOINCREMENT)
);
```

#### Import Table from CSV

DB Browser for SQLite:
```
File -> Import -> Table from CSV file -> check and save it
```

Optionally, you can create the tables first, then import the CSV.  

### Syntax

```
SELECT Expressions
FROM Table-Name
JOIN Table-Name ON Clause
JOIN ...
WHERE Clause
GROUP BY Expressions
HAVING Clause
ORDER BY Expressions
LIMIT Number
```

See [Syntax under Research](Research/Syntax).  

### Order of Operations

1) FROM/JOIN and all the ON conditions
2) WHERE
3) GROUP BY
4) HAVING
5) SELECT (including window functions)
6) ORDER BY
7) LIMIT

### Aggregate functions

* COUNT: does not count NULLs. Count NULLs with `*`
* SUM
* MIN, MAX
* AVG
* DISTINCT: not a true aggregate function

### Date and time

* Subtract days: `date(Column-Name, '-' || Column-Name || ' days')`

### Common Table Expression (CTE, WITH)

A named temporary result set.  
Concise, replaces subqueries, allows recursive CTEs.  

```
WITH Cte-Table-1 AS (...),
     Cte-Table-2 AS (...)
SELECT ... FROM Cte-Table-1
```

### Window Functions

```
aggregate_window_function() OVER (PARTITION BY Expressions
                                  ORDER BY Expressions
                                  ROWS/RANGE/GROUPS Keywords/Expressions)
```

Keywords:
* BETWEEN
* UNBOUNDED
* PRECEDING
* CURRENT ROW
* FOLLOWING

See [WindowFunction under Research](Research/WindowFunction).  

### Self-joins

ToDo

### Tips and tricks

Problems that involve consecutivness: use rank() and then subtract a number from a column and then group by the new column
