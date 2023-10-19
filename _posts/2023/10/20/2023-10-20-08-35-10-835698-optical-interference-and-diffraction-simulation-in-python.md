---
layout: post
title: "[python] Optical interference and diffraction simulation in Python"
description: " "
date: 2023-10-20
tags: [python]
comments: true
share: true
---

Optical interference and diffraction phenomena are essential concepts in understanding the behavior of light. Simulating these phenomena can aid in better comprehension and visualization of light interactions with various objects. In this blog post, we will explore how to simulate optical interference and diffraction using Python.

## Table of Contents
1. [Wave Superposition](#wave-superposition)
2. [Single Slit Diffraction](#single-slit-diffraction)
3. [Double Slit Interference](#double-slit-interference)
4. [Conclusion](#conclusion)

## 1. Wave Superposition<a name="wave-superposition"></a>
Wave superposition is the combination of two or more waves to form a new wave. In the context of optical interference, this results in constructive or destructive interference depending on the phase of the waves.

To simulate wave superposition in Python, we can use libraries such as NumPy and Matplotlib. Here's an example code snippet that illustrates wave superposition:

```python
import numpy as np
import matplotlib.pyplot as plt

# Define wave properties
amplitude_1 = 1.0
amplitude_2 = 0.8
frequency_1 = 2.0
frequency_2 = 1.5
phase_1 = 0.0
phase_2 = np.pi/2.0

# Create time axis
t = np.linspace(0, 2*np.pi, 1000)

# Calculate waveforms
wave_1 = amplitude_1 * np.sin(2*np.pi*frequency_1*t + phase_1)
wave_2 = amplitude_2 * np.sin(2*np.pi*frequency_2*t + phase_2)
superposition = wave_1 + wave_2

# Plot waveforms
plt.plot(t, wave_1, label='Wave 1')
plt.plot(t, wave_2, label='Wave 2')
plt.plot(t, superposition, label='Superposition')
plt.legend()
plt.xlabel('Time')
plt.ylabel('Amplitude')
plt.title('Wave Superposition')
plt.show()
```

In the above code, we define the properties of two waves (amplitude, frequency, and phase) and then calculate the waveforms using the sine function. Finally, we plot the individual waves and their superposition using the `plot` function from Matplotlib.

## 2. Single Slit Diffraction<a name="single-slit-diffraction"></a>
Single slit diffraction occurs when light passes through a narrow slit, resulting in the spreading of the light waves. To simulate single slit diffraction, we can use the Fresnel-Kirchhoff diffraction equation.

Here's an example code snippet that simulates single slit diffraction using Python and Matplotlib:

```python
import numpy as np
import matplotlib.pyplot as plt

# Define diffraction parameters
wavelength = 500e-9
slit_width = 50e-6
screen_distance = 1.0
screen_width = 2.0

# Create screen grid
x = np.linspace(-screen_width/2, screen_width/2, 1000)

# Calculate intensity using diffraction equation
intensity = (np.sinc(slit_width*x/(wavelength*screen_distance)))**2

# Plot intensity distribution
plt.plot(x, intensity)
plt.xlabel('Distance (m)')
plt.ylabel('Intensity')
plt.title('Single Slit Diffraction')
plt.show()
```

In the above code, we define the parameters of the diffraction experiment and create a grid for the screen. Next, we calculate the intensity at each point using the diffraction equation (`np.sinc` function) and plot the intensity distribution using Matplotlib.

## 3. Double Slit Interference<a name="double-slit-interference"></a>
Double slit interference occurs when light passes through two narrow slits, resulting in an interference pattern. To simulate double slit interference, we can use the concept of wave interference and the superposition of waves.

Here's an example code snippet that simulates double slit interference using Python and Matplotlib:

```python
import numpy as np
import matplotlib.pyplot as plt

# Define interference parameters
wavelength = 500e-9
slit_width = 50e-6
slit_distance = 200e-6
screen_distance = 1.0
screen_width = 2.0

# Create screen grid
x = np.linspace(-screen_width/2, screen_width/2, 1000)

# Assume equal amplitudes for both slits
amplitude = 1.0

# Calculate intensity using interference equation
intensity = (np.cos((np.pi*slit_width*x)/(wavelength*screen_distance)))**2
intensity *= (np.sinc((slit_distance*x)/(wavelength*screen_distance)))**2

# Plot intensity distribution
plt.plot(x, intensity)
plt.xlabel('Distance (m)')
plt.ylabel('Intensity')
plt.title('Double Slit Interference')
plt.show()
```

In the above code, we define the parameters of the interference experiment (wavelength, slit widths, distances, etc.) and create a grid for the screen. Next, we calculate the intensity at each point using the interference equation and plot the intensity distribution using Matplotlib.

## 4. Conclusion<a name="conclusion"></a>
In this blog post, we explored how to simulate optical interference and diffraction phenomena using Python. We covered wave superposition, single slit diffraction, and double slit interference. By implementing these simulations, we can gain a better understanding of the behavior of light and its interactions with various objects.