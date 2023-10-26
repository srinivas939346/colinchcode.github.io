---
layout: post
title: "[python] Encoding categorical variables in Python"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When working with machine learning models, it is essential to encode categorical variables correctly. Categorical variables are those that contain values from a limited, predefined set, such as colors or categories.

In this blog post, we will explore different methods for encoding categorical variables in Python. We'll cover the following techniques:
1. One-Hot Encoding
2. Label Encoding
3. Ordinal Encoding

## One-Hot Encoding

One-Hot Encoding is a popular method for encoding categorical variables. It converts each category into a binary column, where each column represents the presence or absence of a category.

Let's see an example of how to perform one-hot encoding in Python, using the `pandas` library:

```python
import pandas as pd

# Create a DataFrame with categorical variables
data = {'color': ['red', 'blue', 'green', 'red', 'blue']}
df = pd.DataFrame(data)

# Perform one-hot encoding
df_encoded = pd.get_dummies(df['color'])

# Concatenate the encoded columns with the original DataFrame
df_final = pd.concat([df, df_encoded], axis=1)

print(df_final)
```

Output:

|   color |   blue |   green |   red |
|---------|--------|---------|-------|
| red     |      0 |       0 |     1 |
| blue    |      1 |       0 |     0 |
| green   |      0 |       1 |     0 |
| red     |      0 |       0 |     1 |
| blue    |      1 |       0 |     0 |

In the above example, the original DataFrame contains the `color` column with categorical values. After applying one-hot encoding, three additional columns are created (`blue`, `green`, and `red`) to represent each category. The original `color` column is then dropped, and the encoded columns are concatenated with the original DataFrame.

## Label Encoding

Label Encoding is another technique for encoding categorical variables. It assigns a unique numerical label to each category. However, this method introduces an implicit ordinal relationship that may not exist in the data.

Here is an example of how to perform label encoding in Python, using the `sklearn` library:

```python
from sklearn.preprocessing import LabelEncoder

# Create a list of categorical variables
categories = ['red', 'blue', 'green', 'red', 'blue']

# Create an instance of LabelEncoder
encoder = LabelEncoder()

# Perform label encoding
encoded_categories = encoder.fit_transform(categories)

print(encoded_categories)
```

Output:
```
[2 0 1 2 0]
```

In the above example, we have a list of categorical variables called `categories`. By using the `LabelEncoder` class from `sklearn.preprocessing`, we can perform label encoding. The resulting encoded categories are represented by numerical labels.

## Ordinal Encoding

Ordinal Encoding is similar to label encoding, but it assigns numerical labels in a way that preserves the ordinal relationship between the categories. This method is useful when the categories have a specific order or hierarchy.

Let's see an example of how to perform ordinal encoding in Python, using the `category_encoders` library:

```python
import pandas as pd
import category_encoders as ce

# Create a DataFrame with categorical variables
data = {'size': ['S', 'M', 'L', 'XL', 'M']}
df = pd.DataFrame(data)

# Create an instance of OrdinalEncoder
encoder = ce.OrdinalEncoder(cols=['size'])

# Perform ordinal encoding
df_encoded = encoder.fit_transform(df)

print(df_encoded)
```

Output:

|   size |
|--------|
|      1 |
|      2 |
|      3 |
|      4 |
|      2 |

In the above example, the original DataFrame contains the `size` column with categorical values. By using the `OrdinalEncoder` class from the `category_encoders` library, we can perform ordinal encoding. The size categories are encoded with numerical labels while preserving their ordinal relationship.

## Conclusion

In this blog post, we explored various methods for encoding categorical variables in Python. One-Hot Encoding is suitable when there is no inherent order or hierarchy between categories. Label Encoding and Ordinal Encoding are useful when the categorical variables have an inherent order. Each encoding method has its advantages and disadvantages, so it's essential to choose the appropriate approach based on the data and machine learning task at hand.

To learn more about these techniques and other related topics, refer to the following resources:

- [pandas documentation](https://pandas.pydata.org/pandas-docs/stable/)
- [scikit-learn documentation](https://scikit-learn.org/)
- [category_encoders documentation](https://contrib.scikit-learn.org/category_encoders/index.html)

Now you're equipped with the knowledge to handle categorical variables efficiently in your machine learning projects. Happy encoding!