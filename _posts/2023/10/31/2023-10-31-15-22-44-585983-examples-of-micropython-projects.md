---
layout: post
title: "[python] Examples of MicroPython projects"
description: " "
date: 2023-10-31
tags: [python]
comments: true
share: true
---

MicroPython is a lightweight implementation of the Python programming language that is designed to run on microcontrollers and other resource-constrained devices. It provides an easy and efficient way to program and interact with hardware, making it ideal for various IoT (Internet of Things) projects. In this article, we will explore some examples of MicroPython projects to give you a taste of its capabilities.

## Table of Contents

- [Introduction to MicroPython](#introduction-to-micropython)
- [1. LED Blink](#1-led-blink)
- [2. Temperature and Humidity Monitoring](#2-temperature-and-humidity-monitoring)
- [3. Motion Detection with PIR Sensor](#3-motion-detection-with-pir-sensor)
- [4. Servo Motor Control](#4-servo-motor-control)
- [Conclusion](#conclusion)

## Introduction to MicroPython

MicroPython differs from the standard Python in that it is optimized for microcontrollers and provides a smaller runtime footprint. It offers a subset of the Python features and libraries while still retaining the ease of use and flexibility of the language.

Without further ado, let's dive into some exciting MicroPython projects!

## 1. LED Blink

The classic LED blink project is a great starting point to get familiar with MicroPython. By connecting an LED to a microcontroller, you can use MicroPython to control its state and create various blinking patterns.

Here is a simple example code snippet to blink an LED using MicroPython:

```python
import machine
import time

pin = machine.Pin(2, machine.Pin.OUT)

while True:
    pin.on()
    time.sleep(1)
    pin.off()
    time.sleep(1)
```

In this code, we import the necessary `machine` module, initialize the LED pin as an output pin, and then toggle its state using the `on()` and `off()` methods along with the `time.sleep()` function for delays.

## 2. Temperature and Humidity Monitoring

Using a microcontroller with built-in sensors or external sensors, you can easily read and monitor temperature and humidity data. This can be useful for creating home weather stations or controlling environmental conditions.

Here is a simplified code snippet to read temperature and humidity using MicroPython and a DHT11 sensor:

```python
import dht
import machine

dht_pin = machine.Pin(4)
dht_sensor = dht.DHT11(dht_pin)

while True:
    dht_sensor.measure()
    temperature = dht_sensor.temperature()
    humidity = dht_sensor.humidity()
    print("Temperature: {}°C, Humidity: {}%".format(temperature, humidity))
    time.sleep(2)
```

In this example, we import the `dht` module to interface with the DHT11 sensor, initialize the sensor pin, and then continuously measure and display temperature and humidity readings.

## 3. Motion Detection with PIR Sensor

A PIR (Passive Infrared) sensor can be used to detect motion around a specific area. By connecting a PIR sensor to a microcontroller, we can easily create motion-activated projects like security systems or automatic lighting.

Here is a code snippet to detect motion using MicroPython and a PIR sensor:

```python
import machine

pir_pin = machine.Pin(2, machine.Pin.IN)
led_pin = machine.Pin(4, machine.Pin.OUT)

while True:
    if pir_pin.value() == 1:
        led_pin.on()
    else:
        led_pin.off()
```

In this example, we read the state of the PIR sensor and control an LED accordingly.

## 4. Servo Motor Control

MicroPython can also be used to control servo motors, which are commonly used in robotics and automation projects. By manipulating the pulse width modulation (PWM) signals, you can control the position of the servo motor.

Here is a code snippet to control a servo motor using MicroPython:

```python
import machine
import time

servo_pin = machine.Pin(2)
servo = machine.PWM(servo_pin)
servo.freq(50)

while True:
    servo.duty(40)  # 0° position
    time.sleep(1)
    servo.duty(115)  # 90° position
    time.sleep(1)
    servo.duty(190)  # 180° position
    time.sleep(1)
```

In this example, we initialize the servo pin as PWM, set the PWM frequency, and then control the duty cycle to position the servo at different angles.

## Conclusion

MicroPython offers a straightforward and efficient way to program microcontrollers and create various IoT projects. From simple LED blinking to more complex tasks like sensor monitoring and motor control, MicroPython provides a wide range of capabilities. These examples should give you a good starting point to explore further and unleash your creativity.

If you want to dive deeper into MicroPython, be sure to check out the official MicroPython documentation and explore the vast community of makers and hobbyists who have shared their projects and experiences.

References:
- [MicroPython Documentation](https://docs.micropython.org)
- [MicroPython on GitHub](https://github.com/micropython/micropython)
- [MicroPython Forum](https://forum.micropython.org)