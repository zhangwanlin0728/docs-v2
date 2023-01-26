---
title: The JOIN clause
list_title: The JOIN clause
description: > 
    Use the `JOIN` clause to combine the results of two or more SELECT statements without returing any duplicate rows.
menu:
  influxdb_cloud_iox:
    name: The JOIN clause
    parent: Explore data using SQL
weight: 290
---

The `JOIN` clause combines rows from two or more tables in a database using common values. In other words, a `JOIN` allows you to pull data from multiple measurements into one results set.  InfluxDB's SQL implementation curently supports INNER JOIN, LEFT JOIN (LEFT OUTER JOIN), RIGHT JOIN (RIGHT OUTER JOIN) and FULL OUTER JOIN.

{{< flex >}}
{{< flex-content "quarter" >}}
  <p style="text-align:center"><strong>Inner join</strong></p>
  {{< svg svg="static/svgs/join-diagram.svg" class="inner small center" >}}
{{< /flex-content >}}
{{< flex-content "quarter" >}}
  <p style="text-align:center"><strong>Left outer join</strong></p>
  {{< svg svg="static/svgs/join-diagram.svg" class="left small center" >}}
{{< /flex-content >}}
{{< flex-content "quarter" >}}
  <p style="text-align:center"><strong>Right outer join</strong></p>
  {{< svg svg="static/svgs/join-diagram.svg" class="right small center" >}}
{{< /flex-content >}}
{{< flex-content "quarter" >}}
  <p style="text-align:center"><strong>Full outer join</strong></p>
  {{< svg svg="static/svgs/join-diagram.svg" class="full small center" >}}
{{< /flex-content >}}
{{< /flex >}}

## INNER JOIN

An INNER JOIN is one of the most common join types.  The INNER JOIN clause gathers data where there is a match between the two measurements being joined. The results only show rows where there is match in **both tables**.

To join measurements using INNER JOIN, do the following:

1. Specify the column or columns from both measurements that you want in the `SELECT`clause.  You can also use `SELECT *`.
2. Specify the first measurement in the `FROM` clause.
3. Specify the second measurement in the `INNER JOIN` clause.
4. Use the ``ON` keyword to specify exactly how the two measurments are to be joined.  

```sql
SELECT tag1, tag2
FROM measurementA
INNER JOIN measurementB.tag1
ON measurementA.tag1 = measurementB.tag1 AND measurementA.tag2 = measurementB.tag2
```

#### Examples

Use `INNER JOIN` with the `SELELCT *` statement:

```sql
SELECT *
FROM h2o_feet
INNER JOIN h2o_temperature
ON h2o_feet.location = h2o_temperature.location AND h2o_feet.time = h2o_temperature.time
```

Results:

| degrees | level description    | location     | time                     | water_level |
| :------ | :------------------- | :----------- | :----------------------- | :---------- |
| 67      | between 6 and 9 feet | coyote_creek | 2019-08-20T00:06:00.000Z | 8.658       |
| 63      | between 6 and 9 feet | coyote_creek | 2019-08-20T00:18:00.000Z | 8.684       |
| 66      | between 6 and 9 feet | coyote_creek | 2019-08-20T00:36:00.000Z | 8.61        |
| 62      | between 6 and 9 feet | coyote_creek | 2019-08-20T01:12:00.000Z | 8.258       |
| 68      | between 6 and 9 feet | coyote_creek | 2019-08-20T01:36:00.000Z | 7.858       |
| 64      | between 6 and 9 feet | coyote_creek | 2019-08-20T02:18:00.000Z | 7.054       |


The query returns data from all tags and fields from h2o_feet and h2o_measurement where time `time` and `location` match. Note that this is only a partial data set. The number of rows returned is 7,604.





## LEFT OUTER JOIN

The keywords LEFT JOIN or LEFT OUTER JOIN define a join that includes all rows from the left table even if there is not a match in the right table. When there is no match, null values are produced for the right side of the join.

## RIGHT OUTER JOIN

The keywords RIGHT JOIN or RIGHT OUTER JOIN define a join that includes all rows from the right table even if there is not a match in the left table. When there is no match, null values are produced for the left side of the join.

## FULL OUTER JOIN

The keywords FULL JOIN or FULL OUTER JOIN define a join that is effectively a union of a LEFT OUTER JOIN and RIGHT OUTER JOIN. It will show all rows from the left and right side of the join and will produce null values on either side of the join where there is not a match.


