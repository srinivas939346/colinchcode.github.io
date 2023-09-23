---
layout: post
title: "SQL SELECT distinct with joins"
description: " "
date: 2023-09-23
tags: [SELECT, distinct]
comments: true
share: true
---

When working with SQL joins, it is common to retrieve multiple records that have duplicate values in one or more columns. However, there may be scenarios where you want to retrieve only distinct values from a specific column or set of columns. In such cases, you can use the `SELECT DISTINCT` statement along with joins.

## Syntax

The syntax for using `SELECT DISTINCT` with joins is similar to the regular join syntax. Here's an example:

```sql
SELECT DISTINCT column_name(s)
FROM table1
JOIN table2 ON join_condition
```

## Example

Let's consider a scenario where you have two tables: `students` and `courses`. The `students` table contains information about students, including their names and student IDs. The `courses` table contains information about different courses, including the course names and the student IDs of the students enrolled in each course.

To retrieve the distinct course names for all enrolled students, you can use the `SELECT DISTINCT` statement with a join:

```sql
SELECT DISTINCT courses.course_name
FROM students
JOIN courses ON students.student_id = courses.student_id
```

In this example, the `DISTINCT` keyword ensures that only unique course names are returned, eliminating any duplicate values. The `JOIN` condition connects the two tables based on the `student_id` column.

## Conclusion

Using `SELECT DISTINCT` with joins allows you to retrieve only unique values from a specific column or set of columns when working with multiple tables. By incorporating this syntax in your SQL queries, you can filter out duplicate records and obtain the distinct results you desire.

#SQL #SELECT #distinct #joins