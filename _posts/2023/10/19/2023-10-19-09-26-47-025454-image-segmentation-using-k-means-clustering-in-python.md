---
layout: post
title: "[python] Image segmentation using K-means clustering in Python."
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

Image segmentation is the process of partitioning an image into multiple segments or regions to simplify the representation of an image. It is a crucial step in various computer vision applications, such as object recognition, image editing, and medical image analysis.

**K-means clustering** is a popular unsupervised learning algorithm used for clustering data points into groups or clusters. It assigns each data point to the cluster whose mean value is closest to that data point. In the context of image segmentation, K-means clustering can be applied to group similar pixels together.

In this article, we will walk through the process of using K-means clustering for image segmentation in Python.

## Table of Contents
1. [Loading the Image](#loading-the-image)
2. [Preprocessing the Image](#preprocessing-the-image)
3. [Performing K-means Clustering](#performing-k-means-clustering)
4. [Displaying the Segmented Image](#displaying-the-segmented-image)
5. [Conclusion](#conclusion)

## Loading the Image <a name="loading-the-image"></a>

Before we can perform image segmentation, we need to load the image into our Python program. We can use the `PIL` library to open and read the image.

```python
from PIL import Image

# Open the image
image = Image.open('image.jpg')
```

## Preprocessing the Image <a name="preprocessing-the-image"></a>

Image preprocessing involves performing some initial cleaning and transformation on the image to improve the quality of the segmentation results. In this step, we will convert the image to grayscale to simplify the clustering process.

```python
# Convert the image to grayscale
gray_image = image.convert('L')
```

## Performing K-means Clustering <a name="performing-k-means-clustering"></a>

Now that we have our preprocessed image, we can apply K-means clustering to segment the image. We will use the `scikit-learn` library to perform the clustering.

```python
import numpy as np
from sklearn.cluster import KMeans

# Convert the image into a NumPy array
image_array = np.array(gray_image)

# Reshape the array into a 2D shape
reshaped_array = image_array.reshape((-1, 1))

# Perform K-means clustering with k=2
kmeans = KMeans(n_clusters=2)
kmeans.fit(reshaped_array)

# Get the labels assigned by the clustering algorithm
labels = kmeans.labels_
```

## Displaying the Segmented Image <a name="displaying-the-segmented-image"></a>

Finally, we can display the segmented image using the original image and the labels we obtained from K-means clustering.

```python
import matplotlib.pyplot as plt

# Reshape the labels array back to the original image shape
segmented_image_array = labels.reshape(image_array.shape)

# Create a new PIL image using the segmented image array
segmented_image = Image.fromarray(segmented_image_array.astype(np.uint8))

# Display the original and segmented images side by side
fig, axes = plt.subplots(1, 2, figsize=(10, 5))
axes[0].imshow(image)
axes[0].set_title('Original Image')
axes[1].imshow(segmented_image, cmap='gray')
axes[1].set_title('Segmented Image')
plt.show()
```

## Conclusion <a name="conclusion"></a>

In this tutorial, we learned how to perform image segmentation using K-means clustering in Python. We loaded the image, preprocessed it, applied K-means clustering, and displayed the segmented image. Image segmentation is a powerful technique that finds applications in various fields, and K-means clustering provides a simple and effective way to achieve it.

**References:**
- [scikit-learn documentation](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html)
- [PIL (Python Imaging Library) documentation](https://pillow.readthedocs.io/en/stable/)
- [matplotlib documentation](https://matplotlib.org/)