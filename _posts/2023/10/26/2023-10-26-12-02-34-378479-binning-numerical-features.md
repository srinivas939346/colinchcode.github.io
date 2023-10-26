---
layout: post
title: "[python] Binning numerical features"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In data analysis, binning is a technique used to group continuous numerical variables into discrete intervals or bins. Binning can be useful in various scenarios, such as reducing the impact of outliers, simplifying models, or creating categorical features from numerical data.

In this blog post, we will explore how to bin numerical features in Python using the `pandas` and `numpy` libraries.

### Importing the Libraries

Before we start, let's import the necessary libraries:

```python
import pandas as pd
import numpy as np
```

### Creating Example DataFrame

Let's create an example DataFrame to demonstrate the binning process:

```python
df = pd.DataFrame({'Age': [25, 30, 35, 40, 45, 50, 55, 60, 65, 70],
                   'Income': [30000, 50000, 40000, 80000, 60000, 90000, 70000, 120000, 100000, 110000]})
print(df)
```

The DataFrame contains two columns: 'Age' and 'Income', representing numerical features.

### Equal Width Binning

Equal Width Binning (also known as uniform binning) divides the feature range into equal-sized intervals. This method is useful when the feature has a relatively uniform distribution.

To perform equal width binning using `pandas`, we can use the `cut()` function:

```python
df['Age_Bins'] = pd.cut(df['Age'], bins=3) 
print(df['Age_Bins'])
```

The above code creates new bins for the 'Age' feature by dividing it into 3 equal intervals. The resulting intervals will be stored in the 'Age_Bins' column.

### Equal Frequency Binning

Equal Frequency Binning (also known as quantile binning) divides the feature into bins containing an equal number of observations. This method is useful when we want to handle skewed distributions or outliers.

To perform equal frequency binning using `pandas`, we can use the `qcut()` function:

```python
df['Income_Bins'] = pd.qcut(df['Income'], q=4)
print(df['Income_Bins'])
```

The above code creates new bins for the 'Income' feature by dividing it into 4 intervals of approximately equal size. The resulting intervals will be stored in the 'Income_Bins' column.

### Custom Binning

In some cases, we may want to define custom bins based on specific criteria. We can use the `cut()` function with a custom binning definition:

```python
# Define the custom bin edges
age_bins = [0, 30, 50, 100]

# Perform custom binning based on the defined edges
df['Age_Custom_Bins'] = pd.cut(df['Age'], bins=age_bins)
print(df['Age_Custom_Bins'])
```

The above code defines custom bin edges for the 'Age' feature and performs binning accordingly. The resulting intervals will be stored in the 'Age_Custom_Bins' column.

### Conclusion

Binning numerical features can be a useful preprocessing technique in data analysis or machine learning tasks. In this blog post, we learned how to bin numerical features in Python using the `pandas` library. We covered equal width binning, equal frequency binning, and custom binning. By applying these techniques, we can transform continuous numerical variables into discrete intervals, facilitating data analysis and modeling processes.

**References:**
- [pandas.cut documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.cut.html)
- [pandas.qcut documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.qcut.html)