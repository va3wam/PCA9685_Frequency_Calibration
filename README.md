# Introduction
This code is used to calibrate the frequency of the PCA9685 I2C 16 channel servo driver using a 30 pin ESP32 DEVKIT V1 board. Note that the circuit used here does not allow for hooking up 5VDC power so you will not be able to drive an actual servo motor. This code and circuit is to demonstrate how the servo driver can be calibrated.

## Overview
In order to ensure that all Hexapod robots behave the same way we need to follow two seperate calibration procedures. The first calibration procedure sets the output frequency of the PCA9685 servo driver. The second procedure calibrates the mapping of angles with the movement range of each servo motor attached to the driver. 

## Procedure 1. Calibrating the PCA9685 output Frequency
Change the value of the argument passed to setPWMFreq(~50) until the output frequency is constantly hitting the target frequency. For example. If you are targeting 50Hz and you set the FREQUENCY variable to 50 and read the output to be. 51 to 52 Hz then you can reduce the FREQENCY variable until the output is constantly 50Hz. Example wiring instructions and code for all of this are provided below. 

The Adafruit library for controlling the PCA9685 module can. Be found [here](https://adafruit.github.io/Adafruit-PWM-Servo-Driver-Library/html/class_adafruit___p_w_m_servo_driver.html)

## Procedure 2. Calibrating the Servo Motor Angle
See [this repo](https://github.com/va3wam/calibrateServoMotor) for details and sample code for this procedure.

# Wiring without LLC
These instructions tell you how to wire up a circuit to measure the PWM output frequency of the PCA9685 without the use of a logic level converter. This circuit is only useful for  bench testing. To follow the instructions in this section it will help to use the following orientations of the boards involved. 
* Orient your ESP32 so that the USB port is facing down.
* Orient the PCA9685 so that the big capacitor and the two screw down power terminals  are to the right.

## The ESP32
On the ESP32 use the following [physical pins](https://www.electronicshub.org/esp32-pinout/):
* Pin 11 goes to bottom right pin of first cluster of PWM pins on the PCA9685.  
* Pin 29 goes t the SCL header pin on the PCA9685.
* Pin 26 goes to the SDA header pin on the PCA9685.

## The PCA9685
In addition to the connections outlined in the previous section make the following additional connections to the PCA9685 board

To the header:
* V+ on the header pin row goes to +3.3vdc
* VCC on the header pin row goes to +3.3vdc
* GND on the header pin row goes to a GND on the ESP32 board
* Also connect +3.3vdc to the + screw down power terminal

# Wiring with an LLC
These instructions tell you how to wire up a circuit to measure the PWM output frequency of the PCA9685 with the use of a logic level converter. This circuit can be used in a working circuit not just a bench testing situation like the method from the previous section. To follow the instructions in this section it will help to use the following orientations of the boards involved. 
* Orient your ESP32 so that the USB port is facing down.
* Orient the PCA9685 so that the big capacitor and the two screw down power terminals  are to the right.
* Orient the LLC with the low level pins on the left hand side of the board.

## The ESP32
On the ESP32 use the following [physical pins](https://www.electronicshub.org/esp32-pinout/):
* Pin 11 goes to top left pin of the LLC (L1). 
* A second wire goes from the top right pin of the LLC (H1) to the bottom right pin of the first cluster of PWM pins on the PCA9685.  
* Pin 29 goes t the SCL header pin on the PCA9685.
* Pin 26 goes to the SDA header pin on the PCA9685.

## The PCA9685
In addition to the connections outlined in the previous section make the following additional connections to the PCA9685 board

To the header:
* V+ on the header pin row goes to +5VDC
* VCC on the header pin row goes to +3.3VDC
* GND on the header pin row goes to a GND on the ESP32 board

To the screw down power terminal block:
* Connect +5VDC to the V+ post
* Connect ground to the GND post

## The LLC
We are using the [KeeYees 4 Channel I2C Logic Level Converter Bi-Directional Module 3.3V to 5V Shifter for Arduino](https://www.amazon.ca/gp/product/B07LG646VS/ref=ppx_yo_dt_b_asin_title_o06_s00?ie=UTF8&psc=1). This board shifts the 5VDC signal coming out of the PCA9685 servo driver to 3.3VDC for input into pin 11 on the ESP32 dev board. 

* Connect the LV pin to the 3.3VDC power.
* Connect the GND pin on the left side of the board to ground.
* Connect the HV pin to the 5VDC power.
* Connect the GND pin on the right side of the board to ground.
