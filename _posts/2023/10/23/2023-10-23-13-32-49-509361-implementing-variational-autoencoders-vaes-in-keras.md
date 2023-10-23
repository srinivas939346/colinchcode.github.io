---
layout: post
title: "[python] Implementing variational autoencoders (VAEs) in Keras"
description: " "
date: 2023-10-23
tags: [python]
comments: true
share: true
---

Variational Autoencoders (VAEs) are powerful generative models that can learn the underlying distribution of high-dimensional data, such as images or text. They are a variant of the traditional autoencoder architecture that incorporates probabilistic latent variables to capture the data's inherent variability. In this blog post, we will implement a VAE in Keras using the TensorFlow backend. 

## Table of Contents
1. [Introduction to VAEs](#introduction-to-vaes)
2. [Architecture of VAE](#architecture-of-vae)
3. [Implementing VAE in Keras](#implementing-vae-in-keras)
4. [Training the VAE](#training-the-vae)
5. [Generating new samples](#generating-new-samples)
6. [Conclusion](#conclusion)
7. [References](#references)

## Introduction to VAEs

Autoencoders are unsupervised learning models that aim to reconstruct the input data by encoding it into a latent space representation and decoding it back to the original input. VAEs take this concept further by introducing a probabilistic encoder that maps the input data to a latent distribution, and a decoder that generates samples from this latent distribution. The probabilistic nature of VAEs allows them to generate new samples that approximate the original data distribution.

## Architecture of VAE

The architecture of a VAE consists of an encoder network, a latent space, and a decoder network. The encoder network takes the input data and maps it to the mean and variance of the latent distribution. The decoder network samples from this latent distribution and reconstructs the input data. During training, the model is optimized to minimize the reconstruction loss and the Kullback-Leibler divergence between the latent distribution and a prior distribution.

## Implementing VAE in Keras

To implement a VAE in Keras, we need to set up the encoder and decoder networks. The encoder network consists of several dense layers followed by two separate dense layers for the mean and variance of the latent distribution. The decoder network is symmetrical to the encoder, with several dense layers followed by a final layer that outputs the reconstructed data.

```python
# Import necessary libraries
import tensorflow as tf
from tensorflow.keras import layers
from tensorflow.keras import Model

# Define the encoder network
latent_dim = 10

encoder_inputs = tf.keras.Input(shape=(input_dim,))
x = layers.Dense(128, activation='relu')(encoder_inputs)
x = layers.Dense(64, activation='relu')(x)
mean = layers.Dense(latent_dim)(x)
log_var = layers.Dense(latent_dim)(x)

# Define the sampling function for the latent space
def sampling(args):
    mean, log_var = args
    epsilon = tf.keras.backend.random_normal(shape=(tf.keras.backend.shape(mean)[0], latent_dim), mean=0.0, stddev=1.0)
    return mean + tf.keras.backend.exp(log_var / 2) * epsilon

latent_space = layers.Lambda(sampling)([mean, log_var])

# Define the decoder network
x = layers.Dense(64, activation='relu')(latent_space)
x = layers.Dense(128, activation='relu')(x)
decoder_outputs = layers.Dense(input_dim, activation='sigmoid')(x)

# Define the VAE model
vae = Model(encoder_inputs, decoder_outputs)

# Define the loss function to include both the reconstruction loss and KL divergence
reconstruction_loss = tf.keras.losses.binary_crossentropy(encoder_inputs, decoder_outputs) * input_dim
kl_loss = -0.5 * tf.keras.backend.mean(1 + log_var - tf.keras.backend.exp(log_var) - tf.keras.backend.square(mean), axis=-1)
vae_loss = tf.keras.backend.mean(reconstruction_loss + kl_loss)
vae.add_loss(vae_loss)

# Compile and summarize the model
vae.compile(optimizer='adam')
vae.summary()
```

## Training the VAE

To train the VAE, we need a dataset of samples to reconstruct. We can use any suitable dataset based on the problem domain. Here, we will use the MNIST dataset of handwritten digits. We train the model by simply calling the `fit` method on the VAE model with the training dataset.

```python
# Load the MNIST dataset
(x_train, _), (x_test, _) = tf.keras.datasets.mnist.load_data()

# Preprocess the dataset
x_train = x_train.reshape(-1, input_dim) / 255.0
x_test = x_test.reshape(-1, input_dim) / 255.0

# Train the VAE model
vae.fit(x_train, epochs=10, batch_size=32, validation_data=(x_test, None))
```

## Generating new samples

Once the VAE model is trained, we can generate new samples by sampling from the latent space and decoding the samples using the decoder network. We can visualize the generated samples to observe how well the VAE has learned the underlying data distribution.

```python
# Generate new samples from the VAE
num_samples = 10
random_latent_vectors = tf.keras.backend.random_normal(shape=(num_samples, latent_dim))
decoded_samples = vae.decoder.predict(random_latent_vectors)

# Visualize the generated samples
for i in range(num_samples):
    plt.imshow(decoded_samples[i].reshape(28, 28), cmap='gray')
    plt.show()
```

## Conclusion

In this blog post, we have implemented a Variational Autoencoder (VAE) in Keras using the TensorFlow backend. We discussed the architecture of VAEs and how they can be used to generate new samples that approximate the original data distribution. By training the VAE on suitable datasets, we can generate novel and realistic samples from a given data distribution.

## References

- Kingma, D. P., & Welling, M. (2013). Auto-encoding variational bayes. arXiv preprint arXiv:1312.6114.
- Doersch, C. (2016). Tutorial on variational autoencoders. arXiv preprint arXiv:1606.05908.