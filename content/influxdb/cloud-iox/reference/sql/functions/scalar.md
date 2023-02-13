---
title: SQL scalar functions
list_title: Scalarfunctions
description: >
  Use SQL scalar functions.
menu:
  influxdb_cloud_iox:
    name: Scalar
    parent: sql-functions
weight: 310

---

## Conditional functions


Conditional functions 


### coalesce



SELECT *,
coalesce ('water_level', 0)
from h2o_feet


below 3 feet	santa_monica	2019-08-27T09:18:00.000Z	0

### nulllif

Returns a null value if value1 equals value2; otherwise it returns value1. 

```sql
NULLIF(argument_1,argument_2);
```

```sql
SELECT *,
nullif ('level description', 'none')
from h2o_feet
```

| level description    | location     | time                 | water_level | nullif            |
| :------------------- | :----------- | :------------------- | :---------- | :---------------- |
| between 3 and 6 feet | coyote_creek | 2019-09-06T00:00:00Z | 5.938       | level description |
| between 6 and 9 feet | coyote_creek | 2019-09-06T00:06:00Z | 6.112       | level description |
| between 6 and 9 feet | coyote_creek | 2019-09-06T00:12:00Z | 6.283       | level description |
| between 6 and 9 feet | coyote_creek | 2019-09-06T00:18:00Z | 6.434       | none              |