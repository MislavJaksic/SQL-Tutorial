## [Window Functions](https://www.sqlite.org/windowfunctions.html)

See Practice/WindowFunctionsTutorial.sqlnb for examples.  

### Introduction to Window Functions

If a function has an OVER clause, then it is a window function.  
Window functions might also have a FILTER clause in between the function and the OVER clause.  

Window functions cannot use the DISTINCT keyword.  

Window functions come in two varieties:
* aggregate window functions
* built-in window functions

```
--   x | y | row_number
-----------------------
--   1 | aaa | 1         
--   2 | ccc | 3         
--   3 | bbb | 2         
-- 
SELECT x,
       y,
       row_number() OVER (ORDER BY y) AS row_number
FROM t0
ORDER BY x;
```
`row_number()` assigns number by the `ORDER BY y` clause to each row in the window.  
In the example, the window is the size of the whole table.  
However, the final order is governed by `ORDER BY x`.  

```
SELECT x,
       y,
       row_number() OVER win1,
       rank() OVER win2 
FROM t0 
WINDOW win1 AS (ORDER BY y RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW),
       win2 AS (PARTITION BY y ORDER BY x)
ORDER BY x;
```
WINDOW clause allows windows to be referred to by name within window function invocations.  

### Aggregate window functions

Aggregates values for each row depending on the size of the sliding window, the order of rows, filter and partition specified in the OVER clause.  

### The PARTITION BY Clause

A partition consists of all rows that have the same value for all terms of the PARTITION BY clause.  
Window-function processing is performed separately for each partition.  

### Frame Specifications

Determines which rows are read.  

Parts:
* frame type - either ROWS, RANGE or GROUPS
* starting frame boundary
* ending frame boundary; defaults to CURRENT ROW
* EXCLUDE clause

If RANGE or GROUPS, then rows with the same values for all ORDER BY expressions are considered peers.  

### The FILTER Clause

ToDo