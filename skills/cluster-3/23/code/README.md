# i2c_accel.c

Took the given example code to communicate with the ADXL343 accelerometer (slave) through i2c in the ESP32 (master).

Wrote a function to write bytes to the slave address given a register. The steps were to analyze the waveform and matching the necessary code to write bytes. This involved a start command, writing slave address, waiting for an ack, writing register and acking, and finally writing the data itself and acking. All these commands are queued then pushed out at once at the end of the funciton.

The function for reading bytes is similar in the sense that we have to follow the waveform, but it required us to use the start command again after writing the register. We had to then write and ack check the read bit and use the read_byte function.

The function for reading two bytes just used the read_byte function twice and then shifted the MSBs over to the left before combining it with the LSBs.

The funciton for roll pitch and yaw does not include yaw because yaw and pitch can be viewed as the same. When you tilt on axes at an angle, another axes is inherently getting tilted at the same angle. The third axes provides the roll factor. 
