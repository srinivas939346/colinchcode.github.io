---
layout: post
title: "[python] Principal Component Analysis (PCA)"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Principal Component Analysis (PCA) is a widely used technique in data analysis and machine learning. It is used to reduce the dimensionality of high-dimensional datasets while still maintaining as much information as possible.

PCA works by finding a set of new variables, known as principal components, that are linear combinations of the original features in the dataset. These new variables are uncorrelated, and each successive component captures as much of the remaining variance in the data as possible.

PCA can be applied to a wide range of applications, including image and face recognition, feature extraction, and data visualization. In this blog post, we will discuss the basic steps involved in performing PCA and provide a Python code example.

## Steps in PCA
1. Standardize the data: Before applying PCA, it is important to standardize the data, as PCA is sensitive to the scale of the variables. This involves subtracting the mean from each feature and dividing it by the standard deviation.
2. Compute the covariance matrix: The next step is to compute the covariance matrix of the standardized data. The covariance matrix measures the relationships between the different variables in the dataset.
3. Compute the eigenvectors and eigenvalues: The eigenvectors and eigenvalues of the covariance matrix represent the principal components of the data. The eigenvectors indicate the directions of the maximum variance in the dataset, while the eigenvalues represent the amount of variance explained by each component.
4. Select the principal components: Based on the eigenvalues, we can select the number of principal components to retain. A common approach is to choose the components that explain a certain percentage of the total variance, such as 95%.
5. Transform the data: Finally, we can transform the original data into the new space defined by the selected principal components.

## Python Code Example

```python
import numpy as np
from sklearn.decomposition import PCA

# Step 1: Standardize the data
X = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
X_std = (X - np.mean(X, axis=0)) / np.std(X, axis=0)

# Step 2: Compute the covariance matrix
cov_matrix = np.cov(X_std.T)

# Step 3: Compute the eigenvectors and eigenvalues
eigenvalues, eigenvectors = np.linalg.eig(cov_matrix)

# Step 4: Select the principal components
total_variance = sum(eigenvalues)
explained_variance = [(eigval / total_variance) for eigval in eigenvalues]
cumulative_variance = np.cumsum(explained_variance)
n_components = np.argmax(cumulative_variance >= 0.95) + 1

# Step 5: Transform the data
pca = PCA(n_components=n_components)
X_pca = pca.fit_transform(X_std)
```

In the above code, we first standardize the dataset using numpy's `mean` and `std` functions. We then compute the covariance matrix using numpy's `cov` function. Next, we use numpy's `eig` function to compute the eigenvectors and eigenvalues of the covariance matrix.

To select the principal components, we calculate the explained variance for each component and compute the cumulative variance. We choose the number of components that explain at least 95% of the variance.

Finally, we use scikit-learn's PCA class to perform the dimensionality reduction and transform the original data into the new space.

## Conclusion

PCA is a powerful technique for dimensionality reduction, data visualization, and feature extraction. In this blog post, we discussed the basic steps involved in performing PCA and provided a Python code example.

To learn more about PCA and its applications, refer to the following references:

- Bishop, C. M. (2006). Pattern Recognition and Machine Learning. Springer.
- Jolliffe, I. T. (2002). Principal Component Analysis (2nd ed.). Springer.

Give PCA a try in your own projects and see how it can help you analyze and visualize complex datasets efficiently.