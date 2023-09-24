---
layout: post
title: "Finding the average occupancy rate of hotels using SQL AVG"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

In the hotel industry, tracking and analyzing the occupancy rate is crucial for understanding the performance and profitability of a property. The average occupancy rate provides insights into how well a hotel is utilizing its available rooms. In this tech blog post, we will explore how to calculate the average occupancy rate of hotels using SQL and the AVG function.

## Understanding the Average Occupancy Rate

The average occupancy rate is calculated by dividing the total number of occupied rooms by the total number of available rooms, expressed as a percentage. It helps hotel managers assess the effectiveness of their pricing strategies, marketing efforts, and overall business performance.

## SQL Syntax to Calculate Average Occupancy Rate

To calculate the average occupancy rate of hotels using SQL, we need a table that stores information about room occupancy over a specific time period. Let's assume we have a table named `room_occupancy` with the following columns:

- `hotel_id` (unique identifier for the hotel)
- `date` (date of occupancy)
- `occupied_rooms` (number of occupied rooms on that date)
- `total_rooms` (total number of available rooms in the hotel)

Here's an example SQL query that calculates the average occupancy rate:

```sql
SELECT AVG((occupied_rooms * 100) / total_rooms) AS average_occupancy_rate
FROM room_occupancy
WHERE date >= '2022-01-01' AND date <= '2022-12-31';
```

In the above query, we use the AVG function to calculate the average occupancy rate. We multiply the occupancy rate by 100 to convert it into a percentage.

## Example Usage

Let's consider a scenario where we want to calculate the average occupancy rate for a hotel chain across all their properties for the year 2022. We can execute the following SQL query:

```sql
SELECT AVG((occupied_rooms * 100) / total_rooms) AS average_occupancy_rate
FROM room_occupancy
WHERE date >= '2022-01-01' AND date <= '2022-12-31';
```

The query will return the overall average occupancy rate for the hotel chain during the specified time period.

## Conclusion

Calculating the average occupancy rate of hotels using SQL and the AVG function provides valuable insights into room utilization and helps hotel managers make informed decisions. By analyzing this metric, hoteliers can optimize their business strategies and improve overall performance.