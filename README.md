<a name="mantis"></a>
# Mantis AR Glasses
Open source smart glasses

![alt text](https://i.imgur.com/jm8B8wC.png)

<a name="features"></a>
### Features


- Use a bluetooth multimeter and display the obtained data on the screen of the glasses.
- View the temperatures of electronic circuits with the MLX90640 thermal camera, displaying the video and the number data in the screen.

With these features, the Mantis AR Glasses wearer will be able to use the multimeter directly with the glasses and monitor circuit temperatures.

> ***This project has been realized by the students of the department of electronics of the institute CIFP Don Bosco LHII.***


- [ Mantis AR Glasses ](#mantis)
- [ Features ](#features)
- [ How did it start? ](#history)
	- [ Reverse engineering ](#reverse)
		- [ Vuzix Blade ](#vuzixblade)
		- [ Mantis Glasses ](#mantisglasses)
- [ What do we need? ](#whatweneed)
	- [ List of materials ](#listofmaterials)
	- [ Circuits and connections ](#circuits)
		- [ ST7735 Display ](#st7735)
		- [ MLX90640 ](#mlx90640)
		- [ Touch sensors ](#touchsensors)
		- [ Power management ](#power)
	- [ Software ](#software)
		- [ Install libraries ](#libraries)
		- [ Select the driver of our display ](#selectdriver)
- [ Bugs and error ](#bugserror)
- [ Thanks and references ](#thanks)
	- [ References ](#references)
- [ Disclaimer ](#disclaimer)


<a name="history"></a>
# How did it start?

We had the opportunity to test the Vuzix smart glasses and we thought it would be a good idea to do something similar but open source and cheaper.

One advantage of our glasses is that as they are open source, anyone with sufficient knowledge can improve them or adapt them to their needs.

<a name="reverse"></a>
## Reverse engineering
Before starting to design the parts, program or design the electronic circuits, we had to know how smart glasses were made on the inside, so we disassembled the Vuxiz Blade to have a clearer idea of how to realize our project.

<a name="vuzixblade"></a>
### Vuzix Blade
![alt text](https://i.imgur.com/sv9tv17.png)
We had a better understanding of the required hardware after disassembling the smart glasses.

<a name="mantisglasses"></a>
### Mantis Glasses
![alt text](https://i.imgur.com/GydCLwF.jpg)
In this photo, you can see the components we used for our glasses based on the Vuzix Blade.

<a name="whatweneed"></a>
# What do we need?
<a name="listofmaterials"></a>
## List of materials
Here is a detailed list of what we need to build our own smart glasses

- Microcontroller board (we reccomend and ESP32 or higher ram device)
- Display module (e.g. OLED or TFT)
- Micro-USB cable for programming and powering the board
- Lithium-ion battery or power bank
- 3D printer and filament to print the frame
- Light reflective material to display the screen (better if it's transparent)
- Power management circuit
- Wi-Fi or Bluetooth module (in case ypu are not using a board which already comes with it) 
- Sensors (e.g. accelerometer, gyroscope, proximity, we did not use them but might upload an upgrade with them)
- Buttons or touchpad for user input
- Wiring and cables to connect the components
- A software development kit and libraries to program the glasses.

In our case, we will use an ESP32 because it already has integrated WiFi and Bluetooth, and our sensor will be a thermal camera and a TFT RGB IPS screen because it offers higher resolution for using the thermal camera.

<a name="circuits"></a>
## Circuits and connections
<a name="st7735"></a>
### ST7735 Display
![alt text](https://i.imgur.com/MXfNOGr.png)

| ST7735 PIN      | ESP32 PIN |
| :--------- | :-----:|
| GND      | GND                    |
| VCC      | 3V3                       |   
| SCL | 15        |
| SDA      | 2        |   
| RES | 4        |
| DC      | 16        |   
| CS | 17        |
| BLK | No connected        |

<a name="mlx90640"></a>
### MLX90640
![alt text](https://i.imgur.com/uXUjABv.png)

| MLX90640 PIN      | ESP32 PIN |
| :--------- | :-----:|
| GND      | GND                    |
| VIN      | 3V3                       |   
| SCL | 22        |
| SDA      | 21        |   
| PS | GND        |

<a name="touchsensors"></a>
### Touch sensors
![alt text](https://i.imgur.com/2C5GvKA.png)

| TOUCH PIN      | ESP32 PIN |
| :--------- | :-----:|
| GND      | GND                    |
| VIN      | 3V3                       |   
| LEFT | 26        |
| GO BACK      | 14        |   
| SELECT | 27        |
| RIGHT | 25        |

<a name="power"></a>
### Power management
![alt text](https://i.imgur.com/TlzLC9l.png)

| BATTERY PIN      | ESP32 PIN |
| :--------- | :-----:|
| BATT-      | GND                    |
| BAT+      | 3V3                       |   
| VOLTAGE DIVIDER OUTPUT  | 34        |


<a name="software"></a>
## Software

<a name="libraries"></a>
### Install libraries
To install a library in arduino we have to go to :
- sketch->include library->manage libraries
![alt text](https://i.imgur.com/vbDBNBz.png)
And a window will open where we can look for the name of the library:
- TFT_eSPI
![alt text](https://i.imgur.com/Cnmn5hQ.png)

<a name="selectdriver"></a>
### Select the driver of our display
Once we have installed the TFT_eSPI library, we need to locate the library folder, which is located in the Arduino folder. In our case:
`C:\Users\Carlos\This PC\Documents\Arduino\libraries\TFT_eSPI`
Next, we need to edit the file named
`User_Setup_Select.h`
By default, it will contain the line
`#include <User_Setup.h>`
We need to comment out this line and locate the driver for our screen, in our case
`#include <User_Setups/Setup43_ST7735.h>`
and uncomment it.

It should look something like this:

```c++
...
//#include <User_Setup.h>           // Default setup is root library folder
...
#include <User_Setups/Setup43_ST7735.h>            // Setup file for ESP8266 & ESP32 configured for my ST7735S 80x160
...
```

<a name="bugserror"></a>
## Bugs and error

- When you are inside an option (multimeter, battery, info...), if you click left or right, you move through the menu without the need to click back.
- When you are in the thermal camera, if you click back, the program crashes and you need to reset the glasses.
- To connect the multimeter, the glasses must be switched off, first the multimeter is switched on and then the glasses, otherwise they do not connect.

<a name="thanks"></a>
## Thanks and refereces

Thanks to the electronics maintenance teachers for all the help offered during the project.

![alt text](https://i.imgur.com/BMM94Ca.jpg)

<a name="referenecs"></a>
### References

- 3D case:
	- https://www.youtube.com/watch?v=pdVS8--_uQQ
	
- How to install and use the TFT_eSPI library
	- https://www.youtube.com/watch?v=T2A4cEktt6Q

- Voltage divider design
	- [voltage divider](https://www.pangodream.es/esp32-getting-battery-charging-level) 	



<a name="disclaimer"></a>
## Disclaimer
![alt text](https://i.imgur.com/LufqfRG.png)

We are not responsible for any error, damage of the components or physical injury. Do this project under your own responsibility.




