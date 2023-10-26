---
layout: post
title: "[python] Implementing pagination with Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Pagination is a common feature in web development that allows users to navigate through a large set of data in smaller, more manageable chunks. In this blog post, we will explore how to implement pagination using Tortoise ORM in Python.

## Table of Contents

- [What is Tortoise ORM?](#what-is-tortoise-orm)
- [Why use Pagination?](#why-use-pagination)
- [Implementing Pagination with Tortoise ORM](#implementing-pagination-with-tortoise-orm)
  - [Fetching Data with Limit and Offset](#fetching-data-with-limit-and-offset)
  - [Calculating Total Pages](#calculating-total-pages)
  - [Displaying Page Links](#displaying-page-links)
- [Conclusion](#conclusion)
- [References](#references)

## What is Tortoise ORM?

Tortoise ORM is an easy-to-use asyncio ORM (Object Relational Mapping) library for Python that provides support for managing database records and relationships. It is highly compatible with asyncio and is designed to work seamlessly with the Tortoise-ORM-compatible databases, such as PostgreSQL and SQLite.

## Why use Pagination?

When dealing with large datasets, it's essential to implement pagination to improve the user experience and optimize performance. Here are a few reasons why pagination is important:

1. **Improved Performance**: By loading a limited number of records per page, pagination reduces the amount of data fetched from the database, resulting in faster page rendering.

2. **Enhanced User Experience**: Users can navigate through pages easily, allowing them to find the desired information quickly.

3. **Reduced Server Load**: With pagination, the server only needs to process and transmit a small subset of data, reducing server load and improving overall scalability.

## Implementing Pagination with Tortoise ORM

To implement pagination with Tortoise ORM, we can follow a few simple steps.

### Fetching Data with Limit and Offset

The first step is to fetch data from the database using the `limit` and `offset` parameters, which control the number of records to be retrieved per page and the starting position, respectively.

Here's an example code snippet for fetching paginated data using Tortoise ORM:

```python
async def get_paginated_data(page_number, page_size):
    offset = (page_number - 1) * page_size
    query = MyModel.query.order_by("-created_at").offset(offset).limit(page_size)
    data = await query.all()
    return data
```

In the above code, we calculate the `offset` based on the desired page number and page size. We then use `offset()` and `limit()` methods along with the desired query filters to retrieve the paginated data.

### Calculating Total Pages

To provide navigation links and indicate the total number of pages, we need to calculate the total number of pages based on the total count of records and the desired page size.

Here's an example code snippet to calculate the total number of pages:

```python
async def get_total_pages(page_size):
    total_records = await MyModel.query.count()
    total_pages = total_records // page_size
    if total_records % page_size != 0:
        total_pages += 1
    return total_pages
```

In the above code, we calculate the `total_records` using the `count()` method. We then divide the total records by the page size to get the total number of pages. If there are remaining records, we increment the total pages by 1 to accommodate them.

### Displaying Page Links

Finally, to provide navigation links and allow users to switch between pages, we can generate the necessary URLs or page numbers dynamically.

Here's an example code snippet to generate page links:

```python
def generate_page_links(current_page, total_pages):
    page_links = []
    for page_number in range(1, total_pages + 1):
        if page_number == current_page:
            page_links.append(f"[**{page_number}**](/page/{page_number})")
        else:
            page_links.append(f"[{page_number}](/page/{page_number})")
    return " | ".join(page_links)
```

In the above code, we iterate over the range of total pages and generate the appropriate links. The current page is highlighted using bold markdown formatting.

## Conclusion

Implementing pagination is crucial when working with large datasets to improve performance, enhance user experience, and reduce server load. Tortoise ORM simplifies the process of implementing pagination by providing convenient methods to fetch limited records and calculate the total number of pages.

By following the steps outlined in this blog post, you can easily implement pagination with Tortoise ORM in your Python projects.

## References

- [Tortoise ORM Documentation](https://tortoise.github.io/)
- [Pagination in Web Design: Best Practices and Examples](https://www.smashingmagazine.com/2007/11/pagination-gallery-examples-and-good-practices/)