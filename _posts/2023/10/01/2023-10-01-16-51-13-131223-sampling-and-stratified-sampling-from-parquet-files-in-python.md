---
layout: post
title: "[python] Sampling and stratified sampling from Parquet files in Python"
description: " "
date: 2023-10-01
tags: [python]
comments: true
share: true
---

In data analysis or machine learning tasks, it is often necessary to work with a large dataset. However, processing such large datasets can be time-consuming and computationally expensive. One way to overcome this challenge is to work with a sample of the dataset rather than the entire dataset.

In this blog post, we will explore how to sample data from Parquet files in Python using the `pandas` and `fastparquet` libraries. Additionally, we will discuss the concept of stratified sampling and demonstrate how to perform stratified sampling from Parquet files.

### Table of Contents

1. [Introduction to Parquet Files](#introduction-to-parquet-files)
2. [Sampling from Parquet Files](#sampling-from-parquet-files)
3. [Stratified Sampling from Parquet Files](#stratified-sampling-from-parquet-files)
4. [Conclusion](#conclusion)

### Introduction to Parquet Files

Parquet is a columnar storage file format specifically designed for big data processing in tools like Apache Spark, Apache Hive, and Apache Impala. Parquet files are highly compressed and optimized for data processing performance. They are especially useful for working with large datasets.

To work with Parquet files in Python, we can use the `pandas` library along with the `fastparquet` library for efficient Parquet file reading and writing.

### Sampling from Parquet Files

Sampling refers to the process of selecting a representative subset from a larger dataset. This subset can be used for various purposes, such as exploratory data analysis or model training. Sampling from Parquet files can be done using the following steps:

1. Load the Parquet file into a `pandas` DataFrame using `pd.read_parquet()`.
2. Use the `sample()` method of the DataFrame to randomly select a specified number or fraction of rows.

Here is an example code snippet that demonstrates how to sample from a Parquet file in Python:

```python
import pandas as pd

# Load Parquet file into DataFrame
df = pd.read_parquet('path/to/file.parquet')

# Sample 10% of the rows
sampled_df = df.sample(frac=0.1, random_state=42)
```

In the above code, we first load the Parquet file into a DataFrame using the `pd.read_parquet()` function. Then, we use the `sample()` method of the DataFrame to randomly select 10% of the rows, setting the `frac` parameter to 0.1.

### Stratified Sampling from Parquet Files

Stratified sampling is a sampling technique where the population is divided into distinct groups called strata, and samples are randomly selected from each stratum. This technique ensures that each stratum is represented in the final sample, making it useful when dealing with imbalanced datasets.

To perform stratified sampling from a Parquet file, we can follow these steps:

1. Load the Parquet file into a DataFrame.
2. Determine the strata based on specific criteria or columns.
3. Use the `groupby()` method to group the DataFrame based on the strata.
4. Apply the `sample()` method to each group to select samples from each stratum.
5. Concatenate the sampled groups into a single DataFrame.

Here is an example code snippet that demonstrates how to perform stratified sampling from a Parquet file in Python:

```python
import pandas as pd

# Load Parquet file into DataFrame
df = pd.read_parquet('path/to/file.parquet')

# Determine strata based on a column
strata_col = 'category'
strata_values = df[strata_col].unique()

# Apply stratified sampling
sampled_dfs = []
for stratum in strata_values:
    stratum_df = df[df[strata_col] == stratum]
    sampled_stratum_df = stratum_df.sample(n=100, random_state=42)  # Sample 100 rows from each stratum
    sampled_dfs.append(sampled_stratum_df)

# Concatenate sampled DataFrames
stratified_sampled_df = pd.concat(sampled_dfs)
```

In the above code, we first load the Parquet file into a DataFrame. Then, we determine the strata based on a specific column. In this example, we use the 'category' column as the stratifying variable.

Next, we apply stratified sampling by iterating over each stratum, filtering the DataFrame for that stratum, and selecting a sample of 100 rows using the `sample()` method.

Finally, we concatenate the sampled DataFrames from each stratum into a single DataFrame using the `pd.concat()` function to obtain the stratified sample.

### Conclusion

In this blog post, we learned how to sample data from Parquet files in Python using the `pandas` and `fastparquet` libraries. We also explored the concept of stratified sampling and demonstrated how to perform stratified sampling from Parquet files.

Sampling can be a powerful technique when working with large datasets, allowing us to gain insights and train models efficiently. By leveraging the capabilities of Parquet files and the flexibility of Python libraries, we can make our data analysis process more streamlined and resource-efficient.