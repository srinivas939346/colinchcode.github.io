---
layout: post
title: "SQL SELECT date functions"
description: " "
date: 2023-09-23
tags: [SELECT, DateFunctions]
comments: true
share: true
---

In SQL, date functions are used to manipulate and format dates stored in the database. These functions allow you to perform various operations on dates, such as extracting specific parts of a date or performing mathematical calculations with dates.

Here are some commonly used date functions in SQL:

## 1. `DATE()`
The `DATE()` function is used to extract the date portion from a datetime or timestamp value. It returns the date without the time component.

```sql
SELECT DATE(datetime_column) AS date_only
FROM your_table;
```

## 2. `YEAR()`, `MONTH()`, `DAY()`
These functions are used to extract the year, month, and day from a date respectively.

```sql
SELECT YEAR(date_column) AS year,
       MONTH(date_column) AS month,
       DAY(date_column) AS day
FROM your_table;
```

## 3. `GETDATE()`
The `GETDATE()` function is used to get the current system date and time.

```sql
SELECT GETDATE() AS current_datetime;
```

## 4. `DATEDIFF()`
The `DATEDIFF()` function calculates the difference between two dates in a specified unit. It returns an integer value.

```sql
SELECT DATEDIFF(day, start_date, end_date) AS days_difference
FROM your_table;
```

## 5. `DATEADD()`
The `DATEADD()` function is used to add or subtract a specified time interval to a date. It can be used to calculate a future or past date based on the provided interval.

```sql
SELECT DATEADD(day, 7, start_date) AS future_date
FROM your_table;
```

## Conclusion
Date functions in SQL are powerful tools that allow you to manipulate and format dates stored in a database. Whether you need to extract specific parts of a date or perform calculations with dates, these functions provide the necessary functionality. By using these functions effectively, you can easily work with dates in SQL queries.

#SQL #SELECT #DateFunctions