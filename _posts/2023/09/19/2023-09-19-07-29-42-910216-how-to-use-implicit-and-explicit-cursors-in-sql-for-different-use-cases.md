---
layout: post
title: "How to use implicit and explicit cursors in SQL for different use cases"
description: " "
date: 2023-09-19
tags: [SQLCursors, ImplicitCursors, ExplicitCursors]
comments: true
share: true
---

In SQL, cursors are used to traverse through the result set returned by a query. Cursors provide a way to access and manipulate individual rows in a result set. There are two types of cursors: implicit and explicit. In this blog post, we'll explore how to use both types of cursors in different use cases.

## Implicit Cursors

Implicit cursors are automatically created by the database management system (DBMS) when a query is executed. They are used by default to retrieve and process the result set. Implicit cursors are useful for simple operations where you only need to iterate through the result set once.

Here's an example of using an implicit cursor to fetch rows from a table:

```sql
DECLARE
  v_id employees.employee_id%TYPE;
  v_name employees.last_name%TYPE;
BEGIN
  SELECT employee_id, last_name INTO v_id, v_name 
  FROM employees WHERE department_id = 20;
  
  -- Process fetched data
  DBMS_OUTPUT.PUT_LINE('Employee ID: ' || v_id || ', Last Name: ' || v_name);
END;
/
```

In the above code snippet, the implicit cursor retrieves the `employee_id` and `last_name` of employees from the `employees` table with the specified `department_id`. The fetched data is then processed using the `DBMS_OUTPUT.PUT_LINE` function.

## Explicit Cursors

Explicit cursors, on the other hand, are explicitly declared and used by the programmer. They provide more control and flexibility than implicit cursors, especially in complex scenarios where you need to perform operations like fetching data repeatedly or handling exceptions.

Let's look at an example of using an explicit cursor:

```sql
DECLARE
  CURSOR c_employees IS
    SELECT employee_id, last_name
    FROM employees WHERE department_id = 20;
    
  v_id employees.employee_id%TYPE;
  v_name employees.last_name%TYPE;
BEGIN
  OPEN c_employees;
  
  LOOP
    FETCH c_employees INTO v_id, v_name;
    EXIT WHEN c_employees%NOTFOUND;
    
    -- Process fetched data
    DBMS_OUTPUT.PUT_LINE('Employee ID: ' || v_id || ', Last Name: ' || v_name);
  END LOOP;
  
  CLOSE c_employees;
END;
/
```

In the above example, an explicit cursor `c_employees` is declared to select the `employee_id` and `last_name` from employees in the `employees` table with the specified `department_id`. The cursor is explicitly opened, and then a loop is used to fetch each row from the result set. The loop continues until all rows have been fetched, and then the cursor is closed.

## Conclusion

Understanding the difference between implicit and explicit cursors is crucial when working with SQL. Implicit cursors are convenient for simple operations, while explicit cursors offer more control in complex scenarios. By using the appropriate cursor type for different use cases, you can efficiently retrieve and manipulate data from the result set in your SQL queries.

#SQLCursors #ImplicitCursors #ExplicitCursors