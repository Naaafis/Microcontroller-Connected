# Uart_echo_example_main.c


The main window contains a while loop that is consistently awaiting input from user.

If the user enters "s" by itself, the loop would run the switch statement and select the next mode available.

The Three modes that users could interact with is:
- Hex conversion of user input from decimal
- Echoing back user input
- toggling an LED light based on input if user is inputting 't'

All three modes are coded inside each switch statement.
 - toggle mode just sets the gpio pin if t is pressed
 - echo mode adds inputed characters to a char array until enter is pressed and displays the contents of the array to console.
 - hex mod utilizes same array and converts chars to its integer equivilant in ascii and converts them to hex using %x

The name of the coding file contains information about which example was utilized for this task.
