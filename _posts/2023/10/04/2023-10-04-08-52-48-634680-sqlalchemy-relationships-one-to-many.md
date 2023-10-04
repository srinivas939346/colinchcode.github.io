---
layout: post
title: "[python] SQLAlchemy Relationships: One-to-Many"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

When working with databases, it is often necessary to establish relationships between different tables. In SQLAlchemy, a common type of relationship is the one-to-many relationship, where one record in one table is related to multiple records in another table. In this blog post, we will explore how to define and work with one-to-many relationships using SQLAlchemy.

## Table Design

To illustrate the concept of a one-to-many relationship, let's consider a simple example of an online store. We have two tables: `Customer` and `Order`. Each customer can have multiple orders, but an order can only belong to a single customer. 

Let's define the `Customer` table:

```python
from sqlalchemy import Column, Integer, String
from sqlalchemy.orm import relationship

class Customer(Base):
    __tablename__ = 'customers'
    
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    orders = relationship('Order', backref='customer')
```

Here, we define a one-to-many relationship between `Customer` and `Order` using the `relationship` function. The `backref` parameter creates an additional attribute on the `Order` model, allowing easy access to the associated customer.

Now, let's define the `Order` table:

```python
from sqlalchemy import Column, Integer, String, ForeignKey

class Order(Base):
    __tablename__ = 'orders'
    
    id = Column(Integer, primary_key=True)
    order_number = Column(String(10))
    customer_id = Column(Integer, ForeignKey('customers.id'))
```

In the `Order` table, we include a foreign key `customer_id` that references the `id` column of the `Customer` table. This establishes the relationship between the two tables.

## Querying One-to-Many Relationships

Once the tables are defined, we can perform queries that involve the one-to-many relationship. Let's say we want to retrieve all orders for a specific customer. We can simply use the `orders` attribute of the `Customer` model:

```python
customer = session.query(Customer).filter_by(id=1).first()
orders = customer.orders
```

In this example, we query the `Customer` table to retrieve the customer with `id` equal to 1. We then access the `orders` attribute, which will give us a list of all the orders associated with that customer.

## Creating One-to-Many Relationships

To create a new order for a customer, we can perform the following steps:

```python
customer = session.query(Customer).filter_by(id=1).first()
order = Order(order_number='12345', customer=customer)
session.add(order)
session.commit()
```

Here, we first retrieve the customer object from the database. We then create a new `Order` object, specifying the `order_number` and associating it with the customer by assigning the customer object to the `customer` attribute. Finally, we add the order object to the session and commit the changes to the database.

## Conclusion

In this blog post, we have explored how to define and work with one-to-many relationships using SQLAlchemy. We saw how to define the relationship between two tables, how to query records based on this relationship, and how to create new records that establish the relationship. Understanding and effectively using one-to-many relationships is crucial when dealing with relational databases. SQLAlchemy provides a powerful and flexible toolkit to handle such relationships seamlessly.

I hope you found this blog post helpful in understanding one-to-many relationships using SQLAlchemy. Stay tuned for more posts on SQLAlchemy and database modeling.