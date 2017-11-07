---
layout: post
title: Postgresql optimization trick
---

## Postgresql condition both tables of join ##

if we apply the range on the time block itself aswell,
we can use the index on "time_block" table aswell,
and join less rows,
making the query 1/5th of the time

```sql

SELECT *
FROM
  "time_block"
  JOIN "sub_time_block"
    ON ("sub_time_block"."father" = "time_block"."id")
    
WHERE "time_block"."endTime" >= $START_OF_SEARCH_RANGE
  AND "time_block"."startTime" <= $END_OF_SEARCH_RANGE

  AND "sub_time_block"."endTime" >= $START_OF_SEARCH_RANGE
  AND "sub_time_block"."startTime" <= $END_OF_SEARCH_RANGE

```
