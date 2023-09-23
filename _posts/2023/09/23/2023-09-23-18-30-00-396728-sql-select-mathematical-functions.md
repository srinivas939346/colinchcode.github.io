---
layout: post
title: "SQL SELECT mathematical functions"
description: " "
date: 2023-09-23
tags: [MathematicalFunctions]
comments: true
share: true
---

In SQL, there are several mathematical functions that can be used in the SELECT statement to perform calculations on numeric data. These functions can help transform and analyze data in a meaningful way.

## 1. ABS function

The ABS function returns the absolute value of a number. It takes a single argument and returns its positive value. For example:

```sql
SELECT ABS(-10);
```

Output: 10

## 2. ROUND function

The ROUND function rounds a number to a specified number of decimal places. It takes two arguments - the number to be rounded and the number of decimal places. For example:

```sql
SELECT ROUND(3.14159, 2);
```

Output: 3.14

## 3. CEILING function

The CEILING function rounds a number up to the nearest integer greater than or equal to the input value. For example:

```sql
SELECT CEILING(4.8);
```

Output: 5

## 4. FLOOR function

The FLOOR function rounds a number down to the nearest integer less than or equal to the input value. For example:

```sql
SELECT FLOOR(4.8);
```

Output: 4

## 5. POWER function

The POWER function calculates the value of a number raised to a specified power. It takes two arguments - the base number and the exponent. For example:

```sql
SELECT POWER(2, 3);
```

Output: 8

## 6. SQRT function

The SQRT function calculates the square root of a number. It takes a single argument and returns the square root. For example:

```sql
SELECT SQRT(25);
```

Output: 5

## 7. MOD function

The MOD function calculates the remainder of a division operation. It takes two arguments - the dividend and the divisor. For example:

```sql
SELECT MOD(10, 3);
```

Output: 1

These are just a few examples of the mathematical functions available in SQL. By utilizing these functions, you can perform various calculations and manipulate numeric data to derive valuable insights. Happy coding! #SQL #MathematicalFunctions