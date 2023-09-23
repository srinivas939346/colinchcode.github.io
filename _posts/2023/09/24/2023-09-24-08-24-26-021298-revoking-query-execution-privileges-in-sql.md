---
layout: post
title: "Revoking query execution privileges in SQL"
description: " "
date: 2023-09-24
tags: [DatabaseSecurity]
comments: true
share: true
---

In SQL, query execution privileges grant users the ability to retrieve data from a database. However, there may be situations where you want to revoke or remove these privileges from certain users or roles. This can be useful for security purposes or to limit access to sensitive information. In this blog post, we will discuss how to revoke query execution privileges in SQL.

## Syntax

The syntax to revoke query execution privileges in SQL varies slightly depending on the database management system (DBMS) you are using. We will cover the most common syntax for popular DBMSs.

### PostgreSQL

To revoke query execution privileges in PostgreSQL, you can use the `REVOKE` statement with the `SELECT` privilege. The syntax is as follows:

```sql
REVOKE SELECT ON table_name FROM user_or_role;
```

Here, `table_name` refers to the name of the table from which you want to revoke the `SELECT` privilege, and `user_or_role` specifies the user or role to which you want to revoke the privilege.

### MySQL/MariaDB

In MySQL and MariaDB, you can use the `REVOKE` statement with the `SELECT` privilege to revoke query execution privileges. The syntax is as follows:

```sql
REVOKE SELECT ON database_name.table_name FROM user_or_role;
```

In this syntax, `database_name` specifies the name of the database containing the table, `table_name` is the name of the table from which you want to revoke the privilege, and `user_or_role` denotes the user or role to which you want to revoke the privilege. 

### Oracle

In Oracle, you can use the `REVOKE` statement with the `SELECT` privilege to revoke query execution privileges. The syntax is as follows:

```sql
REVOKE SELECT ON schema_name.table_name FROM user_or_role;
```

In this syntax, `schema_name` denotes the name of the schema containing the table, `table_name` is the name of the table from which you want to revoke the privilege, and `user_or_role` specifies the user or role to which you want to revoke the privilege.

## Example

Let's say we have a PostgreSQL database with a table called `employees` and we want to revoke query execution privileges from a user named `john`. We can use the following command to achieve this:

```sql
REVOKE SELECT ON employees FROM john;
```

This command will remove the `SELECT` privilege from the `employees` table for the user `john`.

## Conclusion

Revoking query execution privileges in SQL is an essential aspect of database security. By understanding the syntax for revoking privileges in different DBMSs, you can effectively control access to data and ensure the confidentiality of sensitive information.

#SQL #DatabaseSecurity