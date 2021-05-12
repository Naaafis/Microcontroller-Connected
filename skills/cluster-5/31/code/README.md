# udp_client

Code focus on line 1023 - 1062
We used PWM for the LIDAR reading, which depends on a trigger pin to go low for activation. We set this pin low at every iteration of a while loop and then measure the rising and falling edge following that lowering. The duration of the next pulse is proportional to the distance to the nearest object detected by the LIDAR.
