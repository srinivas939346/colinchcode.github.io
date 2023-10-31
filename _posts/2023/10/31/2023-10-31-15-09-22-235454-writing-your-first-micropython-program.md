---
layout: post
title: "[python] Writing your first MicroPython program"
description: " "
date: 2023-10-31
tags: [python]
comments: true
share: true
---
MicroPython is a lightweight implementation of the Python programming language that is optimized to run on microcontrollers. It is a great choice for projects that require low power consumption and have limited hardware resources. In this article, we will cover the steps to write your first MicroPython program.

## Prerequisites
Before getting started, you will need the following:

1. A microcontroller board that supports MicroPython. Some popular options include the ESP32 and the Pyboard.
2. A USB cable to connect the microcontroller board to your computer.
3. MicroPython firmware specific to your microcontroller board. You can find the firmware on the official MicroPython website.

## Step 1: Flashing the MicroPython firmware
The first step is to flash the MicroPython firmware onto your microcontroller board. This process may vary depending on your board, so it is important to refer to the documentation provided with your board. In general, the steps involve connecting your board to your computer via USB, entering the bootloader mode, and using a tool such as esptool or stm32flash to flash the firmware.

## Step 2: Connecting to the MicroPython REPL
Once the firmware is flashed, you can connect to the MicroPython Read-Eval-Print Loop (REPL) to interact with the board. To do this, open a terminal or command prompt and navigate to the folder where you downloaded the MicroPython firmware. Connect your board to your computer using a USB cable.

For boards such as the ESP32, you can use a tool like picocom or screen to connect to the REPL. For example, on Linux, you can use the following command:
```
picocom -b 115200 /dev/ttyUSB0
```
On Windows, you can use a tool like PuTTY.

For boards like the Pyboard, you can use a serial communication software such as PuTTY or Minicom.

## Step 3: Writing and running your program
With the REPL connected, you can start writing and running your MicroPython program. The REPL allows you to enter Python code one line at a time and see the results immediately. This is a great way to experiment and test your code.

To write a program that runs independently, you can write your code in a file with a `.py` extension and upload it to the microcontroller. To do this, you will need a way to transfer files to the microcontroller, such as a tool like `ampy` or using a serial terminal.

For example, assume you want to blink an LED connected to pin 13 on your microcontroller board. You can write the following code and save it as `blink.py`:

```python
import machine
import time

led = machine.Pin(13, machine.Pin.OUT)

while True:
    led.value(1)
    time.sleep(1)
    led.value(0)
    time.sleep(1)
```

To run the program, upload `blink.py` to your microcontroller using your preferred method. Once uploaded, the program will start running, and you should see the LED blinking.

## Conclusion
Writing your first MicroPython program is a great way to start exploring the world of microcontrollers. MicroPython's simplicity and compatibility with Python make it an excellent choice for beginners and professionals alike. Once you have mastered the basics, you can start building more complex projects and exploring the vast possibilities offered by MicroPython.

**References:**
- [MicroPython documentation](https://docs.micropython.org/en/latest/)
- [MicroPython official website](https://micropython.org/)