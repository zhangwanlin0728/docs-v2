---
title: Time series functions
list_title: Time series functions
description: >
  Use functions unique to working with time series data.
menu:
  influxdb_cloud_iox:
    name: Time series 
    parent: SQL functions
weight: 230
---

## The NOW() function



## The DATE_BIN() function

The `DATE_BIN` function "bins" the input timestamp into a specified time interval.  The DATE_BIN function is constructed in the following manner:

1. This first argument is the interval you want to window by.  Supported intervals include seconds, minutes, hours, days and years.  
2. The second argument is the tiime value or column to operate om

```sql
SELECT DATE_BIN(INTERVAL '1 day', time, TIMESTAMP '2022-01-01 00:00:00Z') AS time, AVG("water_level")  as water_level_avg
FROM "h2o_feet"
WHERE time >= timestamp '2019-09-10T00:00:00Z' AND time <= timestamp '2019-09-20T00:00:00Z'
GROUP BY 1
ORDER BY 1 DESC
```

Results:

| time                     | water_level_avg |
| :----------------------- | --------------- |
| 2019-09-17T00:00:00.000Z | 381             |
| 2019-09-16T00:00:00.000Z | 2               |







## The DATE_TRUNC() function



```sql
SELECT date_trunc('month',time) AS "date",
SUM(water_level)
FROM "h2o_feet"
GROUP BY time
```

### The DATE_PART() function







<!-- ## The TIME_BUCKET_GAPFILL function (not working for Jan 31 release)


```sql
SELECT time_bucket_gapfill('1 day', time, TIMESTAMP '2022-01-01 00:00:00Z') as day,
"degrees", "location", "time"
FROM "h2o_temperature"
GROUP BY 1,2
ORDER BY 1,2
``` -->

