---
layout: post
title: "How to check if a table has a non-clustered index in SQL"
description: " "
date: 2023-09-22
tags: [NonClusteredIndex]
comments: true
share: true
---

```sql
SELECT
    i.name AS IndexName
FROM
    sys.indexes i
INNER JOIN
    sys.tables t ON i.object_id = t.object_id
WHERE
    t.name = 'YourTableName'
    AND i.type_desc = 'NONCLUSTERED'
```

In this query, replace `'YourTableName'` with the actual name of the table you want to check. If the query returns any rows, it means that the table has one or more non-clustered indexes. If it returns no rows, it means that the table does not have any non-clustered indexes.

Keep in mind that this query works for Microsoft SQL Server. If you're using a different database system, the query syntax may vary.

#SQL #NonClusteredIndex