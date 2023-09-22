---
layout: post
title: "Handling type 3 slowly changing dimensions in SQL."
description: " "
date: 2023-09-22
tags: [datawarehousing]
comments: true
share: true
---

Slowly Changing Dimensions (SCD) are a common challenge in data warehousing and database management. SCDs refer to dimensions that change over time, requiring careful handling to maintain the integrity and accuracy of the data.

There are different types of SCDs, with Type 3 being one of the most commonly used. Type 3 SCDs keep a limited history of changes by storing only the most recent value and the original value. This is useful when you need to track some changes but don't require a complete historical record.

In this blog post, we will explore how to handle Type 3 SCDs in SQL. Let's dive in!

## 1. Identifying Type 3 SCD Columns
To handle Type 3 SCDs, you first need to identify the columns that require tracking changes. These columns are typically the ones that are subject to updates.

For example, let's consider a table called `customers` with the following columns:

```sql
CREATE TABLE customers (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    email VARCHAR(100),
    status VARCHAR(10),
    last_updated DATETIME
);
```

In this case, the `status` column could be a Type 3 SCD column. We want to track its changes while keeping a limited history.

## 2. Adding Additional Columns
To handle Type 3 SCDs, you'll need to add additional columns to the table. These columns will store the original and most recent values.

In our example, we can add two columns: `status_original` and `status_latest`:

```sql
ALTER TABLE customers ADD COLUMN status_original VARCHAR(10);
ALTER TABLE customers ADD COLUMN status_latest VARCHAR(10);
```

Now we have the necessary columns to track changes.

## 3. Updating the Table
Whenever a change in the SCD column occurs, we need to update both the `status_latest` and `last_updated` columns, as well as preserve the original value in the `status_original` column.

```sql
UPDATE customers
SET status_original = status_latest,
    status_latest = 'NEW_STATUS',
    last_updated = now()
WHERE id = 1;
```

In this example, we're updating the `status_latest` column to a new value ('NEW_STATUS'), preserving the original value in `status_original`, and updating the `last_updated` column with the current date and time. The WHERE clause restricts the update to a specific row.

## 4. Querying the Changes
To analyze the changes in Type 3 SCDs, you can write queries that compare the original and latest values.

```sql
SELECT id, name, status_original, status_latest, last_updated
FROM customers
WHERE id = 1;
```

This query retrieves the original and latest values of the `status` column for a specific customer.

## Conclusion

Handling Type 3 Slowly Changing Dimensions in SQL requires the identification of SCD columns, the addition of additional columns to store original and latest values, and proper update and query operations. By following these steps, you can effectively track and manage changes in your SCDs.

#datawarehousing #SQL