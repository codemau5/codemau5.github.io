---
layout: post
title: Postgresql trick
---

## Postgresql insert returning with row number ##

```sql

WITH insert_xyz_inner AS (
INSERT INTO xyz ("data")
  SELECT params.data
  FROM params
RETURNING xyz."id"
),
insert_xyz AS (
  SELECT
    id,
    row_number() OVER () AS rownum
  FROM insert_xyz_inner
)

...

```
