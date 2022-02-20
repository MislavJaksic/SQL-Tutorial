## Select Star SQL

### Beazley's Last Statement

View SQL queries as blocks.  

Wildcards: + % _
String quotes: ''
Column, table name backtick marks it as a name

SELECT
FROM
WHERE < > <= >= like NOT AND OR IS (must evaluate to TRUE or FALSE)
LIMIT

### Claims of Innocence

Aggregate functions take multiple rows create a single row.  

NULL is an empty entry.  

```
CASE
    WHEN <clause> THEN <result>
    WHEN <clause> THEN <result>
    ...
    ELSE <result>
END
```

COUNT: does not count NULLs. Count NULLs with `*`
MIN, MAX
AVG
LENGTH
DISTINCT: not a true aggregate function

### The Long Tail

The only rows that needn't be aggregated are those that are in the GROUP BY.  

Queries can be nested.  
It is a good idea to demarcate them.  
They are neccessery when you have to both GROUP BY and aggregate and aggregate without grouping at the same time.  
Percentiles notoriously need nested queries.  

GROUP BY: apply aggregate function within each group specified in SELECT
<expression> AS <alias>
HAVING: Like WHERE but after grouping and aggregations.

### Execution Hiatuses

JOINs create a new table by combining two tables.  

The clause in the JOIN is similar to a clause in WHERE.  
The clause must evaluate to TRUE or FALSE.  

If the clause condition is not met, the unmatched rows are dropped.  
You can specify LEFT or OUTER to keep the unmatched rows.  

If there are multiple matches, enough rows are created so that each matching row gets its own partner.  

The LEFT and OUTER JOINs are stronger then the clause: even if the clause is FALSE or the rows don't match, the rows will stil be kept.  

Each SQL dialect has functions that operate on dates.  
