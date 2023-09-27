---
layout: post
title: "[python] Theano for text generation"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

**Introduction**

Text generation is a popular application in the field of natural language processing (NLP). It involves creating new text based on a given set of input text or a language model. In this blog post, we will explore how to use Theano, a popular deep learning library, for text generation applications.

**What is Theano?**

Theano is a powerful Python library that allows efficient mathematical computations involving multi-dimensional arrays. It is widely used in machine learning and deep learning research due to its efficient implementation of automatic differentiation and GPU support.

**Preparing the Data**

Before we start generating text with Theano, we need to prepare our input data. In the case of text generation, we typically use a large corpus of text as our training data. This could be a collection of books, articles, or any other text source.

We need to tokenize the text, convert it into numerical format, and create sequences of words that will serve as the input for our model. The input sequences will then be used to predict the next word in the text.

**Building the Text Generation Model**

To build our text generation model, we will use a recurrent neural network (RNN) with LSTM (Long Short-Term Memory) cells. Theano provides a flexible framework for building neural networks, making it suitable for this task.

First, we import the necessary libraries and define the architecture of our model. We initialize the input and output layers, and add LSTM cells to the model. We then compile the model by specifying the loss function and optimizer.

```python
import theano
import theano.tensor as T
import numpy as np
from theano import function
from theano import shared
import random

# Define the architecture of the model
input_layer = T.matrix('input')
output_layer = T.matrix('output')

hidden_size = 128
vocab_size = 10000

Wxh = shared(np.random.randn(hidden_size, vocab_size) * 0.01, name='Wxh')
Whh = shared(np.random.randn(hidden_size, hidden_size) * 0.01, name='Whh')
Why = shared(np.random.randn(vocab_size, hidden_size) * 0.01, name='Why')
bh = shared(np.zeros((hidden_size, 1)), name='bh')
by = shared(np.zeros((vocab_size, 1)), name='by')

# Define the forward pass of the model
def rnn_forward(inputs):
    hidden_state = T.zeros((hidden_size, 1))

    for i in range(len(inputs)):
        input_word = inputs[i]
        hidden_state = T.tanh(T.dot(Wxh, input_word) + T.dot(Whh, hidden_state) + bh)
        output = T.softmax(T.dot(Why, hidden_state) + by)

    return output

# Compile the model
output = rnn_forward(input_layer)
loss = T.mean(T.nnet.categorical_crossentropy(output, output_layer))

grads = T.grad(loss, [Wxh, Whh, Why, bh, by])

```

**Training the Text Generation Model**

Now that our model is defined, we can proceed to train it using our prepared training data. The training process involves updating the model weights based on the input sequences and the corresponding target (the next word in the sequence).

We define a training function that takes in the input and target data, and updates the model weights using the Adam optimizer. We iterate through the input sequences and calculate the loss at each step. Finally, we update the model weights using the gradients calculated earlier.

```python

# Define the training function
learning_rate = 0.01

updates = []
for param, grad in zip([Wxh, Whh, Why, bh, by], grads):
    updates.append((param, param - learning_rate * grad))

train = theano.function([input_layer, output_layer], loss, updates=updates)

# Train the model
num_epochs = 100
batch_size = 32

for epoch in range(num_epochs):
    epoch_loss = 0
    num_batches = 0

    for i in range(0, len(training_data), batch_size):
        inputs = training_data[i:i+batch_size]
        targets = training_targets[i:i+batch_size]
      
        batch_loss = train(inputs, targets)
      
        epoch_loss += batch_loss
        num_batches += 1

    average_loss = epoch_loss / num_batches
    print(f"Epoch {epoch+1}: Average Loss = {average_loss}")

```

**Generating Text**

Once the model is trained, we can start generating text using the learned weights. We give the model a seed sequence and let it predict the next word. We then append the predicted word to the sequence and repeat the process to generate the desired amount of text.

```python

# Generate text
def generate_text(seed_sequence, num_words):
    seed = seed_sequence
    hidden_state = T.zeros((hidden_size, 1))
    generated_text = seed_sequence.copy()

    for _ in range(num_words):
        input_word = seed[-1]
        hidden_state = T.tanh(T.dot(Wxh, input_word) + T.dot(Whh, hidden_state) + bh)
        output = T.softmax(T.dot(Why, hidden_state) + by)

        # Sample the next word from the output distribution
        next_word = np.random.choice(range(vocab_size), p=output.flatten())

        generated_text.append(next_word)
        seed = generated_text[-order:]

    return generated_text

# Set the seed sequence and generate text
seed_sequence = [1, 2, 3, 4] # Example seed sequence
num_words = 20

generated_text = generate_text(seed_sequence, num_words)
print(generated_text)

```

**Conclusion**

In this blog post, we explored how to use Theano for text generation applications. We built a language model using a recurrent neural network with LSTM cells, trained the model using our prepared data, and generated text using the learned weights. Theano provides a flexible and efficient framework for building deep learning models and is a powerful tool for NLP tasks like text generation.