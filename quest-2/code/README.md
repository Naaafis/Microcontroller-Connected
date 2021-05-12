# Code Readme

There are several files incorporated in this Quest.
-HTML
-JS
-C : brought over from the ADC code example in the ESP examples.

The timer_isr handler sets a global timer_flag to 1 every 2 seconds, when the handler is called, and this sets the conditions to be met to average out all of the data points read in over the past 2 seconds, to then be sent to be plotted.

There are 3 separate tasks running, one for each sensor, and they each have their respective conversions to convert ADC values to either degrees celsius or meters.

The JS file reads in data from serialport (the ESP) as a string value. It properly parses through and splits this data up into the 3 respective values of Temperature, IR, and Ultrasonic. It then sends these values to the HTML file. The HTML files creates x,y data points based off of the arrays sent in. Then it generates 3 seperate charts to render to the screen.
