# ir-car-beacon.c

Given the original code to change traffic light every 10 seconds and to always be sending and receiving data. Button interrupt functionality was unclear.

Modified code to not include timer as we set light states with button interrupts. The button handler function also sends out the current state of LED lights after setting the current state. This is how our button does two things at once

The receiving function remains the same and is always listening in a while loop. We set the states such that if the receiver sees a color in the data it receives, it sets its own color to that color. This allows us to demo transmission because we can show that the state of a FOB was changing without pressing its button.

Only two ways to change state: button press and IR reception
