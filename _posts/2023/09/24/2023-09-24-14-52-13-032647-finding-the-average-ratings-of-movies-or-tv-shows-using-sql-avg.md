---
layout: post
title: "Finding the average ratings of movies or TV shows using SQL AVG"
description: " "
date: 2023-09-24
tags: [database]
comments: true
share: true
---

In the world of entertainment, ratings play a crucial role in determining the popularity and quality of movies or TV shows. As a data analyst or developer, you may often come across the need to calculate the average ratings of these media items based on user reviews or ratings. In this article, we will explore how to efficiently retrieve these average ratings using the SQL AVG function.

## What is SQL AVG?

AVG is an aggregate function in SQL that allows you to calculate the average of a set of values in a specified column. When applied to a column containing ratings, AVG will return the average rating of the selected items.

## Syntax of SQL AVG

The basic syntax of SQL AVG is as follows:

```sql
SELECT AVG(column_name) FROM table_name;
```

Where `column_name` is the column that contains ratings, and `table_name` is the name of the table holding the data.

## Example Usage

To illustrate the usage of SQL AVG, let's consider a table called `movies` with the following structure:

```sql
CREATE TABLE movies (
  id INT,
  title VARCHAR(255),
  rating FLOAT
);
```

Assume that this table contains several movie records with their respective ratings. To find the average rating of all movies in the table, you can use the following query:

```sql
SELECT AVG(rating) AS average_rating FROM movies;
```

The `AVG(rating)` expression calculates the average rating, and the optional `AS average_rating` clause assigns the result to a column alias for better readability. The result of this query will be the average rating of all movies in the table.

## Filtering by Condition

If you want to calculate the average rating of movies or TV shows that meet specific criteria, you can use a `WHERE` clause to filter the data. For example, to find the average rating of movies released in the past year, you can modify the previous query as follows:

```sql
SELECT AVG(rating) AS average_rating FROM movies WHERE YEAR(release_date) = YEAR(CURDATE()) - 1;
```

In this modified query, we are using the `YEAR()` function to compare the release year of movies with the previous year. The `CURDATE()` function is used to get the current date, and subtracting 1 from its year component gives us the previous year.

## Conclusion

The SQL AVG function provides a simple and efficient way to calculate the average ratings of movies or TV shows based on their user ratings. By leveraging this powerful aggregate function, data analysts and developers can derive valuable insights from the vast amount of entertainment data available today.

#database #SQL