+++
title = "Color organ"
date = "2029-12-14"
description = "Mixing colors and music is always fun"
+++

Mixing colors and music is always fun

The term color organ refers to a tradition of mechanical devices built to represent sound and accompany music in a visual medium. This is what I built for myself.

[Video]

### Theory

To convert music into visual effects, I sampled the recording every 100ms and ran it through a Fast Fourier Transform to get its frequency components. Then I convoluted this with 3 band pass filters designed to provide me the coefficients of bass, speech and treble. With these coefficients, I lit up the RGB leds using Pulse Width Modulation (PWM) to get the colors as shown above. The steps are simple. However, the real challenge was the implementation.


I found out that you should power the control and power circuits from the same supply. When the beat was too high, the whole thing lit up like christmas and took all the power to themselves. This caused a voltage drop in the control circuit, i.e. Arduino. So, it shut down. As a result the leds powered off causing the voltage to rise back up again and Arduino output voltages reached the threshold to drive the MOSFET circuit causing the leds to start dancing again. So, you would actually see flashes when you play a song with large beats.

