## [SQL for data analysis: what you can do without Pandas](https://hakibenita.com/sql-for-data-analysis)

### SQL vs Pandas Performance

To take advantage of both worlds and create lightweight programs that are also fast, use SQL and Pandas together!

### Basics

The SQL query language has subtle differences between popular database engines such as PostgreSQL, MySQL, Oracle, SQL Server.  

```
SELECT <expressions>
FROM <tables>
JOIN <to other table> ON <join condition>
WHERE <predicates>
GROUP BY <expressions>
HAVING <predicate>
ORDER BY <expressions>
LIMIT <number of rows>
```

#### Common Table Expressions

It's sometimes useful to split a large query into smaller steps.  
Common Table Expression or CTE is defined with the WITH clause.  
You can have multiple CTEs that depend on each other.  

```
WITH emails AS (
    SELECT 'ME@hakibenita.com' AS email
),
     normalized_emails AS (
    SELECT lower(email) AS email FROM emails
)
SELECT * FROM normalized_emails;
```

#### Generating Data

Generating data is very handy. Sometimes you need to generate data for practice, sometime you need to generate a time series or a small table to join to. There are several ways to generate data in SQL:

##### UNION ALL

##### VALUES LIST

##### UNNEST

##### GENERATE_SERIES

##### GENERATE_SERIES with row numbers

#### Random

#### Random Choice

#### Sampling

#### Example: Train / Test Split with SQL

### Descriptive Statistics

#### Describing a Series

#### Describing a Categorical Series

### Subtotals

#### Rollup

#### Cube

#### Grouping Sets

### Pivot Tables

### Running and Cumulative Aggregation

```
SELECT
    *,
    MAX(c) OVER (
        ORDER BY t
        ROWS BETWEEN 2 PRECEDING AND CURRENT ROW -- or RANGE BETWEEN '2 days' PRECEDING AND '0 days' FOLLOWING
    ) AS hottest_temperature_last_three_days
FROM
    temperatures;
```

### Linear Regression

### Interpolation

### Binning

### Take Away
