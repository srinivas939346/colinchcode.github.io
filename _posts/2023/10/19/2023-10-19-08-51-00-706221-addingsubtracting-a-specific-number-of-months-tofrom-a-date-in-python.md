---
layout: post
title: "[python] Adding/subtracting a specific number of months to/from a date in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

First, make sure you have `dateutil` installed. If not, you can install it by running the following command:

```bash
pip install python-dateutil
```

Now, let's look at an example. Suppose you have a date and you want to add 3 months to it. Here's how you can do it in Python:

```python
from datetime import datetime
from dateutil.relativedelta import relativedelta

date_string = "2022-01-01"
date = datetime.strptime(date_string, "%Y-%m-%d")

new_date = date + relativedelta(months=3)

print(new_date)
```

In the code above, we first import the necessary modules: `datetime` to handle dates and `relativedelta` from `dateutil` to perform the date arithmetic.

Next, we define a `date_string` representing a date in the format "YYYY-MM-DD". We use `strptime()` from `datetime` to convert this string into a `datetime` object.

Then, we create a new date by adding a `relativedelta` of 3 months to the original date. The `months` parameter specifies the number of months we want to add.

Finally, we print the new date.

If you want to subtract a specific number of months, you can simply use a negative integer value for the `months` parameter in `relativedelta`. For example, to subtract 2 months, you can do:

```python
new_date = date - relativedelta(months=2)
```

Using `relativedelta`, you can easily perform date arithmetic with months and other units, making it a powerful tool for manipulating dates in Python.

For more information, you can refer to the official documentation of the `dateutil` module: [python-dateutil documentation](https://dateutil.readthedocs.io/en/stable/relativedelta.html)