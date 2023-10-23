---
layout: post
title: "[python] Semantic segmentation using Keras"
description: " "
date: 2023-10-23
tags: [python]
comments: true
share: true
---

Semantic segmentation is a computer vision task that involves dividing an image into different regions or segments, where each segment represents a specific object or class. In this tutorial, we will explore how to perform semantic segmentation using Keras, a popular deep learning framework.

## Table of Contents

- [Introduction to Semantic Segmentation](#introduction-to-semantic-segmentation)
- [Setting up the Environment](#setting-up-the-environment)
- [Data Preparation](#data-preparation)
- [Building the Model](#building-the-model)
- [Training the Model](#training-the-model)
- [Evaluation and Inference](#evaluation-and-inference)
- [Conclusion](#conclusion)

## Introduction to Semantic Segmentation

Semantic segmentation differs from object detection or classification tasks as it assigns a label to every pixel in an image. This is useful in various computer vision applications such as autonomous driving, medical image analysis, and scene understanding.

The popular deep learning library Keras provides a simple and efficient way to implement semantic segmentation models. We will be using a convolutional neural network (CNN) architecture called U-Net, which has been widely used for semantic segmentation tasks.

## Setting up the Environment

To get started, we need to set up our development environment. Make sure you have the following dependencies installed:

- Python 3.x
- Keras
- TensorFlow

You can install Keras and TensorFlow using the following command:

```bash
$ pip install keras tensorflow
```

## Data Preparation

Semantic segmentation models require a dataset with annotated images. There are several datasets available online, such as the PASCAL VOC dataset or the Cityscapes dataset. For the sake of simplicity, let's assume we have a dataset stored in the `data` directory, containing the input images and their corresponding semantic masks.

We need to preprocess the data by resizing the images and masks to a consistent size. Additionally, we should convert the masks into one-hot encoded format to match the output shape of our model.

Here's an example code snippet to perform the data preparation:

```python
from PIL import Image
import numpy as np

def preprocess_data(image_path, mask_path):
    input_image = Image.open(image_path)
    input_mask = Image.open(mask_path)

    input_image = input_image.resize((256, 256))
    input_mask = input_mask.resize((256, 256))

    input_image = np.array(input_image)
    input_mask = np.array(input_mask)

    # Convert mask to one-hot encoded format
    num_classes = len(np.unique(input_mask))
    mask_shape = input_mask.shape
    one_hot_mask = np.zeros((mask_shape[0], mask_shape[1], num_classes), dtype=np.int)
    for i, class_id in enumerate(np.unique(input_mask)):
        one_hot_mask[..., i][input_mask == class_id] = 1

    return input_image, one_hot_mask
```

## Building the Model

We will be using the U-Net architecture, which is known for its effectiveness in semantic segmentation tasks. U-Net follows an encoder-decoder approach, where the encoder downsamples the input image, and the decoder upsamples the feature maps to obtain the segmentation mask.

Here's an example code snippet to build the U-Net model using Keras:

```python
from tensorflow.keras.models import Model
from tensorflow.keras.layers import Input, Conv2D, MaxPooling2D, Dropout, UpSampling2D, Concatenate

def build_model():
    inputs = Input((256, 256, 3))

    # Encoder
    conv1 = Conv2D(64, 3, activation='relu', padding='same')(inputs)
    conv1 = Conv2D(64, 3, activation='relu', padding='same')(conv1)
    pool1 = MaxPooling2D(pool_size=(2, 2))(conv1)

    # Decoder
    conv6 = Conv2D(1024, 3, activation='relu', padding='same')(pool5)
    conv6 = Conv2D(1024, 3, activation='relu', padding='same')(conv6)
    up7 = UpSampling2D(size=(2, 2))(conv6)
    conv7 = Conv2D(512, 2, activation='relu', padding='same')(up7)
    conv7 = Concatenate()([conv4, conv7])

    # Output
    outputs = Conv2D(num_classes, 1, activation='softmax')(conv7)

    model = Model(inputs=[inputs], outputs=[outputs])
    model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])

    return model
```

## Training the Model

To train the model, we need a training set and corresponding target masks. We will split our dataset into training and validation sets and use Keras' `fit` function to train the model.

```python
def train_model():
    # Load and preprocess the training data
    x_train, y_train = preprocess_data('data/train/image.jpg', 'data/train/mask.jpg')

    # Split into training and validation sets
    split_index = int(len(x_train) * 0.8)
    x_train, x_val = x_train[:split_index], x_train[split_index:]
    y_train, y_val = y_train[:split_index], y_train[split_index:]

    # Build and compile the model
    model = build_model()

    # Train the model
    model.fit(x_train, y_train, batch_size=16, epochs=10, validation_data=(x_val, y_val))
```

## Evaluation and Inference

After training the model, you can evaluate its performance on a test set using Keras' `evaluate` function.

```python
def evaluate_model():
    # Load and preprocess the test data
    x_test, y_test = preprocess_data('data/test/image.jpg', 'data/test/mask.jpg')

    # Build and compile the model
    model = build_model()

    # Load the trained weights
    model.load_weights('model_weights.h5')

    # Evaluate the model
    loss, accuracy = model.evaluate(x_test, y_test)
    print(f"Test Loss: {loss}")
    print(f"Test Accuracy: {accuracy}")
```

To perform inference on new images, you can use the trained model to predict the segmentation mask.

```python
def perform_inference():
    # Load and preprocess the input image
    input_image, _ = preprocess_data('data/input/image.jpg', 'data/input/mask.jpg')

    # Build and compile the model
    model = build_model()

    # Load the trained weights
    model.load_weights('model_weights.h5')

    # Perform inference
    predicted_mask = model.predict(np.expand_dims(input_image, axis=0))
```

## Conclusion

In this tutorial, we learned how to perform semantic segmentation using Keras. We used the U-Net architecture and trained the model on a dataset of annotated images. By leveraging Keras' simplicity and efficiency, we were able to build a semantic segmentation model and perform evaluation and inference. Semantic segmentation is a powerful technique in computer vision that has numerous applications in various domains.