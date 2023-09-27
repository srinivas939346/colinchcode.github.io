---
layout: post
title: "[python] Setting up Theano environment"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

Theano is a popular Python library used for deep learning and numerical computation. In order to get started with Theano, you need to set up the environment properly.

## Prerequisites

Make sure you have Python installed on your system. You can download the latest version of Python from the official website - https://www.python.org/downloads/

## Installing Theano

To install Theano, you can use `pip`, the standard package management system for Python. Open your command line or terminal and run the following command:

```
pip install theano
```

This will download and install Theano along with any required dependencies.

## Configuring GPU Support

If you have a GPU and want to utilize its power for faster computation, you need to configure Theano to use the GPU. Follow the steps below:

1. Install the CUDA toolkit from NVIDIA's website - https://developer.nvidia.com/cuda-downloads. Make sure you choose the version compatible with your GPU and operating system.

2. Set the environment variable `THEANO_FLAGS` to enable GPU support. Open your command line or terminal and run the following command:

```
export THEANO_FLAGS=device=cuda
```

Alternatively, you can add the above line to your `.bashrc` or `.bash_profile` file to set the variable permanently.

3. Verify the GPU support by running the following Python code:

```python
import theano
print(theano.config.device)
```

If the output is `gpu`, then Theano is successfully configured to use the GPU.

## Verifying Theano Installation

To verify that Theano is installed correctly, run the following Python code:

```python
import theano
theano.test()
```

This will run a series of tests to ensure that Theano functions properly. If all tests pass without any error or warning, then Theano installation is successful.

## Conclusion

By following the steps mentioned above, you can set up Theano environment on your system. With Theano installed, you can start exploring its powerful features for deep learning and numerical computation tasks.