---
title: SQL approximate functions
list_title: Approximate functions
description: >
  Approximate data with SQL approximate functions.
menu:
  influxdb_cloud_iox:
    name: Approximate
    parent: SQL functions
weight: 250
---

Approximate Functions

approx_distinct -  uint64 returns the approximate number (HyperLogLog) of distinct input values

approx_median -  x returns the approximate median of input values. it is an alias of approx_percentile_cont(x, 0.5).

approx_percentile_cont
approx_percentile_cont(x, p) -> x return the approximate percentile (TDigest) of input values, where p is a float64 between 0 and 1 (inclusive).

It supports raw data as input and build Tdigest sketches during query time, and is approximately equal to approx_percentile_cont_with_weight(x, 1, p).

approx_percentile_cont(x, p, n) -> x return the approximate percentile (TDigest) of input values, where p is a float64 between 0 and 1 (inclusive),

and n (default 100) is the number of centroids in Tdigest which means that if there are n or fewer unique values in x, you can expect an exact result.

A higher value of n results in a more accurate approximation and the cost of higher memory usage.

approx_percentile_cont_with_weight
approx_percentile_cont_with_weight(x, w, p) -> x returns the approximate percentile (TDigest) of input values with weight, where w is weight column expression and p is a float64 between 0 and 1 (inclusive).

It supports raw data as input or pre-aggregated TDigest sketches, then builds or merges Tdigest sketches during query time. TDigest sketches are a list of centroid (x, w), where x stands for mean and w stands for weight.

It is suitable for low latency OLAP system where a streaming compute engine (e.g. Spark Streaming/Flink) pre-aggregates data to a data store, then queries using Datafusion.





### The APPROX_MEDIAN function

```sql
SELECT approx_median("pH")
FROM "h2o_pH"
```


### The APPROX_PERCENTILE_CONT function

doesn't work
SELECT APPROX_PERCENTILE_CONT("pH"), time
FROM "h2o_pH"
GROU BY time

