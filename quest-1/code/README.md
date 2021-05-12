//Quest1_Feed_Fish_main

Brough over code borrowed for timer initialization, i2c, button and Servo

move_Server()
- if server flag is triggered it rotates the servo 3 times

Lots of i2c initialization functions

GPIO_isr handler turns on a start flag to signal that button has been pressed

timer_isr handler sets a global timer_flag to 1 every second the handler is called

The button task just reinitializes the global counter that is being used to display to i2c and start servo

The timer event task also displays to i2c by using counter and mod operations to acquire time in hours, minutes and seconds
  - Global timer_flag is reset to 0 at then end of display and it only turns on at the next second mark, so for that second, the display shows the counter values set by the counter value in the previous second

I2C is initialized to display 'WAIT'

pressing the button resets counter which resets the display, but the timer is still running without being initialized
