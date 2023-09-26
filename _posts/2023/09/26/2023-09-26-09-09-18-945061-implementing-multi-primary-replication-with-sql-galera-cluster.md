---
layout: post
title: "Implementing multi-primary replication with SQL Galera Cluster"
description: " "
date: 2023-09-26
tags: [galeracluster, multiprimaryreplication]
comments: true
share: true
---

In today's technologically advanced world, high availability of databases is extremely crucial for businesses. **SQL Galera Cluster** provides a highly reliable and scalable solution for achieving database high availability and redundancy using **multi-primary replication**. This blog post aims to guide you through the process of implementing multi-primary replication with SQL Galera Cluster.

## What is Multi-Primary Replication?

Traditional database replication typically follows a master-slave architecture, where one node acts as the master or primary node, and the others serve as slaves or secondary nodes. In this setup, only the master node handles write operations, while the slaves replicate the changes from the master.

On the other hand, **multi-primary replication** allows multiple nodes within a cluster to accept write operations simultaneously. Each node can perform both read and write operations, making it an ideal solution for applications that require high write scalability and read availability.

## Installing SQL Galera Cluster

To begin, let's install SQL Galera Cluster on our desired machines. SQL Galera Cluster is built on top of the popular **MariaDB** database, so we need to ensure that we have MariaDB installed on all the nodes.

```shell
# Install MariaDB on Ubuntu
sudo apt-get update
sudo apt-get install mariadb-server

# Install MariaDB on CentOS
sudo yum install mariadb-server
sudo systemctl enable mariadb
sudo systemctl start mariadb
```

## Configuring MariaDB for Multi-Primary Replication

Once MariaDB is installed, we need to configure it to enable multi-primary replication. 

1. Open the MariaDB configuration file:

```shell
sudo vi /etc/mysql/mariadb.conf.d/50-server.cnf
```

2. Add the following configuration options under the `[mysqld]` section:

```shell
wsrep_on=ON
wsrep_cluster_name="my_galera_cluster"
wsrep_cluster_address="gcomm://<list_of_cluster_IPs>"
wsrep_provider=/usr/lib/galera/libgalera_smm.so
wsrep_sst_method=rsync
```

Replace `<list_of_cluster_IPs>` with the comma-separated IP addresses of all the nodes in your SQL Galera Cluster.

3. Save and exit the configuration file.

## Bootstrapping the Galera Cluster

To bootstrap the Galera Cluster, perform the following steps on one of the nodes:

1. Stop the MariaDB service:

```shell
sudo systemctl stop mariadb
```

2. Initialize the cluster:

```shell
sudo galera_new_cluster
```

3. Start MariaDB service:

```shell
sudo systemctl start mariadb
```

## Joining Additional Nodes to the Cluster

To join the remaining nodes to the cluster, perform the following steps on each node:

1. Stop the MariaDB service:

```shell
sudo systemctl stop mariadb
```

2. Clear the data directory:

```shell
sudo rm -rf /var/lib/mysql/*
```

3. Copy the Galera Cluster state from an existing node:

```shell
sudo rsync -av --progress <existing_node>:/var/lib/mysql/ /var/lib/mysql/
```

Replace `<existing_node>` with the IP address of any existing node in the cluster.

4. Start MariaDB service:

```shell
sudo systemctl start mariadb
```

Repeat steps 1-4 for each additional node you want to add to the cluster.

## Verifying the Cluster Status

To verify the status of the SQL Galera Cluster, run the following command on any node in the cluster:

```shell
sudo mysql -e "SHOW STATUS LIKE 'wsrep_%'"
```

## Conclusion

Implementing multi-primary replication with SQL Galera Cluster can significantly enhance the availability and scalability of your database. By allowing multiple nodes to accept write operations, you can achieve higher write scalability, read availability, and redundancy. Follow the steps outlined in this blog post to implement multi-primary replication with SQL Galera Cluster and enjoy a highly reliable database solution.

#galeracluster #multiprimaryreplication