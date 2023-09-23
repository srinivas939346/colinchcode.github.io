---
layout: post
title: "SQL SELECT string functions"
description: " "
date: 2023-09-23
tags: [stringfunctions]
comments: true
share: true
---

In this blog post, we will explore some commonly used string functions in SQL's SELECT statement. These functions allow you to manipulate and perform operations on string data types within the SELECT query.

## 1. CONCAT

The `CONCAT` function is used to concatenate two or more strings together. It takes the form `CONCAT(string1, string2, ...)`, where `string1` and `string2` are the strings to be concatenated.

```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM users;
```

In the example above, the `CONCAT` function is used to concatenate the `first_name` and `last_name` columns, separated by a space. The result will be displayed as the `full_name` column.

## 2. SUBSTRING

The `SUBSTRING` function is used to extract a portion of a string. It takes the form `SUBSTRING(string, start_position, length)`, where `string` is the source string, `start_position` is the starting index of the substring, and `length` is the number of characters to include.

```sql
SELECT SUBSTRING(email, 1, 5) AS username
FROM users;
```

In the example above, the `SUBSTRING` function is used to extract the first 5 characters from the `email` column. The result will be displayed as the `username` column.

## 3. UPPER and LOWER

The `UPPER` and `LOWER` functions are used to convert a string to uppercase and lowercase, respectively. They take the form `UPPER(string)` and `LOWER(string)`, where `string` is the source string.

```sql
SELECT UPPER(username) AS uppercase_username, LOWER(email) AS lowercase_email
FROM users;
```

In the example above, the `UPPER` function is used to convert the `username` column to uppercase, and the `LOWER` function is used to convert the `email` column to lowercase. The results will be displayed as the `uppercase_username` and `lowercase_email` columns.

## Conclusion

In this blog post, we have explored some commonly used string functions in SQL's SELECT statement. The `CONCAT` function allows us to concatenate strings, the `SUBSTRING` function allows us to extract substrings, and the `UPPER` and `LOWER` functions allow us to convert strings to uppercase and lowercase, respectively. These functions are useful for manipulating and working with string data in SQL queries.

#SQL #stringfunctions