---
layout: post
title: "Revoking privileges on multiple tables in SQL"
description: " "
date: 2023-09-24
tags: [Database]
comments: true
share: true
---

In SQL, privileges can be granted or revoked to users or roles to control access to tables. There may be situations where you need to revoke privileges on multiple tables at once. In this blog post, we will explore different methods to accomplish this task efficiently.

## Method 1: Revoke Privileges Individually

The first method involves revoking privileges on each table individually. This method is suitable when you have a small number of tables to revoke privileges from. Here's an example of how you can use the `REVOKE` statement in SQL to revoke privileges on multiple tables:

```sql
REVOKE SELECT, INSERT, UPDATE, DELETE ON table1 FROM user1;
REVOKE SELECT, INSERT, UPDATE, DELETE ON table2 FROM user1;
REVOKE SELECT, INSERT, UPDATE, DELETE ON table3 FROM user1;
```

In this example, we are revoking the `SELECT`, `INSERT`, `UPDATE`, and `DELETE` privileges on `table1`, `table2`, and `table3` from `user1`.

## Method 2: Revoke Privileges Using Wildcards

If you have a large number of tables to revoke privileges from, using wildcards can save you time and effort. Wildcards allow you to revoke privileges on multiple tables that match a specific pattern. Here's an example:

```sql
REVOKE SELECT, INSERT, UPDATE, DELETE ON tables_prefix% FROM user1;
```

In this example, we are revoking the same privileges on all tables that have a prefix of "tables_prefix". The '%' symbol acts as a wildcard, matching any characters after the specified prefix.

## Method 3: Revoke Privileges Using a Loop

If you have a dynamic list of tables or a specific condition to revoke privileges, you can use a loop to iterate over the tables and revoke privileges on each one. This method requires stored procedures or other programming constructs available in your SQL database.

Here's an example using a loop in MySQL:

```sql
DELIMITER //
CREATE PROCEDURE revoke_privileges()
BEGIN
    DECLARE table_name VARCHAR(100);
    DECLARE done INT DEFAULT 0;
    
    DECLARE cur CURSOR FOR SELECT table_name FROM information_schema.tables WHERE table_schema = 'your_database_name';
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = 1;
    
    OPEN cur;
    
    read_loop: LOOP
        FETCH cur INTO table_name;
        
        IF done = 1 THEN
            LEAVE read_loop;
        END IF;
        
        SET @sql = CONCAT('REVOKE SELECT, INSERT, UPDATE, DELETE ON ', table_name, ' FROM user1');
        PREPARE stmt FROM @sql;
        EXECUTE stmt;
        DEALLOCATE PREPARE stmt;
    END LOOP;
    
    CLOSE cur;
END //
DELIMITER ;

CALL revoke_privileges();
```

In this example, we create a stored procedure called `revoke_privileges` that uses a cursor to iterate over the tables in the specified database. We revoke the required privileges on each table using dynamic SQL.

## Conclusion

Revoking privileges on multiple tables in SQL can be done using different methods. The choice of method depends on the number of tables and the level of flexibility required. Whether you revoke privileges individually, use wildcards, or create a loop, it's important to regularly review and manage the access privileges in your database to ensure proper data security.

#SQL #Database