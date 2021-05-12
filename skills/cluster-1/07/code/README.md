# LED_counter.c

The GPIO pins that the LEDs are connected to, are defined at the beginning of code.

The directions of GPIO pins are set to be outputs after being reset.

The LEDs receive voltage in binary order inside a while loop. The algorithm runs four for loops, one inside another, and the inner for loops represent LED functionality for LSBs and outer for loops do the same for MSBs.
