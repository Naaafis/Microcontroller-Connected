# i2c_display.c

Borrowed code from i2c_display example

The code initializes i2c display functions

Brought over code from Adafruit website: array to hold binary representation of ASCII characters

get_input() function:
  - uses uart to acquire user Input
  - stores input into a char array and converts chars to its ascii equivilant number
  - indexes into array holding binary equivilant of characters to set the displaybuffer array which is used to display the chars in the i2c

test_alpha_display() function:
  Given in the example code, just displays the displaybuffer set in the get input function
