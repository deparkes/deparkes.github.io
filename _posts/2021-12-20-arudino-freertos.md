---
layout: post
title: Arduino FreeRTOS
date: 2021-12-20 20:07:21.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- arduino
- c
- free rtos
- hardware
- iot
- python
- rtos
- usb
author:
  display_name: deparkes
permalink: "/2021/12/20/arudino-freertos/"
---
I was interested to follow <a href="https://feilipu.me/2015/11/24/arduino_freertos/">this guide</a> to doing an Arduino FreeRTOS install. It's a good tutorial and my post here just adds a few more notes around areas that didn't immediately make sense to me.
Also <a href="https://github.com/feilipu/Arduino_FreeRTOS_Library">check out the Arduino FreeRTOS source code on GitHub</a>


<h2>Arduino FreeRTOS</h2>
This section has a few notes about following <a href="https://feilipu.me/2015/11/24/arduino_freertos/">the guide</a>, and a couple of things that might not be obvious on first reading.
<h3>Basic Usage</h3>
I didn't see on my first reading of the blog post that there are examples available at the github repository, such as the one for <a href="https://github.com/feilipu/Arduino_FreeRTOS_Library/blob/master/examples/Blink_AnalogRead/Blink_AnalogRead.ino">Blink_AnalogRead .</a> Going directly to those examples would probably have saved my a bit of confusion.
Compiling an 'Empty' sketch with just the import of

```c
#include <Arduino_FreeRTOS.h>
```

ran with no problems
As did defining parameters

```c
// define two tasks for Blink and AnalogRead
void TaskBlink( void *pvParameters );
void TaskAnalogRead( void *pvParameters );
```

From the code in the blog post itself, there seemed to be a couple of typos  - an extra <code>;</code> after "Blink" and "Analog Read" in the xTaskCreate function calls.
<h3>Updating the loop function</h3>
For the loop function with power saving code to work you need to also include

```c
#include <avr/sleep.h>
```

which is one of the <a href="https://www.arduino.cc/en/Reference/UsingAVR">AVR libraries</a>
Specific details on sleep are available <a href="https://www.nongnu.org/avr-libc/user-manual/group__avr__sleep.html">here</a>
<h2>Task Status Example</h2>
There is a <a href="https://github.com/feilipu/Arduino_FreeRTOS_Library/blob/master/examples/TaskStatus/TaskStatus.ino">nice example on the GitHub repository</a> which includes the blinking of an LED and the option to switch the blinking on or off via the sub connection.
One way to control that blinking is with <a href="https://pyserial.readthedocs.io/en/latest/shortintro.html">pyserial</a>
Here is a simply python control script. Note that you will need to change the serial port to the one your arduino is connected to. In Linux this will be something like '/dev/tttUSB0'.

```python
import serial
my_serial_port = 'COM5'
ser.write(b's')
```

To resume blinking use

```python
ser.write(b'r')
```

which will trigger the vTaskResume() function within the Arduino.
<h2>Taking things further</h2>
The <a href="https://github.com/feilipu/Arduino_FreeRTOS_Library/">Arduino FreeRTOS GitHub repository</a> has some <a href="https://github.com/feilipu/Arduino_FreeRTOS_Library/tree/master/examples">ready to go examples </a> which are made with Arduino in mind.
You can also work your way through the <a href="https://www.freertos.org/FreeRTOS-quick-start-guide.html">FreeRTOS quick start guide.</a>
Youtube has some channels with good videos covering FreeRTOS such as <a href="https://www.youtube.com/watch?v=F321087yYy4">Digi-key</a> and <a href="https://www.youtube.com/c/millsinghion/videos">C and Embedded</a>.

