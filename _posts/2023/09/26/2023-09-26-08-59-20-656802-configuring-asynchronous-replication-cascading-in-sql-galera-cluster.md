---
layout: post
title: "Configuring asynchronous replication cascading in SQL Galera Cluster"
description: " "
date: 2023-09-26
tags: [Replace, GaleraCluster]
comments: true
share: true
---

## Introduction

SQL Galera Cluster is a popular solution for high availability and scalability in relational databases. It uses synchronous replication to ensure data consistency across multiple nodes. However, there are scenarios where asynchronous replication cascading can be useful. This blog post explains how to configure asynchronous replication cascading in SQL Galera Cluster.

## Prerequisites

To follow along, you need:
- SQL Galera Cluster installed and up and running.
- Basic knowledge of SQL Galera Cluster and its configuration files.

## Configuring Asynchronous Replication Cascading

1. **Enable the binlog**:
   - Open the `my.cnf` or `my.ini` configuration file on the primary node.
   - Set the following parameters:
     ```ini
     [mysqld]
     log_bin                     = /var/log/mysql/mysql-bin.log
     log_slave_updates           = 1
     relay_log                   = /var/log/mysql/mysql-relay-bin.log
     relay_log_info_repository   = TABLE
     ```
     _#Add the above lines to the existing [mysqld] section._

2. **Restart the primary node**:
   - After adding the configuration, restart the primary node to apply the changes:  
     `sudo service mysql restart`

3. **Check replication status**:
   - Connect to the primary node and execute the following query to check the replication status:
     ```sql
     SHOW MASTER STATUS;
     ```
     Note down the `Binary Log File` and `Position` values.

4. **Configure the secondary node**:
   - Open the `my.cnf` or `my.ini` configuration file on the secondary node.
   - Add the following parameters to enable replication cascading:
     ```ini
     [mysqld]
     log_slave_updates           = 1
     relay_log                   = /var/log/mysql/mysql-relay-bin.log
     relay_log_info_repository   = TABLE
     relay_log_purge             = 1
     binlog_format               = ROW
     slave_compressed_protocol   = 0
  
     replicate_do_db             = example_database
     replicate_ignore_table      = example_database.sample_table
     ```
     _#Add the above lines to the existing [mysqld] section._

5. **Restart the secondary node**:
   - Once the configuration is added, restart the secondary node to apply the changes:  
     `sudo service mysql restart`

6. **Go to primary node**:
   - Connect to the primary node and execute the following query to grant replication privileges to the secondary node:
     ```sql
     GRANT REPLICATION SLAVE ON *.* TO 'slave_user'@'secondary_node_ip' IDENTIFIED BY 'password';
     FLUSH PRIVILEGES;
     ```

7. **Configure secondary node replication**:
   - Connect to the secondary node and execute the following query to configure replication from the primary node:
     ```sql
     CHANGE MASTER TO MASTER_HOST='primary_node_ip', MASTER_PORT=3306, MASTER_USER='slave_user', MASTER_PASSWORD='password', MASTER_LOG_FILE='binary_log_file', MASTER_LOG_POS=binary_log_position;
     ```
     _#Replace the placeholders with actual values._

8. **Start replication**:
   - Execute the following query on the secondary node to start replication:
     ```sql
     START SLAVE;
     ```

9. **Verify replication status**:
   - Connect to the secondary node and execute the following query to verify the replication status:
     ```sql
     SHOW SLAVE STATUS\G;
     ```

## Conclusion

Configuring asynchronous replication cascading in SQL Galera Cluster allows you to achieve high availability and scalability while also accommodating different scenarios and distributed setups. By following the steps outlined in this blog post, you can easily configure asynchronous replication cascading in your SQL Galera Cluster. #GaleraCluster #ReplicationCascading