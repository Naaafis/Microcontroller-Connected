# Code Readme

There are 3 main files to work with for this Quest: udp_client.c , node_server.js, and testing.html.
The udp_client.c file is in the 'code folder', however the other two files can be found in the 'exp' folder, also located inside of this 'code' folder.


##UDP_CLIENT.C:
The first 130 lines include all the initializations needed. Lines 133-180 include the timer_group0_isr() function that initializes the timer flags needed. There are around 200 lines of functions that both initialize things such as the I2C, as well as test the connection and such.

Lines 370-542 include code from the acceleration skill.

Lines 544-552 include the task to toggle the LED, which toggles the LED based on the value of on/off.

Lines 554 - 592 handle the battery level. It uses an adc reading to calculate the voltage level and prints this accordingly.

Lines 594-654 include code from the thermistor skill to read accurate temperature values.

Lines 670-768 handle the udp_client. This creates a socket, and sends all the relevant data across this socket to the server listening on the other end , as well as receives data from the server to handle the led toggle accordingly.

##node_server.js:
This file handles everything related to the server. PORT and HOST are initialized on lines 21/22, where the HOST is the ip address of the RPi. A socket is created on line 25, and furthermore we listen on this socket from lines 28-31.
On line 34, given a message, this message is converted to a string and then parsed appropriately to hold these respective values + their labels on lines 41-48. Lines 54-77 simply split this data up even more so that these 'arrs' hold the final value at that point in time.

Depending on whether the button is clicked or not, which is implemented in the next steps, lines 82-100  send data over the server so the .c file can register these button clicks, and furthermore toggle the LED. Finally, all the relevant data such as the button click + readings are sent to the html file and handled properly from lines 108-148 using post/get methods.

Finally we listen on internal port 8888, which is port-forwarded to port 4400, and using DDNS can be accessed on returnnosleep444.ddns.net:4400

##testing.html:
This file handles everything related to the html page.
Initializes for the html pages and variables to hold in these readings' values. When the window loads, there are 4 charts initialized from lines 43-206. This code was adapted from the last quest, and just needed to be slightly modified with the new dataPoints. There are $ajax requests on lines 231 - 258 which get the values that are sent from the server to these different pages. These values are stored, and furthermore on lines 261 - 288, these values are stored into the respective arrays for each reading, and these arrays hold the proper (x,y) point to be graphed.

Lines 291 - 299 handle the fixed portion of this strip-chart. by shifting the array of points to hold one less point after there are 10 points read in, we are able to keep a fixed graph with updated points, unlike the strip-chart which held every point from Quest 2.

The last main portion is the button handled on lines 336 - 340. Using the POST method, a button clicked is read and acknowledged, to actually toggle the LED by accessing this click and handling it, server side.



##Attributions
https://www.w3schools.com/tags/att_form_method.asp
