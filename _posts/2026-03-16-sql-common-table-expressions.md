---
title: Common Table Expressions in SQL
date:  2026-03-16 22:00:00 +0800
categories: [Knowledge, SQL]
tags: [sql, mysql, documentation, knowledge]     # TAG names should always be lowercase
description: A guide on creating common table expressions in SQL.
---

A Common Table Expression (CTE) is a temporary, named result set that you can reference within a single SQL statement, and can be referenced within a "SELECT", "INSERT", "UPDATE", or "DELETE" statement.

CTEs help to simplify complex query and can be reused multiple times within the same query.

## Query
```sql
WITH temp_table AS (
  SELECT
    DISTINCT *,
    SUM(CASE WHEN rating < 3 THEN 1 ELSE 0 END) AS poor_rating
  FROM Queries
  GROUP BY query_name
)

SELECT 
  q.query_name,
  ROUND(AVG(q.rating/q.position), 2) AS quality,
  ROUND((t.poor_rating/count(q.query_name) * 100), 2) AS poor_query_percentage
FROM Queries as q
LEFT JOIN temp_table as t
ON q.query_name = t.query_name
GROUP BY query_name
```
