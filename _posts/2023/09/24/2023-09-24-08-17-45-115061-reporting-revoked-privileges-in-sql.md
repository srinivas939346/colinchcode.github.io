---
layout: post
title: "Reporting revoked privileges in SQL"
description: " "
date: 2023-09-24
tags: [database, security]
comments: true
share: true
---

When managing a database, it is crucial to ensure that users have the appropriate privileges to perform their tasks. However, there may be instances where privileges need to be revoked or modified. In such cases, it is essential to report on revoked privileges to maintain data security and compliance. In this article, we will explore how to report revoked privileges in SQL.

## Retrieving revoked privileges information

To report on revoked privileges, we can query the system tables in the SQL database. Here's an example of how to retrieve revoked privileges information in a SQL Server database:

```sql
SELECT
    USER_NAME(p.grantee_principal_id) AS [User],
    p.class_desc AS [Object Type],
    OBJECT_NAME(p.major_id) AS [Object Name],
    p.permission_name AS [Permission],
    p.state_desc AS [State]
FROM
    sys.database_permissions p
WHERE
    p.state_desc = 'REVOKE'
ORDER BY
    [User], [Object Name], [Permission]
```

This query retrieves revoked privileges details from the `sys.database_permissions` system table. It filters only the entries with a state of 'REVOKE'. The result includes columns for the user, object type, object name, permission, and state.

## Customizing the query

The query above can be customized to suit specific requirements. Here are a few modifications you might consider:

### Filtering by object type or name

If you only want to retrieve revoked privileges for a specific object type or name, you can add a `WHERE` clause to filter the results. For example, to retrieve revoked privileges for tables only, you can add the following condition:

```sql
WHERE
    p.class_desc = 'OBJECT_OR_COLUMN'
    AND OBJECT_NAME(p.major_id) = 'table_name'
```

Replace `'table_name'` with the name of the table you want to filter on.

### Expanding the result set

If you need additional details, such as the grantor or the date the privileges were revoked, you can include additional columns in the `SELECT` statement. You can explore other system tables like `sys.database_principals` or `sys.database_permissions` to gather more information.

## Conclusion

Reporting on revoked privileges is an important aspect of maintaining database security and compliance. By querying the appropriate system tables in SQL, you can retrieve detailed information about revoked privileges. This enables administrators to identify and address any security gaps effectively.

#SQL #database #security #privileges #revoked