---
layout: post
title: "Revoking system privileges in SQL"
description: " "
date: 2023-09-24
tags: [DatabaseSecurity]
comments: true
share: true
---

In SQL, system privileges grant access to perform certain actions on the overall database or the underlying system. However, there may be situations where you need to revoke these privileges from a user or role. Revoking system privileges ensures that users or roles no longer have permission to perform specific actions.

To revoke system privileges in SQL, you can use the `REVOKE` statement followed by the privilege and the object on which the privilege is granted.

Here's the syntax for revoking system privileges in SQL:

```sql
REVOKE privilege_name [, privilege_name ...]
ON object_name
FROM user_name [, user_name ...] | role_name [, role_name ...]
```

Let's break down the different elements in the syntax:

1. `REVOKE` - The keyword that starts the revoke statement.
2. `privilege_name` - The name of the system privilege(s) you want to revoke.
3. `ON object_name` - The name of the object (e.g., table, view, or schema) on which the privilege is granted.
4. `FROM user_name [, user_name ...] | role_name [, role_name ...]` - The user(s) or role(s) from which you want to revoke the privilege(s).

Now, let's see a few examples of revoking system privileges in SQL.

## Example 1: Revoking a Single System Privilege

Suppose you have granted the `CREATE TABLE` privilege to a user named `john_doe` and want to revoke it. You can use the following SQL statement:

```sql
REVOKE CREATE TABLE
ON schema_name.table_name
FROM john_doe;
```

This statement revokes the `CREATE TABLE` privilege on the specified table from the user `john_doe`.

## Example 2: Revoking Multiple System Privileges

If you want to revoke multiple system privileges simultaneously, you can list them separated by commas. For example, if you want to revoke both the `SELECT` and `INSERT` privileges on a table from a user named `jane_smith`, you can use the following SQL statement:

```sql
REVOKE SELECT, INSERT
ON schema_name.table_name
FROM jane_smith;
```

This statement revokes both the `SELECT` and `INSERT` privileges on the specified table from the user `jane_smith`.

## Conclusion

Revoking system privileges in SQL allows you to restrict or remove certain actions from users or roles. By using the `REVOKE` statement, you can revoke system privileges from specific objects and users/roles, thereby enhancing the security and control of your database.

#SQL #DatabaseSecurity