---
title: SQL hash functions
list_title: Hash functions
description: >
  Use hash functions to perform mathematical operations in SQL queries.
menu:
  influxdb_cloud_iox:
    name: Hash
    parent: sql-functions    
weight: 309
---

The InfluxDB SQL implementation supports the following hash functions for
generating secure hashes:

- [sha224](#sha224)
- [sha256](#sha256)
- [sha384](#sha384)
- [sha512](#sha512)

## sha224

```sql
sha224(expression)
```
##### Arguments

- **expression**: Column or literal value to operate on.

{{< expand-wrapper >}}
{{% expand "View `sha224` query example" %}}

{{% /expand %}}
{{< /expand-wrapper >}}

## sha256

```sql
sha256(expression)
```
##### Arguments

- **expression**: Column or literal value to operate on.

{{< expand-wrapper >}}
{{% expand "View `sha256` query example" %}}

{{% /expand %}}
{{< /expand-wrapper >}}

## sha384

```sql
sha384(expression)
```
##### Arguments

- **expression**: Column or literal value to operate on.

{{< expand-wrapper >}}
{{% expand "View `sha384` query example" %}}

{{% /expand %}}
{{< /expand-wrapper >}}

## sha512

```sql
sha512(expression)
```
##### Arguments

- **expression**: Column or literal value to operate on.

{{< expand-wrapper >}}
{{% expand "View `sha512` query example" %}}

{{% /expand %}}
{{< /expand-wrapper >}}
