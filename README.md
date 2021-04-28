# pca9685Demo
Demo of PCA9685 I2C 16 channel servo driver using a 30 pin ESP32 DEVKIT V1 board

## Wiring
To follow the instructions in this section it will help to use the following orientations of the boards involved. 
* Orient your ESP32 so that the USB port is facing down.
* Orient the PCA9685 so that the big capacitor and the two screw down power terminals  are to the right.

### The ESP32
On the ESP32 use the following [physical pins](https://www.electronicshub.org/esp32-pinout/):
* Pin 11 goes to bottom right pin of first cluster of PWM pins on the PCA9685.  
* Pin 29 goes t the SCL header pin on the PCA9685.
* Pin 26 goes to the SDA header pin on the PCA9685.

### The PCA9685
In addition to the connections outlined in the previous section make the following additional connections to the PCA9685 board

To the header:
* V+ on the header pin row goes to +3.3vdc
* VCC on the header pin row goes to +3.3vdc
* GND on the header pin row goes to a GND on the ESP32 board
* Also connect +3.3vdc to the + screw down power terminal