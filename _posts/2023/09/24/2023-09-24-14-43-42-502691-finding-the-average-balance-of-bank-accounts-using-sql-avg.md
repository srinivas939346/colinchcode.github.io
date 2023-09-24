---
layout: post
title: "Finding the average balance of bank accounts using SQL AVG"
description: " "
date: 2023-09-24
tags: [BankAccounts]
comments: true
share: true
---

Calculating the average balance of bank accounts can provide valuable insights into the financial health of customers. In this blog post, we will explore how to use SQL's AVG function to calculate the average balance of bank accounts.

## Getting Started

To start with, we need a table that contains the bank account details, including the account number, customer name, and account balance. Let's assume we have a table named "bank_accounts" with the following structure:

```sql
CREATE TABLE bank_accounts (
  account_number INT,
  customer_name VARCHAR(50),
  account_balance DECIMAL(10,2)
);
```

## Calculating Average Balance

To calculate the average balance of bank accounts, we can use the SQL AVG function. The AVG function calculates the average value of a given column. In this case, we want to calculate the average of the "account_balance" column.

The SQL query to calculate the average balance would be:

```sql
SELECT AVG(account_balance) AS average_balance
FROM bank_accounts;
```

This query uses the AVG function to calculate the average value of the "account_balance" column and aliases it as "average_balance". The result will be a single row with the average balance value.

## Example

Let's consider a simple example to illustrate the usage of the SQL AVG function. Assume we have the following data in our "bank_accounts" table:

| account_number | customer_name | account_balance |
|----------------|---------------|-----------------|
| 123            | John Doe      | 1000.00         |
| 456            | Jane Smith    | 1500.00         |
| 789            | David Johnson | 2000.00         |

If we run the SQL query mentioned above to calculate the average balance, the result would be:

```sql
average_balance
---------------
1500.00
```

## Conclusion

Calculating the average balance of bank accounts is a common task in financial analysis. By using SQL's AVG function, we can easily obtain this information from a database table. The example provided in this blog post demonstrates how to use the AVG function to calculate the average balance of bank accounts using SQL.

#SQL #BankAccounts #AVG