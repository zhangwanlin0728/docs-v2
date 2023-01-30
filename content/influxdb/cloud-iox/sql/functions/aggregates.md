---
title: SQL aggregate functions
list_title: Aggregate functions
description: >
  Aggregate data with SQL aggregate functions.
menu:
  influxdb_cloud_iox:
    name: Aggregates
    parent: SQL functions
weight: 210
---

### The MIN() function

```sql
SELECT MIN("water_level") as minimum_level, "location"
FROM "h2o_feet" 
GROUP BY "location"
```

Results:
| location     | minimum_level |
| :----------- | :------------ |
| coyote_creek | -0.61         |
| santa_monica | -0.243        |


### The MAX() function

```sql
SELECT MAX("water_level") as maximum_level, "location"
FROM "h2o_feet" 
GROUP BY "location"
```

Results:
| location     | maximum_level |
| :----------- | :------------ |
| santa_monica | 7.205         |
| coyote_creek | 9.964         |

### The COUNT() function

The COUNT() function returns the number of rows from a field or tag.

```sql
SELECT COUNT("water_level") 
FROM "h2o_feet"
```

Results:

| COUNT(h2o_feet.water_level) |
| :-------------------------- |
| 15258                       |


### The AVG() function

```sql
SELECT AVG("water_level"), "location"
FROM "h2o_feet" 
GROUP BY "location"


SELECT AVG("water_level"), "location"
FROM "h2o_feet" 
WHERE "time" >= '2019-08-18T09:00:00Z'::timestamp AND "time" <= '2019-08-18T21:00:00Z'::timestamp 
GROUP BY  "location"
```


### The SUM() function

```sql
SELECT SUM("water_level"), "location"
FROM "h2o_feet" 
GROUP BY "location"
```


