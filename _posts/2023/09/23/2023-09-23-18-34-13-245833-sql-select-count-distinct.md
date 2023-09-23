---
layout: post
title: "SQL SELECT count distinct"
description: " "
date: 2023-09-23
tags: [CountDistinct]
comments: true
share: true
---

```sql
SELECT COUNT(DISTINCT column_name) AS distinct_count
FROM table_name;
```

In the above code snippet, replace `column_name` with the name of the column you want to count the distinct values for, and `table_name` with the actual name of the table you are working on.

For example, let's say you have a table called `users` with a column named `country`, and you want to count the number of unique countries in that column. Here's how you can write the query:

```sql
SELECT COUNT(DISTINCT country) AS distinct_country_count
FROM users;
```

The result of this query will be a single row with a column named `distinct_country_count` that contains the count of distinct countries in the `country` column.

Using the `COUNT(DISTINCT column_name)` statement can be helpful when you need to analyze data with unique values in SQL, such as finding the number of unique customers, products, or any other attribute in your dataset.

By using this SQL statement, you can easily obtain the count of distinct values without the need for any additional processing or programming logic.

#SQL #CountDistinct