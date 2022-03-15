## Window Function

Window functions are slightly different between database dialects.  
Window functions operate the same way in both SQLite and PostgreSQL.  

### OVER

Clause for creating windowed functions.  

### Aggregate window functions

Aggregates values for each row depending on the size of the sliding window, the order of rows, filter and partition specified in the OVER clause.  

### FILTER

Excludes row values from being aggregated inside a partition.  
The aggregate will still be calculated for the excluded row, the aggregate just won't include the excluded value.  

* ... FILTER (WHERE c!='two') OVER ...

### PARTITION BY

Splits rows into partitions.  

### ORDER BY

Orders the rows within each partition.  

### Frame

Defines the size of the sliding window.  

Parts:
* frame type - either ROWS, RANGE or GROUPS
* starting frame boundary
* ending frame boundary; defaults to CURRENT ROW
* EXCLUDE clause

Keywords:
* BETWEEN
* UNBOUNDED
* PRECEDING
* CURRENT ROW
* FOLLOWING

Default:
* ... RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW EXCLUDE NO OTHERS ...

### Built-in windowed functions

See WindowFunctionsTutorial.  
