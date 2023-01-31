---
title: Date and time functions
list_title: Date and time functions
description: >
  Use functions unique to working with time series data.
menu:
  influxdb_cloud_iox:
    name: Date and time functions
    parent: SQL functions
weight: 230
---

## The NOW() function

The `NOW` function returns the current date and time.  Use the NOW() function to query data with timestamps relative to the server's current timestamp.  

Note that return type timestamp looks like this: `2023-01-30T20:48:52.722Z`. The timezone is the server's location.

NOW() function syntax:

```
(time >= now() - interval <'insert_interval')
```



```sql
SELECT "water_level", "time"
FROM h2o_feet
WHERE time <= now() - interval '20 days'
```

## The DATE_BIN() function

The `DATE_BIN` function "bins" the input timestamp into a specified time interval.  DATE_BIN syntax looks like this:

```sql
DATE_BIN(INTERVAL <'insert_interval'>, time, TIMESTAMP '<rfc3339_date_time_string>')
```

The first argument is the interval you want to bin or window by. The second argument is the time value, and can also be a column to operate on.  The third argument is the starting point used to determine window boundaries.

Supported intervals include seconds, minutes, hours, days and years.  

```sql
SELECT DATE_BIN(INTERVAL '1 day', time, TIMESTAMP '2022-01-01 00:00:00Z') AS time, AVG("water_level")  as water_level_avg
FROM "h2o_feet"
WHERE time >= timestamp '2019-09-10T00:00:00Z' AND time <= timestamp '2019-09-20T00:00:00Z'
GROUP BY 1
ORDER BY 1 DESC
```

Results:

| time                     | water_level_avg    |
| :----------------------- | :----------------- |
| 2019-09-17T00:00:00.000Z | 4.3642002317349045 |
| 2019-09-16T00:00:00.000Z | 4.605945251510415  |
| 2019-09-15T00:00:00.000Z | 4.680911918172915  |
| 2019-09-14T00:00:00.000Z | 4.85976073572917   |
| 2019-09-13T00:00:00.000Z | 4.911743186958335  |
| 2019-09-12T00:00:00.000Z | 4.766101201200004  |
| 2019-09-11T00:00:00.000Z | 4.657891084837502  |
| 2019-09-10T00:00:00.000Z | 4.608416685452088  |
| 2019-09-09T00:00:00.000Z | 3.77               |

The query returns the timestamp and the average water level for each day within the specified time period.


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

