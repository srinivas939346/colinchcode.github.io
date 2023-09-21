---
layout: post
title: "Working with pluggable databases and tablespace containers in SQL"
description: " "
date: 2023-09-21
tags: [Oracle, Oracle, Oracle, Oracle, Oracle, Oracle]
comments: true
share: true
---

In Oracle Database 12c and onwards, pluggable databases (PDBs) and tablespace containers have revolutionized the way we manage and organize our data. PDBs allow us to isolate and consolidate multiple databases within a single Oracle instance, while tablespace containers provide a logical structure for storing our data files. In this blog post, we will explore some common SQL operations and commands to help you effectively work with PDBs and tablespace containers.

## Creating a Pluggable Database

To create a new PDB, you can use the `CREATE PLUGGABLE DATABASE` statement. Here's an example:

```sql
CREATE PLUGGABLE DATABASE my_pdb
ADMIN USER pdb_admin
IDENTIFIED BY password
FILE_NAME_CONVERT=('/u01/oradata/cdb/my_pdb/', '/u01/oradata/cdb/my_pdb_clone/')
DEFAULT TABLESPACE users
...
```
#SQL #Oracle

## Provisioning Tablespace Containers

Once you have created a PDB, you can provision tablespace containers within it using the `CREATE TABLESPACE` statement. Here's an example:

```sql
CREATE TABLESPACE my_ts
DATAFILE '/u01/oradata/cdb/my_pdb/my_ts01.dbf'
SIZE 100M
AUTOEXTEND ON
NEXT 10M
EXTENT MANAGEMENT LOCAL;
```
#SQL #Oracle

## Switching to a Pluggable Database

To switch to a specific PDB, you can use the `ALTER SESSION` command. Here's an example:

```sql
ALTER SESSION SET CONTAINER = my_pdb;
```
#SQL #Oracle

## Querying Pluggable Database Information

To retrieve information about the PDBs in your Oracle instance, you can query the `CDB_PDBS` view. Here's an example:

```sql
SELECT name, open_mode
FROM CDB_PDBS;
```
#SQL #Oracle

## Managing Tablespace Containers

To manage tablespace containers, you can use various SQL commands. For example, you can add a data file to a tablespace using the `ALTER TABLESPACE` statement:

```sql
ALTER TABLESPACE my_ts
ADD DATAFILE '/u01/oradata/cdb/my_pdb/my_ts02.dbf'
SIZE 100M
AUTOEXTEND ON
NEXT 10M;
```
#SQL #Oracle

## Conclusion

Working with pluggable databases and tablespace containers in Oracle SQL provides flexibility and scalability to manage your databases efficiently. Whether you are creating PDBs, provisioning tablespace containers, or querying PDB information, understanding these SQL commands is crucial. By leveraging these capabilities, you can optimize resource utilization and streamline your database operations.

#SQL #Oracle