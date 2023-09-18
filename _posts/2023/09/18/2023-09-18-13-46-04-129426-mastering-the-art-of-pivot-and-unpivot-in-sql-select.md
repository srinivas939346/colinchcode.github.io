---
layout: post
title: "Mastering the art of pivot and unpivot in SQL SELECT"
description: " "
date: 2023-09-18
tags: [DataManipulation]
comments: true
share: true
---

If you are working with databases and need to manipulate data in a tabular format, you've probably encountered situations where you want to transform rows into columns or vice versa. SQL provides powerful techniques called **pivot** and **unpivot** that allow you to achieve this transformation easily.

## Pivot - Transforming Rows into Columns
Pivoting in SQL is the process of transforming rows into columns, creating a new result set that is more compact and easier to analyze. This is useful when you have data in a long format and want to display it in a wide format.

The syntax for pivoting data in SQL varies across different database management systems, but the basic idea remains the same. Let's take a look at an example using the `PIVOT` keyword in SQL Server:

```sql
SELECT [Category], [2019], [2020], [2021]
FROM (
  SELECT Category, Year, Sales
  FROM SalesData
) AS Data
PIVOT (
  SUM(Sales)
  FOR Year IN ([2019], [2020], [2021])
) AS PivotedData;
```

In this example, we are pivoting the `SalesData` table based on the `Year` column. The `PIVOT` function aggregates the `Sales` column for each year and displays the result as columns `[2019]`, `[2020]`, and `[2021]`. The resulting table will have the `Category` as rows and the sales for each year as columns.

## Unpivot - Transforming Columns into Rows
Unpivoting is the opposite of pivoting, converting columns into rows. This technique is useful when you have data in a wide format and want to normalize it into a long format.

Again, the syntax for performing an unpivot operation may vary, but the concept remains consistent. Here's an example using the `UNPIVOT` keyword in SQL Server:

```sql
SELECT Category, Year, Sales
FROM (
  SELECT [Category], [2019], [2020], [2021]
  FROM PivotedData
) AS Data
UNPIVOT (
  Sales
  FOR Year IN ([2019], [2020], [2021])
) AS UnpivotedData;
```

In this example, we are unpivoting the `PivotedData` table that we obtained from the previous pivot operation. The `UNPIVOT` function converts the columns `[2019]`, `[2020]`, and `[2021]` back into rows, with the corresponding year and sales values.

## Conclusion
By mastering the concepts of pivot and unpivot in SQL, you can efficiently transform data between rows and columns, allowing you to perform more complex analyses and reporting. Remember to use the appropriate pivoting and unpivoting functions based on your database management system.

#SQL #DataManipulation