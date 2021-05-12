# mcpwm_servo_control_example.c

Code borrowed from MCPWM servo code example in peripherals

Duplicated pulse width for steering and updated max degree to 180 for steering

    pin 18 --> ESC GPIO pin
    pin 21 --> Steering servo GPIO pin

There is function to convert degrees to PWM units

Calibrate function delays at first to allow ESC to be turned on

The servo task calls the calibration function then proceeds to run operations for ESC as well as steering servo
