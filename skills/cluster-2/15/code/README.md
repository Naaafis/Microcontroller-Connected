# adc1_example_main.c
Lots of borrowed code from last task
"
Combined i2c display code with adc example code from peripherals

lowered resolution of width from 12 bits to 11 bits
  - just experimenting to get voltage value to show up

increased ADC attenuation perimeter to 12 to include the range of millivolts that would fit our target

used old alphanumeric table from last quest to display the voltage in volts
"

Now the voltage reading is converted to inverse of distance in centimeters and then that inverse is taken and calculated into meters. A little bit of linear calculation had to be be done for the conversion to inverse of centimeters based on the given values of the data sheet of the SHARP IR sensor. This is all done inside a task as another task simultaneously runs a timer.

the task displays the distance every two seconds using timer interrupts to set a timer flag up to 1 every two seconds then it goes back to zero after setting the display values for the distance.
