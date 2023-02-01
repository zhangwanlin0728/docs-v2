---
title: The WHERE clause
list_title: The WHERE clause
description: > 
    Use the `WHERE` clause to filter results based on fields, tags, and/or timestamps.
menu:
  influxdb_cloud_iox:
    name: The WHERE clause
    parent: Explore data using SQL
weight: 220
---

Use the `WHERE` clause to filter results based on fields, tags, and/or timestamps.

- [Syntax](#syntax)
- [Examples](#examples)

### Syntax

```sql
SELECT_clause FROM_clause WHERE <conditional_expression> [(AND|OR) <conditional_expression> [...]]
```

{{% note %}}
**Note:** Unlike InfluxQL, SQL **supports** `OR` in the `WHERE` clause to specify multiple conditions, including time ranges.
{{% /note %}}

### Examples

Note that single quotes are required for string literals in the `WHERE` clause. 

Select data with a specified value:

```sql
SELECT * 
FROM "h2o_feet" 
WHERE "water_level" >= 9.78
```
Results:

| level description         | location     | time                     | water_level |
| :------------------------ | :----------- | :----------------------- | :---------- |
| at or greater than 9 feet | coyote_creek | 2019-09-01T23:06:00.000Z | 9.8         |
| at or greater than 9 feet | coyote_creek | 2019-09-01T23:12:00.000Z | 9.829       |
| at or greater than 9 feet | coyote_creek | 2019-09-01T23:18:00.000Z | 9.862       |
| at or greater than 9 feet | coyote_creek | 2019-09-01T23:24:00.000Z | 9.892       |
| at or greater than 9 feet | coyote_creek | 2019-09-01T23:30:00.000Z | 9.902       |
| at or greater than 9 feet | coyote_creek | 2019-09-01T23:36:00.000Z | 9.898       |

The query returns data from the measurement h2o_feet with field values of water_level that are greater than or equal to 9.78. Note that this is a partial data set.

Select data with specific tag and field values:

```sql
SELECT * 
FROM "h2o_feet" 
WHERE "location" = 'santa_monica' and "level description" = 'below 3 feet' 
```
Results:

| level description | location     | time                     | water_level |
| :---------------- | :----------- | :----------------------- | :---------- |
| below 3 feet      | santa_monica | 2019-09-01T00:00:00.000Z | 1.529       |
| below 3 feet      | santa_monica | 2019-09-01T00:06:00.000Z | 1.444       |
| below 3 feet      | santa_monica | 2019-09-01T00:12:00.000Z | 1.335       |
| below 3 feet      | santa_monica | 2019-09-01T00:18:00.000Z | 1.345       |
| below 3 feet      | santa_monica | 2019-09-01T00:24:00.000Z | 1.27        |

The query returns all data from the `h2o_feet` measurement with the location tag key `santa_monica` and field value of `level description` that equals the `below 3 feet` string. This is a partial data set.

Select data within a specific time period:

```sql
SELECT *
FROM h2o_feet 
WHERE "location" = 'santa_monica'
AND "time" >= '2019-08-19T12:00:00Z'::timestamp AND "time" <= '2019-08-19T13:00:00Z'::timestamp 
```

Results:
| level description | location     | time                     | water_level |
| :---------------- | :----------- | :----------------------- | :---------- |
| below 3 feet      | santa_monica | 2019-08-19T12:00:00.000Z | 2.533       |
| below 3 feet      | santa_monica | 2019-08-19T12:06:00.000Z | 2.543       |
| below 3 feet      | santa_monica | 2019-08-19T12:12:00.000Z | 2.385       |
| below 3 feet      | santa_monica | 2019-08-19T12:18:00.000Z | 2.362       |
| below 3 feet      | santa_monica | 2019-08-19T12:24:00.000Z | 2.405       |
| below 3 feet      | santa_monica | 2019-08-19T12:30:00.000Z | 2.398       |

The query returns results from a range of greater than or equal to 08-19-2019 at 12 noon and less than or equal to  08-19-2019 at 1:00pm. This is a partial results set.

Select data using the OR operator:

```sql
SELECT *
FROM "h2o_feet"
WHERE "level description" = 'less than 3 feet' OR "water_level" < 2.5
```

Results;
| level description | location     | time                     | water_level |
| :---------------- | :----------- | :----------------------- | :---------- |
| below 3 feet      | coyote_creek | 2019-08-25T10:06:00.000Z | 2.398       |
| below 3 feet      | coyote_creek | 2019-08-25T10:12:00.000Z | 2.234       |
| below 3 feet      | coyote_creek | 2019-08-25T10:18:00.000Z | 2.064       |
| below 3 feet      | coyote_creek | 2019-08-25T10:24:00.000Z | 1.893       |

The query returns a `level dsescription` of less than 3 feet or `water_level` of less than 2.5 feet. This is a partial results set.
