---
title: SQL selector functions
list_title: Selector functions
description: >
  Select data with SQL selector functions.
menu:
  influxdb_cloud_iox:
    name: Selectors
    parent: SQL functions
weight: 220
---

Selector functions are unique to time series databases.  Like aggregate functions, selector functions are used to reduce the size of your results set.  Unlike aggregates, which return a single modified value based on an aggregate condition, selectors can return multiple rows of values.  For example, selector_min and selector_max can return multiple values if the value is a tie.  Selectors also allow you to group aggregate values by time.

An aggregate finction will modify a value and return the value.  A selector says "here's the row per the logic you have chosen". 



### The SELECTOR_MIN() function

Examples:

```sql
SELECT 
SELECTOR_MIN(water_level, time)['value'],
SELECTOR_MIN(water_level, time)['time'],
FROM h2o_feet
```
Results:

| time                     | value |
| :----------------------- | :---- |
| 2019-08-28T14:30:00.000Z | -0.61 |

### The SELECTOR_MAX() function

### The SELECTOR_FIRST() function

### The SELECTOR_LAST() function

```sql
SELECT 
SELECTOR_LAST(degrees, time)['time'],
SELECTOR_LAST(degrees, time)['value']
FROM h2o_temperature
WHERE time >= timestamp '2019-09-15T00:00:00Z' AND time <= timestamp '2019-09-19T00:00:00Z'
```

Results:

| time            | value |
| :----------------------- | :---- |
| 2019-09-17T16:24:00.000Z | 63    |
