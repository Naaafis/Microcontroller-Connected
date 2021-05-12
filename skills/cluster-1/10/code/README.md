# uart_asynch_rxtxtasks_main.c

Brought over FreeRTOS example code

deleted uart components of example code because we do not need to utilize user input


Define which pins are used for LED and which one is used for interupt

init():
  - initialized LED pins to be output and interupt pin to be get_input
  - set interupt type to be handled on posedge of clock
  - brought over code to initialize i2c display

Brought over I2C functions from i2c example code


Interupt task:
  - consistently checks if button is pressed and runs handler function if it is.
  - Handler function toggles a flag variable

LED task:
  - different algorithm then LED counter because we had to account for the fact that we must count down/up from current number if button is pressed
  - algorithm now has a counter and utilizes modulus to set each pin individually based on which number is to be represented.
   - if flag is on counter is going up, and down otherwise

I2C task:
  - just hardcoded up or down into conditionals
  - displays up if flag is on and down otherwise

Each task runs simultaneously with delays at the end of each of its constituent while loops.
