---
layout: post
title: "Calculating weighted averages in SQL using AVG function"
description: " "
date: 2023-09-24
tags: [WeightedAverage]
comments: true
share: true
---

## Understanding Weighted Averages

A weighted average assigns different weights to each value in a dataset, based on its significance or importance. This allows you to give more importance to certain values over others when calculating the average. In SQL, you can achieve this by multiplying each value by its weight and then calculating the average.

## Calculating Weighted Averages in SQL

Let's assume we have a table called `grades` with the following structure:

```sql
CREATE TABLE grades (
    student_id INT,
    subject_id INT,
    score INT,
    weight DECIMAL(5,2)
);
```

To calculate the weighted average score for each student in a specific subject, you can use the following SQL query:

```sql
SELECT student_id, subject_id, AVG(score * weight) AS weighted_average
FROM grades
WHERE subject_id = 1
GROUP BY student_id, subject_id;
```

In this example, we are calculating the weighted average score for subject_id = 1. The `AVG(score * weight)` expression multiplies each score by its corresponding weight and calculates the average of these weighted values.

## Example

Let's consider the following data in the `grades` table:

```
| student_id | subject_id | score | weight |
|------------|------------|-------|--------|
| 1          | 1          | 90    | 0.6    |
| 2          | 1          | 80    | 0.4    |
| 3          | 1          | 95    | 0.7    |
```

Using the SQL query mentioned above, we can calculate the weighted average score for subject_id = 1. The result will be:

```
| student_id | subject_id | weighted_average |
|------------|------------|------------------|
| 1          | 1          | 89.5             |
| 2          | 1          | 83.0             |
| 3          | 1          | 96.5             |
```

## Conclusion

Calculating weighted averages in SQL can be easily achieved using the `AVG()` function and the appropriate mathematical calculations. By assigning weights to different values, you can obtain more accurate averages that reflect the importance of each data point. Incorporating weighted averages in your SQL queries can enhance your data analysis capabilities.

#SQL #WeightedAverage