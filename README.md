# Introduction
This code is used to calibrate the frequency of the PCA9685 I2C 16 channel servo driver using a 30 pin ESP32 DEVKIT V1 board. Note that the circuit used here does not allow for hooking up 5VDC power so you will not be able to drive an actual servo motor. This code and circuit is to demonstrate how the servo driver can be calibrated.

## Overview
In order to ensure that all Hexapod robots behave the same way we need to follow two seperate calibration procedures. The first calibration procedure sets the output frequency of the PCA9685 servo driver. The second procedure calibrates the mapping of angles with the movement range of each servo motor attached to the driver. 

## Procedure 1. Calibrating the PCA9685 output Frequency
Change the value of the argument passed to setPWMFreq(~50) until the output frequency is constantly hitting the target frequency. For example. If you are targeting 50Hz and you set the FREQUENCY variable to 50 and read the output to be. 51 to 52 Hz then you can reduce the FREQENCY variable until the output is constantly 50Hz. Example wiring instructions and code for all of this are provided below. 

The Adafruit library for controlling the PCA9685 module can. Be found [here](https://adafruit.github.io/Adafruit-PWM-Servo-Driver-Library/html/class_adafruit___p_w_m_servo_driver.html)

## Procedure 2. Calibrating the Servo Motor Angle
See [this repo](https://github.com/va3wam/calibrateServoMotor) for details and sample code for this procedure.

# Wiring
To follow the instructions in this section it will help to use the following orientations of the boards involved. 
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
