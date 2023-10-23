---
layout: post
title: "[python] Implementing generative adversarial networks (GANs) in Keras"
description: " "
date: 2023-10-23
tags: [python]
comments: true
share: true
---

In this tutorial, we will explore how to implement Generative Adversarial Networks (GANs) using the Keras library. GANs are a type of generative model that can generate new samples similar to a training dataset. They consist of two main components: a generator and a discriminator. The generator tries to generate realistic samples to fool the discriminator, while the discriminator tries to differentiate between real and generated samples.

Let's get started by installing the required libraries:

```bash
pip install tensorflow keras
```

Next, we will import the necessary libraries in Python:

```python
import numpy as np
from keras.models import Sequential
from keras.layers import Dense
from keras.optimizers import Adam
```

## Dataset

For this tutorial, we will use a simple dataset of random numbers. However, you can replace it with any other dataset of your choice. We will generate 1000 random numbers between 0 and 1 as our training dataset:

```python
np.random.seed(42)
random_data = np.random.rand(1000, 1)
```

## Generator Model

The generator model takes random noise as input and generates fake samples. It consists of a few fully connected layers with activation functions. Here is the code to define the generator model:

```python
def create_generator():
    generator = Sequential()
    generator.add(Dense(32, input_shape=(100,), activation='relu'))
    generator.add(Dense(64, activation='relu'))
    generator.add(Dense(1, activation='sigmoid'))
    generator.compile(loss='binary_crossentropy', optimizer='adam')
    return generator

generator = create_generator()
```

## Discriminator Model

The discriminator model takes a sample as input and outputs the probability of it being real or fake. It also consists of a few fully connected layers with activation functions. Here is the code to define the discriminator model:

```python
def create_discriminator():
    discriminator = Sequential()
    discriminator.add(Dense(64, input_shape=(1,), activation='relu'))
    discriminator.add(Dense(32, activation='relu'))
    discriminator.add(Dense(1, activation='sigmoid'))
    discriminator.compile(loss='binary_crossentropy', optimizer='adam')
    return discriminator

discriminator = create_discriminator()
```

## GAN Model

The GAN model combines both the generator and discriminator models. It first generates a sample using the generator and then uses the discriminator to classify it as real or fake. Here is the code to define the GAN model:

```python
def create_gan(generator, discriminator):
    gan = Sequential()
    gan.add(generator)
    discriminator.trainable = False
    gan.add(discriminator)
    gan.compile(loss='binary_crossentropy', optimizer='adam')
    return gan

gan = create_gan(generator, discriminator)
```

## Training

Now, we can train our GAN model. The training process consists of alternating between training the discriminator and the generator. In each iteration, we first train the discriminator on real samples, then on generated samples. Next, we train the generator by generating fake samples and trying to fool the discriminator. Here is the code for the training loop:

```python
def train_gan(gan, generator, discriminator, data):
    for epoch in range(epochs):
        # Train discriminator
        real_samples = data
        fake_samples = generator.predict(np.random.rand(batch_size, 100))
        discriminator_loss_real = discriminator.train_on_batch(real_samples, np.ones((batch_size, 1)))
        discriminator_loss_fake = discriminator.train_on_batch(fake_samples, np.zeros((batch_size, 1)))
        discriminator_loss = 0.5 * np.add(discriminator_loss_real, discriminator_loss_fake)

        # Train generator
        generator_loss = gan.train_on_batch(np.random.rand(batch_size, 100), np.ones((batch_size, 1)))

        # Print progress
        print(f"Epoch: {epoch+1}/{epochs}, Discriminator Loss: {discriminator_loss}, Generator Loss: {generator_loss}")

train_gan(gan, generator, discriminator, random_data)
```

## Conclusion

In this tutorial, we implemented a simple GAN using Keras. GANs are a powerful technique for generating new samples similar to a training dataset. You can further enhance the models by adding more layers, filters, or using different activation functions. Experiment with different datasets and parameters to generate diverse and realistic samples.

## References

- [Goodfellow, I., Pouget-Abadie, J., Mirza, M., Xu, B., Warde-Farley, D., Ozair, S., ... & Bengio, Y. (2014). Generative adversarial networks. arXiv preprint arXiv:1406.2661.](https://arxiv.org/abs/1406.2661)
- [Keras Documentation](https://keras.io/)