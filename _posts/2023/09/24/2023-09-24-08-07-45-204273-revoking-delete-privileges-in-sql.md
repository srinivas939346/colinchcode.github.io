---
layout: post
title: "Revoking DELETE privileges in SQL"
description: " "
date: 2023-09-24
tags: [DELETE, privileges]
comments: true
share: true
---

In SQL, the `DELETE` statement is used to remove records from a database table. However, there may be situations where you want to restrict or revoke the `DELETE` privileges for certain users or roles. This can be done using the `REVOKE` statement.

### Syntax

The syntax for revoking `DELETE` privileges in SQL is as follows:

```sql
REVOKE DELETE ON table_name FROM user_name;
```

### Example

Let's say we have a table called `employees` and we want to revoke the `DELETE` privilege for a user named `jdoe`. We can do this using the following SQL statement:

```sql
REVOKE DELETE ON employees FROM jdoe;
```

After executing this statement, the user `jdoe` will no longer have the permission to delete records from the `employees` table.

### Revoke Privileges from All Users

If you want to revoke the `DELETE` privilege from all users, you can use the `PUBLIC` keyword instead of specifying a specific user. The `PUBLIC` keyword represents all users or roles in the database.

```sql
REVOKE DELETE ON employees FROM PUBLIC;
```

This statement will remove the `DELETE` privilege from all users for the `employees` table.

### Conclusion

By using the `REVOKE` statement in SQL, you can easily revoke the `DELETE` privilege from specific users or roles, or from all users at once. This provides an added layer of security and control over your database operations.

#SQL #DELETE #privileges