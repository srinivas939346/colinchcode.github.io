---
layout: post
title: "SCD (Slowly Changing Dimension) types in dimension tables."
description: " "
date: 2023-09-22
tags: [datawarehousing]
comments: true
share: true
---

Dimension tables in data warehousing are used to capture descriptive attributes and provide context to the data in a fact table. Slowly Changing Dimensions (SCD) refer to those attributes that change over time, necessitating the need to track historical values. There are different types of SCD that can be implemented to handle such changes. In this blog post, we will discuss the commonly used SCD types and their characteristics.

## SCD Type 1: Overwrite/Current Value

SCD Type 1, also known as the overwrite or current value strategy, involves directly updating the existing dimension record whenever there is a change in any attribute. This approach completely discards the history and keeps only the most recent values. It is suitable when historical data is not required, and only the current state matters.

For example, consider a customer dimension table. If a customer changes their address, the existing record will be updated with the new address, and the old address will be lost.

The main advantages of SCD Type 1 are simplicity and speed, as it involves minimal overhead in terms of storage and processing. However, the drawback is the loss of historical data, which may be important for analysis or reporting purposes.

## SCD Type 2: Add New Row/Versioning

SCD Type 2, also known as the add new row or versioning strategy, handles changes by creating a new row for each distinct attribute value combination, thus maintaining a complete history of dimension records. Each row is assigned a unique identifier or surrogate key to track its different versions.

For example, in the customer dimension table, if a customer changes their address, a new row will be added with the updated address, while retaining the old row with the previous address.

This method allows for historical analysis and retrospective reporting, but it comes at the cost of increased storage requirements and complexity in queries that involve joining with the dimension table.

## SCD Type 3: Add New Columns

SCD Type 3 involves adding new columns to the dimension table to capture limited historical changes. Usually, only a few important attributes are chosen to be tracked. The new columns represent the old attribute values before the change, while the existing columns hold the current values.

For example, in the customer dimension table, if a customer changes their phone number, a new column 'old phone number' may be added to store the previous value, while the 'phone number' column holds the current value.

This approach allows for a compromise between storage and historical tracking, but it restricts the number of attributes that can be tracked and hampers the ability to perform detailed analysis on historical changes.

## Conclusion

Understanding the different SCD types is crucial for designing dimension tables in a data warehouse. The choice of SCD type depends on the requirements of the business and the level of historical analysis needed. Whether it's overwriting the current value, adding new rows, or incorporating additional columns, each SCD type has its strengths and trade-offs to consider when maintaining the integrity and context of data in dimension tables.

#datawarehousing #SCD