# Code Readme

## C code
This code files includes 145 lines of initializations and definitions. Some notable ones are the fact that in order to get multiple I2Cs working we had to define different channels for them to run on. They come from the same SDA/SCL pins which was nice, however it did take a long time to figure out that by using different channels we would be able to access both the accelerometer as well as the alphanumeric display. Lines 148 - 182 include the regular i2c_master_init() function used many times in the past. We then have the testConnection() function which is a utility function to test for I2C device addresses, as well as the i2c_scanner which then scans for these respective devices. Next come the alphanumeric functions. Lines 225 - 236 include the alpha_oscillator() which turns on this oscillator for the alphanumeric display. Lines 240-251 include the no_blink() function, and lines 255-267 include the code to set_brightness_max() for the alphanumeric display. Lines 271 - 402 include the alpha_numeric table with all possible values and their respective encoding. Lines 404 - 470 include the alphanumeric_test() which we used to ensure that we were capable of running 2 seperate I2C devices, which we seriously struggled with for some time. Next are the ADX343 Functions. These are just check_efuse(), print_char_val_type(), getDeviceID(), writeRegister(), readRegister(), read16(), setRange(), getRange(), and getDataRate() which ends on line 651. All of these functions have been used in the past, specifically when working with the accelerometer. These next functions deal with actualy reading the values for x,y,z, as well as roll and pitch, and then polling the accelerometer for these values. These functions include getAccel(), calcRP(), and test_adxl343(), and end on line 700.

Next are the timer functions. The timer_group0_isr() geos from lines 714 - 761 and includes several important timers that are used respectively such as timer_flag, timer_flag_IR, timer_flag_IR2, timer_flag_accel, timer_flag_udp.

Next is the IR_task(), which we have done before. This is from lines 792 - 856. We used the IR in the front of the buggy to detect for obstacles/objects in its direct path. The IR proved to be much, much more reliable than the ultrasonic sensor which is why we ended up pulling in this sensor and its code from the past skills/quests.

###buggySpeedDistCalc()

The buggySpeedDistCalc() function runs a while loop set for every 1 second. In each iteration, it takes the number of counts (pinwheel counts). From there, it calculates the distance traveled in that 1 second. This value is added onto the total distance as well as used for buggy speed.

###WHEELCHECK()

THe wheelCheck() function checks the change of voltages going through the encoder. Low voltage means the encoder sees the white pinwheel, while the black pinwheel shows higher voltages. This functions checks to see if the sensor goes from high to low voltage, or vice versa. This tally (count) is sent to buggySpeedDistCalc() for speed calculations.
//PPIDDDD 1084 - 1403

Next comes the UDP code. We have the udp_client_task() that starts on 1422 - 1526. After many initializations this code is very simiair to code from the past. It create the socket on line 1452, it sends the proper payload on line 1466. Then it receives from the socket (information one whether to start or stop the car) and stores the length of this payload in 'len'. If len > 0 then we can analyze the message and act accordingly by changing the on_off flag respectively.

Lines 1528 - 1692 include the main code, which is just to run the respective initializations and tasks.

### PID steering and forward/backward unit
We calibrate our forward/backward unit by setting our device to nutral and leaving it there after a certain amount of specified time.
We used PWM for the LIDAR reading, which depends on a trigger pin to go low for activation. We set this pin low at every iteration of a while loop and then measure the rising and falling edge following that lowering. The duration of the next pulse is proportional to the distance to the nearest object detected by the LIDAR.
Given the Lidar value, we calculate the error of the distance from the wall and based on the severity of the error, in line 1206 to 1260, we resteer the vehicle back to the center. We currently do not account for over steering, but the idea would be to turn the vehicles wheels slightly in the opposite direction of the original steer in order to straighten the car out.

We have a global variable keeping track of the IR distance reading, which is used to calculated the cruising speed. line 1290 - 1299 calculates the errors for the desired distance from the vehicle from the endpoint and 1304-1352 controls the speed of the engine accordingly.

### UDP
We send a payload to our node server in intervals determined by timer flags as well as payload forming flags. This ensures that the node server receives consistent data.
Upon reception of messages, we determine the kind of button was pressed and set flags to turn left or right or start or stop and go and so forth. This is done in lines 1519 - 1575.

## JS code
This code file, 'node_testing.js', is very similair to the code we have been using in the past couple quests. After all of the initializations through line 23, we create a socket on line 23. Then we create the server by turning it on and get its address on lines 26-29. Line 32 is the start of receiving the message from the socket, converting it itno a string, and furthermore splitting it up into its respective values so that we have the accelerometer speed, the encoder speed, and the total distance traveled, all readily available in arrays  to send to the HTML file. On line 69, we handle the button click to turn the car on/off. Based off of the variable 'button_clicked' which will be explained later, we send the respective message to the esp so we know whether to turn the car on/off. Lines 137-139 send the information to the html. Lines 145-154 received the button click using POST method and toggle it accordingly. Lines 178-188 send the appropriate data to the html file, which includes the accelerometer data, the encoder speed, and the total distance traveled.

## HTML code

The HTML code has two separate graphs. One graph compares the readings between the accelerometer speed and the encoder speed. The second graph shows the total distance read from the encoder. We also have buttons for the user to control the car.

Please describe what is in your code folder and subfolders. Make it
easy for us to navigate this space.

Also
- Please provide your name and date in any code submitted
- Indicate attributrion for any code you have adopted from elsewhere
