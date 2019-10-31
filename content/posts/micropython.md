+++
title = "MicroPython"
date = "2019-10-26"
description = "There is still a place for innovation."
categories = ["conversation"]
tags = ["embedded", "iot", "python"]
+++

There is still a place for innovation.

Last month I had a conversation with my friends about how most of the
world has already been invented. And we aren't going to see a life
changing innovation in our lifetime.

Look at how

- Uber changed transportation
- GitHub changed collaboration
- Amazon changed shopping
- Tesla changed cars
- Google changed mobile phones
- Apple changed computers
- WhatsApp changed connectivity
- Tinder changed the lovesphere

In the past five years, things has been pretty constant. Any other
company is either trying to copy someone else, or just doing the bare
minimum to survive. Innovation has stagnated. It was a sad reality. My
friends agreed, but were more optimistic about the future than me.

Fast forward a week, I was watching a [video related to the Internet of
Things](https://www.youtube.com/watch?v=m1miwCJtxeM). The presenter
displayed an embedded device running Python. Suddenly, it hit me!

> ***My hypothesis was solely focused on the software world.***

Software ecosystem has saturated. There is a web service or an app for
everything. This is because tools to build software applications are
extremely accessible and convenient. You can learn to create a new
website in under a day.

However, the hardware market is still in its infancy. Let me explain.

### Flashback

When I was in college, I started learing embedded programming on an
ATmega8 microcontroller. To begin, you had to set up oscillators, fuse
bits, Serial Peripheral Interface using a USBasp programmer. Then you'd
set up your Operating System for the development environment. The whole
process was an extremely demanding task. By the time you were done, it
would be 11pm in the night and you had missed your lunch and dinner.
You'd then write a program in Embedded C to blink an LED, upload it, and
say your prayers. Happy tears would roll down your cheek when you saw
the red LED turning on and off every second. Those were some days!

Do you see it? You spent an entire day just to see an LED blink. The
entry barrier to hardware development was enormous.

### Arduino

Meet Arduino - a ready made development board created by some wonderful
people in Italy. It had a microcontroller, a USB, an LED and General
Purpose Input Output (GPIO) pins, all in one place. Just plug it into
your computer, open BlinkLED example and hit the Upload button. The LED
would be blinking as if you had put a gun to its head. All of this in
under 10 minutes.

> ***Arduino changed the hardware development game.***

Suddenly people from all over the world were creating wonderful projects
and sharing them on the internet.

However, you don't see as many hardware services as you'd see web
services. There is still a big gap between hardware and software
development. Why?

Because writing code in C, compiling it, waiting for it to upload and
verifying that everything works takes a lot of time. And god forbid, you
need to debug something. Hell is a modest word for that situation.

### MicroPython and pyboard

Enter pyboard. It's the new kid on the block. You can write code in
everybody's favourite language — Python (3, not 2). It allows you to get
up and running in just three simple steps:

- Write code in MicroPython
- Plug pyboard into your computer
- Upload your code

Features:

- Powerful - 168MHz CPU, 192k RAM, 1M flash Debuggable - REPL console
- Modular - run code from a microSD card Peripherals - SPI, I2C, Serial,
- RTC, 3 ADC, 2 DAC, 1 accelerometer, 24 GPIO, 4 LEDs

With features like this and an open source programming language
(MicroPython), hardware development has become accessible to everybody.

### Conclusion

It might seem like innovation around us has stalled. But it's not true.
Development of hardware devices is now as easy and convenient as is
developing a web service. I am hopeful that we will see a rapid growth
of new and exciting IOT devices in our lifetime.

One more thing. In light of new evidences like Rust and WebAssembly, I
now believe that the software world is also up for a fight to innovate.

### Sources

[Micro Python pyboard
overview](https://www.youtube.com/watch?v=5LbgyDmRu9s)
