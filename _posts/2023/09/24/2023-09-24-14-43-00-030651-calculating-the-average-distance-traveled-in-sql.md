---
layout: post
title: "Calculating the average distance traveled in SQL"
description: " "
date: 2023-09-24
tags: [average]
comments: true
share: true
---

In this blog post, we will discuss how to calculate the average distance traveled in SQL using a simple example.

### Database Structure

To get started, let's assume we have a database table called "trips" that contains information about different trips taken by users. The table has the following structure:

| trip_id | user_id | distance |
|---------|---------|----------|
| 1       | 100     | 10       |
| 2       | 200     | 20       |
| 3       | 100     | 30       |
| 4       | 300     | 15       |
| 5       | 200     | 25       |

Each row in the table represents a single trip, with columns indicating the trip ID, user ID, and distance traveled in kilometers.

### Calculating Average Distance Traveled

To calculate the average distance traveled by users, we can use the following SQL query:

```sql
SELECT AVG(distance) AS average_distance FROM trips;
```

This query uses the `AVG` function to calculate the average of the `distance` column from the `trips` table. The result is returned as a single value and can be accessed using the alias `average_distance`.

When you execute the above query, you will get the average distance traveled across all trips:

| average_distance |
|------------------|
| 20              |

The result shows that the average distance traveled across all trips is 20 kilometers.

### Conclusion

In this blog post, we discussed how to calculate the average distance traveled in SQL using a simple example. By using the `AVG` function, we were able to find the average distance traveled by users. This can be helpful in analyzing travel patterns and making data-driven decisions. 

#SQL #average-distance