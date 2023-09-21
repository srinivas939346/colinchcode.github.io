---
layout: post
title: "Automating tablespace maintenance tasks with SQL scripts and jobs"
description: " "
date: 2023-09-21
tags: [automation]
comments: true
share: true
---

One common task is to defragment tablespaces, which involves reorganizing the data and indexes to optimize storage and retrieval. To automate this task, we can create a SQL script that generates the necessary statements to defragment the tablespaces. Here's an example of how the script may look like in PL/SQL:

```sql
DECLARE
  tablespace_name VARCHAR2(30);
BEGIN
  FOR ts IN (SELECT tablespace_name FROM dba_tablespaces) LOOP
    tablespace_name := ts.tablespace_name;
  
    EXECUTE IMMEDIATE 'ALTER TABLESPACE ' || tablespace_name || ' COALESCE';
    EXECUTE IMMEDIATE 'ALTER TABLESPACE ' || tablespace_name || ' SHRINK SPACE CASCADE';
    EXECUTE IMMEDIATE 'ALTER TABLESPACE ' || tablespace_name || ' MODIFY DEFAULT ATTRIBUTES (PCTFREE 10)';
  END LOOP;
END;
/
```

This script retrieves the list of tablespaces from the data dictionary and then issues the necessary `ALTER TABLESPACE` commands to defragment each tablespace. The `COALESCE` command helps to merge fragmented free space within the tablespace, while the `SHRINK SPACE` command reclaims unused space.

To automate the execution of this script, we can create a scheduled job in the database. Here's an example of how to create the job using the `DBMS_SCHEDULER` package:

```sql
BEGIN
  DBMS_SCHEDULER.CREATE_JOB (
    job_name             => 'DEFRAG_TABLESPACES_JOB',
    job_type             => 'PLSQL_BLOCK',
    job_action           => 'BEGIN ... END;',
    start_date           => SYSDATE,
    repeat_interval      => 'FREQ=DAILY; BYHOUR=2', -- Run daily at 2 AM
    end_date             => NULL,
    enabled              => TRUE,
    auto_drop            => FALSE,
    comments             => 'Automated job to defragment tablespaces'
  );
END;
/
```

In this example, the job is scheduled to run daily at 2 AM. The `job_action` parameter should be replaced with the actual PL/SQL block that executes the script created earlier.

By automating tablespace maintenance tasks using SQL scripts and jobs, you can ensure optimal performance and storage utilization in your database system. Just make sure to schedule the jobs according to your needs and monitor their execution to ensure they are running successfully.

#SQL #automation