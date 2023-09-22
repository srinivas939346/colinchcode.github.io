---
layout: post
title: "Implementing type 2 slowly changing dimensions."
description: " "
date: 2023-09-22
tags: [datascience, datamodelling]
comments: true
share: true
---

In data warehousing, slowly changing dimensions (SCDs) are used to track and store historical changes in data over time. Type 2 is one of the most common SCD types, where each change to a dimension attribute creates a new entry in the dimension table, preserving the history of the attribute.

In this blog post, we will explore how to implement Type 2 Slowly Changing Dimensions in your data warehouse using an example code in SQL.

## Understanding Type 2 SCD

Type 2 SCDs require two additional columns in the dimension table: **start_date** and **end_date**. 

- The **start_date** represents the beginning of an attribute's validity.
- The **end_date** represents the end of an attribute's validity. If an attribute is still valid, the end_date can be set as '9999-12-31' or any future date.

Here's an example of a dimension table for tracking customer information over time:

```sql
CREATE TABLE customer_dim (
    customer_id INT,
    customer_name VARCHAR(100),
    address VARCHAR(100),
    start_date DATE,
    end_date DATE
);
```
## Implementing Type 2 SCD in SQL

To implement Type 2 SCD, you need to handle two scenarios: inserting new records and updating existing records.

### Inserting New Records

To insert a new record, you need to find the latest end_date for a specific customer_id and set the start_date of the new record accordingly. The end_date for the previous record should be set as the day before the start_date of the new record.

Here's an example of an SQL statement for inserting a new record:

```sql
INSERT INTO customer_dim (customer_id, customer_name, address, start_date, end_date)
SELECT customer_id, 'John Doe', '123 Main St', CURRENT_DATE, '9999-12-31'
FROM (
    SELECT customer_id
    FROM customer_dim
    WHERE customer_id = 1
    ORDER BY start_date DESC
    LIMIT 1
) AS latest_record;
```

### Updating Existing Records

When a customer's attribute changes, you need to update the end_date of the current record and insert a new record with the updated attribute values.

Here's an example of an SQL statement for updating an existing record:

```sql
UPDATE customer_dim
SET end_date = CURRENT_DATE - INTERVAL '1 day'
WHERE customer_id = 1 AND end_date = '9999-12-31';

INSERT INTO customer_dim (customer_id, customer_name, address, start_date, end_date)
VALUES (1, 'John Doe Jr', '456 Elm St', CURRENT_DATE, '9999-12-31');
```

## Conclusion

Implementing Type 2 Slowly Changing Dimensions allows you to track and store historical changes in data, providing valuable insights over time. By understanding the concepts and using the example code provided above, you can effectively implement Type 2 SCDs in your data warehouse.

#datascience #datamodelling