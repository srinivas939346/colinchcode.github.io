---
layout: post
title: "Revoking privileges on columns in SQL"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

When granting user privileges in a relational database management system (RDBMS) like SQL, it is important to have control over what actions different users can perform. Sometimes, you may need to restrict user access to specific columns within a table while still allowing them to have access to other columns or perform other operations.

In SQL, you can revoke privileges on specific columns using the **REVOKE** statement. This allows you to fine-tune user permissions and control exactly what columns they can read or modify. Let's explore how to do this.

## Syntax for Revoking Column Privileges

The syntax for revoking privileges on columns in SQL is as follows:

```sql
REVOKE privilege_name(column_name)
ON table_name
FROM user_name;
```

Here, `privilege_name` can be any of the following:

- **SELECT**: revokes the user's permission to read values from the specified column.
- **UPDATE**: revokes the user's permission to modify values in the specified column.
- **INSERT**: revokes the user's permission to insert values into the specified column.

`column_name` refers to the name of the column you want to revoke privileges on. `table_name` is the name of the table where the column belongs, and `user_name` is the name of the user or role you want to revoke the privileges from.

## Examples

Let's look at some examples to better understand how to revoke privileges on columns.

### Revoke SELECT Privilege on a Column

Suppose we have a table called `employees` with columns `id`, `name`, `email`, and `salary`. If we want to revoke the `SELECT` privilege on the `salary` column for a user named `finance_user`, we can run the following SQL command:

```sql
REVOKE SELECT(salary)
ON employees
FROM finance_user;
```

This prevents `finance_user` from viewing the salary column while still allowing them to access other columns.

### Revoke UPDATE Privilege on a Column

To revoke the `UPDATE` privilege on the `email` column for the user `manager_user`, we can use the following statement:

```sql
REVOKE UPDATE(email)
ON employees
FROM manager_user;
```

Without the `UPDATE` privilege on the `email` column, `manager_user` won't be able to modify the values in that column but can still perform updates on other columns.

### Revoke INSERT Privilege on a Column

If we want to revoke the `INSERT` privilege on the `name` column for the user `user1`, we can execute the following SQL command:

```sql
REVOKE INSERT(name)
ON employees
FROM user1;
```

This will prevent `user1` from inserting values into the `name` column while still allowing them to perform insertions on other columns.

## Conclusion

Revoking privileges on columns in SQL provides a way to control user access and restrict their actions on specific columns within a table. By using the `REVOKE` statement and specifying the column, table, and user, you can finely tailor the level of access granted to individual users.