---
layout: post 
title: Date in MS SQL
categories: [Record]
tags: [tsa]
published: True

---
## Problem

There are duplicate records in my data, i.e. the datetime and device of transactions are identical. Apparently, two transactions cannot take place at the same device at the same time. So I decided to clean out the duplicate records by comparing the datetime.

```sql
select [columns],
       Datediff(
                second,
                datetime,
                lag(datetime, 1) over (partition by device order by datetime) -- the previous record
       ) as [TimeDiff]
from table
```

Note that the `lag` function cannot be used in `WHERE` clause so I have to build a new table then filter the rows of which `TimeDiff` are 0.

The `Datediff` function returns `int`, which is 4 bytes. Concerning the metric of differencing is second, it could compute time difference over 50 years. However, an overflow of date part took place.


## Causes

Some records in my data is dated back to 1899 when computers has not been invented. These are definitely error and the date is filled by MSSQL with default values. I tried to cast the datetime difference to `bigint`, which is 8 bytes thus the whole history could be presented in seconds. But I was still alerted about the overflow error. I suppose there are some issues regarding the default date (`1899-12-31`).


## Solution

Exclude the default date by setting a threshold (e.g. 1980).

```sql
year(datetime) > 1980
```


