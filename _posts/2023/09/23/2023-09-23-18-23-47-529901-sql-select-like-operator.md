---
layout: post
title: "SQL SELECT like operator"
description: " "
date: 2023-09-23
tags: [techblog]
comments: true
share: true
---

When working with SQL databases, the `LIKE` operator is a powerful tool for pattern matching in queries. It allows you to search for a specified pattern within a column's value. Here's how you can use the `LIKE` operator in your SQL `SELECT` statements.

## Syntax

The syntax for using the `LIKE` operator in a `SELECT` statement is as follows:

```sql
SELECT column_name(s) FROM table_name WHERE column_name LIKE pattern;
```

- `column_name(s)`: The name(s) of the column(s) you want to retrieve from the table.
- `table_name`: The name of the table you want to perform the query on.
- `column_name`: The specific column you want to search for the pattern.
- `pattern`: The pattern you want to match against the column's values.

## Examples

Let's explore some examples to understand how the `LIKE` operator works.

1. Retrieve all records where the `name` column starts with "John":

```sql
SELECT * FROM employees WHERE name LIKE 'John%';
```

2. Retrieve all records where the `email` column contains the domain "gmail.com":

```sql
SELECT * FROM users WHERE email LIKE '%gmail.com%';
```

3. Retrieve all records where the `phone_number` column ends with "123":

```sql
SELECT * FROM contacts WHERE phone_number LIKE '%123';
```

## Wildcards

The `LIKE` operator supports the following wildcards for pattern matching:

- `%`: Matches any sequence of characters (including zero characters).
- `_`: Matches any single character.

Here are a few examples to demonstrate the use of wildcards:

- `LIKE 'J%'`: Matches any value that starts with "J".
- `LIKE '%on'`: Matches any value that ends with "on".
- `LIKE '_o%'`: Matches any value with "o" as the second character.

## Conclusion

The `LIKE` operator in SQL is a useful tool for performing pattern matching queries. By using wildcards, you can search for specific patterns within column values. Understanding how to use the `LIKE` operator will enhance your ability to retrieve relevant data from your SQL databases efficiently.

#techblog #sql