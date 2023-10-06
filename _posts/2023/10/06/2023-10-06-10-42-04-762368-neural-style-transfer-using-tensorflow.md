---
layout: post
title: "[python] Neural style transfer using TensorFlow"
description: " "
date: 2023-10-06
tags: [python]
comments: true
share: true
---

In recent years, style transfer has gained significant popularity in the field of computer vision. It allows the fusion of content from one image with the style of another image, resulting in an artistic and visually appealing output. Neural style transfer is a technique that uses deep learning to achieve this transformation. In this blog post, we will explore how to perform neural style transfer using TensorFlow.

## Table of Contents
1. [Introduction](#introduction)
2. [Setup](#setup)
3. [Defining the Model](#defining-the-model)
4. [Loading Images](#loading-images)
5. [Calculating Style and Content Features](#calculating-style-and-content-features)
6. [Defining the Loss Functions](#defining-the-loss-functions)
7. [Training the Model](#training-the-model)
8. [Generating the Output](#generating-the-output)
9. [Conclusion](#conclusion)

## Introduction
Neural style transfer is based on the idea that deep neural networks are capable of extracting both content and style features from images. It involves taking a content image and a style image, and then optimizing another image to minimize the content loss, which measures how different the features of the generated image are from the features of the content image, and the style loss, which measures how different the features of the generated image are from the features of the style image.

## Setup
To get started, you will need to install TensorFlow and import the necessary libraries. Create a new Python environment and install TensorFlow using pip:

```python
pip install tensorflow
```

## Defining the Model
Neural style transfer utilizes a pre-trained convolutional neural network (CNN) model. In this example, we will use the VGG19 model, which has proven to be effective for style transfer tasks. The model can be loaded and its architecture can be accessed using TensorFlow's Keras API:

```python
from tensorflow.keras.applications import VGG19

model = VGG19(weights='imagenet', include_top=False)
```

## Loading Images
To load the content and style images, you can use the `load_img` function from TensorFlow's `keras.preprocessing.image` module. This function loads the image and resizes it to the specified dimensions:

```python
from tensorflow.keras.preprocessing.image import load_img

content_image = load_img('content.jpg', target_size=(224, 224))
style_image = load_img('style.jpg', target_size=(224, 224))
```

## Calculating Style and Content Features
Once the images are loaded, we can preprocess them to obtain the style and content features. The VGG19 model, specifically its convolutional layers, can be used to calculate the features. By passing the images through the model, we can extract the output of specific layers that capture both style and content information:

```python
from tensorflow.keras.applications.vgg19 import preprocess_input
from tensorflow.keras.models import Model

def get_feature_representations(model, content_image, style_image):
    # Preprocess the images
    content_image = preprocess_input(content_image)
    style_image = preprocess_input(style_image)

    # Generate content and style feature representations
    content_features = model(content_image)
    style_features = model(style_image)

    return content_features, style_features

content_features, style_features = get_feature_representations(model, content_image, style_image)
```

## Defining the Loss Functions
The content loss is calculated as the mean squared error between the content features of the generated image and the content features of the content image. The style loss is calculated as the mean squared error between the Gram matrices of the style features of the generated image and the style features of the style image. These loss functions are used to optimize the generated image:

```python
def compute_content_loss(content_features, generated_image_features):
    return tf.reduce_mean(tf.square(content_features - generated_image_features))

def gram_matrix(input_tensor):
    # Calculate the Gram matrix
    result = tf.linalg.einsum('bijc,bijd->bcd', input_tensor, input_tensor)
    input_shape = tf.shape(input_tensor)
    num_locations = tf.cast(input_shape[1] * input_shape[2], tf.float32)
    return result / num_locations

def compute_style_loss(style_features, generated_image_features):
    style_gram = gram_matrix(style_features)
    generated_image_gram = gram_matrix(generated_image_features)
    return tf.reduce_mean(tf.square(style_gram - generated_image_gram))

# Define the total loss as a weighted sum of the content and style losses
def compute_total_loss(model, generated_image, content_features, style_features, content_weight, style_weight):
    generated_image_features = model(generated_image)
    content_loss = compute_content_loss(content_features, generated_image_features)
    style_loss = compute_style_loss(style_features, generated_image_features)
    total_loss = content_weight * content_loss + style_weight * style_loss
    return total_loss
```

## Training the Model
To optimize the generated image and minimize the loss, we can use gradient descent. TensorFlow provides the `tf.GradientTape` API to compute gradients of the loss function with respect to the generated image:

```python
def compute_grads(model, generated_image, content_features, style_features, content_weight, style_weight):
    with tf.GradientTape() as tape:
        # Calculate the total loss
        loss = compute_total_loss(model, generated_image, content_features, style_features, content_weight, style_weight)
    # Calculate the gradients of the loss with respect to the generated image
    grads = tape.gradient(loss, generated_image)
    return grads

def run_style_transfer(model, content_image, style_image, num_iterations=1000, content_weight=1e3, style_weight=1e-2):
    # Initialize the generated image as the content image
    generated_image = tf.Variable(content_image, dtype=tf.float32)

    # Extract the content and style features
    content_features, style_features = get_feature_representations(model, content_image, style_image)

    # Optimization loop
    optimizer = tf.optimizers.Adam(learning_rate=5, beta_1=0.99, epsilon=1e-1)
    best_loss, best_img = float("inf"), None
    for i in range(num_iterations):
        grads = compute_grads(model, generated_image, content_features, style_features, content_weight, style_weight)
        optimizer.apply_gradients([(grads, generated_image)])
        clipped_image = tf.clip_by_value(generated_image, clip_value_min=0.0, clip_value_max=1.0)
        generated_image.assign(clipped_image)

        if loss < best_loss:
            best_loss = loss
            best_image = generated_image.numpy()

    return best_image
```

## Generating the Output
Finally, we can generate the stylized image by running the style transfer algorithm and saving the output:

```python
# Run style transfer
output_image = run_style_transfer(model, content_image, style_image)

# Save the output image
tf.keras.preprocessing.image.save_img('output.jpg', output_image)
```

## Conclusion
Neural style transfer is an exciting technique that combines the content of one image with the style of another to create stunning visual outputs. In this blog post, we have explored how to perform neural style transfer using TensorFlow. By leveraging pre-trained models like VGG19 and optimizing a generated image to minimize the content and style loss, we can obtain impressive results. Experiment with different content and style images to unleash your artistic creations!

**Note**: The complete code example can be found [here](https://github.com/your-repo/style_transfer.py).

**Sources**:
- Neural Style Transfer: [https://arxiv.org/abs/1508.06576](https://arxiv.org/abs/1508.06576)
- TensorFlow: [https://www.tensorflow.org/](https://www.tensorflow.org/)