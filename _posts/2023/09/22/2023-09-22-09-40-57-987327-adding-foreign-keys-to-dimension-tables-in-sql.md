---
layout: post
title: "Adding foreign keys to dimension tables in SQL."
description: " "
date: 2023-09-22
tags: [Database]
comments: true
share: true
---

When designing a database, it is important to establish relationships between the tables to ensure data integrity and consistency. In SQL, one way to establish relationships is by using foreign keys.

Foreign keys provide a way to link a column in one table to the primary key of another table. This is particularly useful in dimension tables, which are used to store descriptive information about the data in a fact table. By adding foreign keys to dimension tables, we can enforce referential integrity and make it easier to join and analyze the data.

Here's an example of how to add foreign keys to dimension tables in SQL:

## Step 1: Create the dimension tables

First, we need to create the dimension tables. These tables will hold the descriptive information that will be referenced by the fact table.

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100),
    customer_address VARCHAR(200)
);

CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    product_category VARCHAR(50)
);
```

## Step 2: Add foreign keys to the dimension tables

Next, we will add foreign keys to the dimension tables to establish the relationships.

```sql
ALTER TABLE fact_table
ADD CONSTRAINT fk_customer_id
FOREIGN KEY (customer_id) REFERENCES customers(customer_id);

ALTER TABLE fact_table
ADD CONSTRAINT fk_product_id
FOREIGN KEY (product_id) REFERENCES products(product_id);
```

In this example, the `fact_table` is the table that holds the actual data, and we are adding foreign keys to the `customer_id` and `product_id` columns, referencing the corresponding columns in the `customers` and `products` tables, respectively.

## Step 3: Verify the foreign key constraints

After adding the foreign keys, it is important to verify the constraints to ensure they are working correctly. This can be done by attempting to insert or update data that violates the foreign key relationships. If the constraints are set up correctly, the database will reject such operations.

## Conclusion

Adding foreign keys to dimension tables in SQL allows us to establish relationships between tables, enforce referential integrity, and simplify data analysis. By linking the dimension tables to the fact table using foreign keys, we can create a well-structured database that ensures the accuracy and consistency of our data.

#SQL #Database