---
layout: post
title: "[python] Using sensors and actuators with MicroPython"
description: " "
date: 2023-10-31
tags: [python]
comments: true
share: true
---

MicroPython is a lean and efficient implementation of the Python programming language that is optimized to run on microcontrollers and other constrained devices. It enables you to write Python code that can interact with sensors and control actuators, allowing you to build a wide range of projects.

In this blog post, we will explore how to use sensors and actuators with MicroPython, including how to interface with common peripherals such as GPIO pins, I2C, and SPI devices.

## Table of Contents
- [Interfacing with GPIO pins](#interfacing-with-gpio-pins)
- [Using I2C devices](#using-i2c-devices)
- [Controlling SPI devices](#controlling-spi-devices)

## Interfacing with GPIO pins

GPIO (General-Purpose Input/Output) pins are a common way to connect sensors and actuators to microcontrollers. MicroPython provides a straightforward API to manipulate GPIO pins, allowing you to read sensor data and control actuators.

To read from a digital sensor connected to a GPIO pin, you can use the `Pin` class in MicroPython. Here's an example of reading a digital input from a button connected to pin `D1`:

```python
from machine import Pin

button_pin = Pin(5, Pin.IN)
if button_pin.value() == 1:
    print("Button pressed!")
```

To control an actuator connected to a GPIO pin, you can use the `Pin` class as well. Here's an example of toggling an LED connected to pin `D2`:

```python
from machine import Pin
import time

led_pin = Pin(4, Pin.OUT)
while True:
    led_pin.on()
    time.sleep(1)
    led_pin.off()
    time.sleep(1)
```

## Using I2C devices

I2C (Inter-Integrated Circuit) is a popular communication protocol for connecting multiple devices to a microcontroller using just two wires. Many sensors and actuators support the I2C interface, and MicroPython provides an I2C module to interact with them.

To use an I2C device with MicroPython, you need to create an `I2C` object and specify the SDA and SCL pins. Here's an example of reading data from a temperature sensor (LM75) connected to a microcontroller with pins `D1` and `D2` used for SDA and SCL:

```python
from machine import Pin, I2C

i2c = I2C(sda=Pin(5), scl=Pin(4))
i2c.writeto(0x48, bytes([0x00]))
data = i2c.readfrom(0x48, 2)
temperature = ((data[0] << 8) | data[1]) / 256
print("Temperature:", temperature, "°C")
```

## Controlling SPI devices

SPI (Serial Peripheral Interface) is another common communication protocol for connecting peripherals to microcontrollers. It enables high-speed communication and is often used for devices such as displays, SD cards, and wireless modules. MicroPython provides an SPI module to interact with SPI devices.

To control an SPI device with MicroPython, you need to create an `SPI` object and specify the communication pins (MOSI, MISO, SCLK) and the chip select pin. Here's an example of writing data to an SPI OLED display module using pins `D1`, `D2`, and `D3`:

```python
from machine import Pin, SPI

spi = SPI(1, baudrate=10000000, sck=Pin(4), mosi=Pin(5), miso=Pin(0))
spi.init()
spi.write(b'\xAF')  # Turn on the display
```

These examples demonstrate how to use sensors and actuators with MicroPython. Make sure to refer to the documentation of specific sensors and peripherals for more detailed instructions on how to interface with them.

Happy hacking with MicroPython!