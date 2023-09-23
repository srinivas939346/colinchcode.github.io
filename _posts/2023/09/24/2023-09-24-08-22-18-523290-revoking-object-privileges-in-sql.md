---
layout: post
title: "Revoking object privileges in SQL"
description: " "
date: 2023-09-24
tags: [Database, Privileges]
comments: true
share: true
---

When working with databases, controlling access to various database objects is essential to ensure data security and privacy. In SQL, object privileges grant or revoke permissions to perform specific operations on database objects, such as tables, views, or procedures.

In this blog post, we will explore how to revoke object privileges in SQL, allowing us to remove previously granted permissions.

## Revoke Privileges Syntax

The **REVOKE** statement is used to revoke object privileges from users or roles. The basic syntax for revoking privileges is as follows:

```
REVOKE privilege_type
ON object_name
FROM user_or_role;
```

- **privilege_type**: Specifies the privilege or privileges to be revoked. It can be a single privilege or a comma-separated list of privileges.
- **object_name**: Refers to the name of the object from which the privilege will be revoked.
- **user_or_role**: Specifies the user or role from which the privilege will be revoked.

### Example Usage

Let's consider a scenario where we have granted the **SELECT** privilege on a table called `employees` to a user named `johndoe`. To revoke this privilege, the following SQL statement can be used:

```sql
REVOKE SELECT
ON employees
FROM johndoe;
```

In the above example, we are revoking the **SELECT** privilege on the `employees` table from the user `johndoe`.

### Revoking Multiple Privileges

You can also revoke multiple privileges at once by providing a comma-separated list of privilege types. For example:

```sql
REVOKE SELECT, INSERT, UPDATE
ON employees
FROM johndoe;
```

In the above example, we are revoking the **SELECT**, **INSERT**, and **UPDATE** privileges on the `employees` table from the user `johndoe`.

### Revoking Privileges from All Users

If you want to revoke privileges from all users, you can use the **PUBLIC** keyword instead of specifying individual user names. For example:

```sql
REVOKE SELECT
ON employees
FROM PUBLIC;
```

In the above example, we are revoking the **SELECT** privilege on the `employees` table from all users.

## Conclusion

Revoking object privileges in SQL is an important aspect of database security. By using the **REVOKE** statement, you can selectively remove privileges from users or roles, ensuring that access to database objects is granted only to authorized entities.

Remember to always review and manage object privileges regularly to maintain tight control over who can perform operations on your database objects.

#SQL #Database #Privileges #Security