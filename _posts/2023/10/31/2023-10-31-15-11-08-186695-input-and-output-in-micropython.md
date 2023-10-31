---
layout: post
title: "[python] Input and output in MicroPython"
description: " "
date: 2023-10-31
tags: [python]
comments: true
share: true
---

MicroPython is a lightweight implementation of the Python programming language that is designed for microcontrollers and embedded systems. In this article, we will explore how to perform input and output operations in MicroPython.

## Input Operations

### Reading from the Console

To read input from the console in MicroPython, we can use the `input()` function. This function waits for the user to enter some text and returns the entered text as a string.

```python
name = input("Enter your name: ")
print("Hello, " + name + "!")
```

In the above example, the `input()` function prompts the user with the message "Enter your name: ". The entered name is then stored in the variable `name`, and it is printed with a greeting message.

### Reading from Sensors

MicroPython provides various libraries and modules to interface with sensors and devices. Depending on the specific hardware and sensor you are using, you can refer to the documentation or libraries provided by the sensor manufacturer to read data from sensors.

## Output Operations

### Printing to the Console

To display output on the console in MicroPython, we can use the `print()` function. This function takes one or more arguments and prints them out as text.

```python
print("Hello, World!")
```

In the above example, the `print()` function displays the message "Hello, World!" on the console.

### Controlling LEDs

Controlling LEDs is a common task in embedded systems. MicroPython provides libraries to control GPIO pins on microcontrollers, which can be used to control LEDs.

```python
import machine
import time

led_pin = machine.Pin(2, machine.Pin.OUT)

while True:
    led_pin.on()
    time.sleep(1)
    led_pin.off()
    time.sleep(1)
```

In the above example, we import the `machine` module to access the GPIO functionality. We create a `Pin` object for the GPIO pin connected to the LED (in this case, pin 2). We then toggle the state of the pin using the `on()` and `off()` methods, with a delay of 1 second between each state change.

## Conclusion

Input and output operations are essential for any programming language, including MicroPython. In this article, we have looked at how to perform input operations such as reading from the console and sensors, and output operations such as printing messages and controlling LEDs. With these capabilities, you can effectively interact with users and interfaces in your MicroPython projects.

## References

- [MicroPython Documentation](https://docs.micropython.org/)
- [MicroPython GitHub Repository](https://github.com/micropython/micropython)