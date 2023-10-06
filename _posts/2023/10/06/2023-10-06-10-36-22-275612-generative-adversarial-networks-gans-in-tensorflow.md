---
layout: post
title: "[python] Generative adversarial networks (GANs) in TensorFlow"
description: " "
date: 2023-10-06
tags: [python]
comments: true
share: true
---

Generative Adversarial Networks (GANs) are a class of machine learning models that are used to generate new data samples. GANs consist of two main components, a generator and a discriminator, which are trained simultaneously in a competitive setting. The generator learns to generate realistic data samples, while the discriminator learns to distinguish between real and fake samples.

In this blog post, we will explore how to implement GANs using TensorFlow, a popular deep learning library. Specifically, we will focus on training a GAN to generate handwritten digits, using the MNIST dataset.

## Table of Contents
1. [Introduction to GANs](#introduction-to-gans)
2. [Implementing GANs in TensorFlow](#implementing-gans-in-tensorflow)
3. [Training the GAN](#training-the-gan)
4. [Generating New Images](#generating-new-images)
5. [Conclusion](#conclusion)

## Introduction to GANs
Generative Adversarial Networks were introduced by Ian Goodfellow and his colleagues in 2014. GANs have gained significant attention in the machine learning community due to their ability to generate highly realistic and diverse data samples.

A GAN consists of two main components:
- Generator: The generator takes random noise as input and generates new data samples. In the case of generating handwritten digits, the generator would take random noise and output an image of a digit.
- Discriminator: The discriminator is responsible for distinguishing between real and fake samples. It takes an input image and outputs a probability that the image is real (1) or fake (0).

The generator and discriminator are trained in a competitive setting. The generator tries to generate realistic samples to fool the discriminator, while the discriminator learns to become more accurate in distinguishing between real and fake samples. This adversarial training process leads to the generation of realistic samples by the generator.

## Implementing GANs in TensorFlow
To implement GANs in TensorFlow, we need to define the generator and discriminator models, and then train them using an appropriate loss function. Let's take a look at the code snippet below to understand the implementation details:

```python
import tensorflow as tf
from tensorflow.keras import layers

# Define the generator model
def build_generator():
    model = tf.keras.Sequential()
    model.add(layers.Dense(256, input_shape=(100,), activation='relu'))
    model.add(layers.Dense(512, activation='relu'))
    model.add(layers.Dense(784, activation='sigmoid'))
    return model

# Define the discriminator model
def build_discriminator():
    model = tf.keras.Sequential()
    model.add(layers.Dense(512, input_shape=(784,), activation='relu'))
    model.add(layers.Dense(256, activation='relu'))
    model.add(layers.Dense(1, activation='sigmoid'))
    return model

# Define the loss function
cross_entropy = tf.keras.losses.BinaryCrossentropy()

# Define the discriminator loss
def discriminator_loss(real_output, fake_output):
    real_loss = cross_entropy(tf.ones_like(real_output), real_output)
    fake_loss = cross_entropy(tf.zeros_like(fake_output), fake_output)
    total_loss = real_loss + fake_loss
    return total_loss

# Define the generator loss
def generator_loss(fake_output):
    return cross_entropy(tf.ones_like(fake_output), fake_output)

# Instantiate the generator and discriminator models
generator = build_generator()
discriminator = build_discriminator()

```

In the code snippet above, we define `build_generator()` and `build_discriminator()` functions to create the generator and discriminator models, respectively. These models are defined using the `tf.keras.Sequential()` API.

We also define the loss functions `discriminator_loss()` and `generator_loss()`, which will be used to train the models. The discriminator loss is calculated based on the discriminator's ability to correctly classify real and fake samples, while the generator loss is based on its ability to fool the discriminator.

## Training the GAN
Once we have defined the models and loss functions, we can proceed with training the GAN. The training loop involves alternating between training the discriminator and generator models. Here's an example of how the training loop can be structured:

```python
# Define training hyperparameters
num_epochs = 100
batch_size = 128

# Define optimizer for both models
generator_optimizer = tf.keras.optimizers.Adam()
discriminator_optimizer = tf.keras.optimizers.Adam()

for epoch in range(num_epochs):
    for _ in range(num_batches):
        # Train the discriminator
        for _ in range(discriminator_iterations):
            train_discriminator(batch_real_images)

        # Train the generator
        train_generator()

        # Update the discriminator and generator weights
        discriminator_optimizer.apply_gradients(discriminator_gradients)
        generator_optimizer.apply_gradients(generator_gradients)
```

In the code snippet above, we iterate over the desired number of epochs and for each epoch, we iterate over the number of batches. Within each batch, we train the discriminator and generator models.

The `train_discriminator()` function trains the discriminator using a batch of real images as well as a batch of generated fake images. It computes the discriminator loss and calculates the gradients.

The `train_generator()` function trains the generator by generating a batch of fake images and computing the generator loss.

Finally, we update the discriminator and generator weights using the optimizer's `apply_gradients()` function.

## Generating New Images
Once the GAN is trained, we can use the generator model to generate new images. We simply pass random noise as input to the generator and it will produce new samples. Here's an example of how we can generate new images:

```python
# Generate new images
noise = tf.random.normal([num_samples, 100])
generated_images = generator(noise, training=False)

# Display generated images
for i in range(num_samples):
    plt.imshow(generated_images[i], cmap='gray')
    plt.axis('off')
    plt.show()
```

In the code snippet above, we generate random noise using `tf.random.normal()` and pass it as input to the generator to generate new images. We can then display the generated images using a plotting library like Matplotlib.

## Conclusion
In this blog post, we explored how to implement Generative Adversarial Networks (GANs) in TensorFlow. We learned about the generator and discriminator models, the loss functions, and the training process involved in training a GAN. GANs have revolutionized the field of generative modeling and have enabled the generation of realistic and diverse data samples.