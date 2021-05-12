#  The Thermistor

Author: Nafis Abeer

Date: 2021-02-26
-----

## Summary
Measure temperature with sensor every two seconds. Display voltage being outputted to adc pin on i2c display. Used timer interrupts to delay the temperature readings on the console. Temperature is calculated by using the voltage at adc pin to calculate resistance of Thermistor and converting that value to degrees Celsius.

## Sketches and Photos
Room temperature:
![Image](./images/roomTemp.png)

In water:
![Image](./images/InWater.png)

## Modules, Tools, Source Used Including Attribution
ESP32
i2c Display
adc
resistors
temperature probe: XLX-1516

## Supporting Artifacts
none for this one

-----
