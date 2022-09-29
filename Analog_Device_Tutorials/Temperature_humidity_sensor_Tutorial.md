# Analog Device(DHT11) set up tutorial #

In this tutorial we will setup and test a temperature and humidity sensor on a ESP32. 
Reference from professor Paul Schragger to setup ESP32 Development Invironment  https://github.com/pschragger/IOT_Tutorials_for_VU/tree/main/RPI_ESP_IDF_tutorial

## Prerequistes/What is needed #
### Information about my tools
- My laptop is a MacBook air M1 2020 version.
- IDE:  The Arduino IDE version 2.0.0 MacOS version 10.14
- Adapter: Belkin USB C Hub, 5-in-1 MultiPort Adapter Dock.
- Microcontroller: ESP32-WROVER_DEV
- Temperature and humidity sensor: DHT11
- 4 Jumper Wires
- Breadboard from ESP32 kit
- 1 10k ohm resister



### Specs and operation of accessing data of the analog device
 Open Arduino IDE, got to File→Preferences and added this URL to additional board manager URLs: https://dl.espressif.com/dl/package_esp32_index.json
 Here is a screenshot:<img width="799" alt="showverboseoutputduringcompileandupload" src="https://user-images.githubusercontent.com/97559266/193134411-a1e95e67-1ba6-4f2d-8e52-38e52100ae53.png">
 Then I changed the baud rate to 115200. I also included DHTesp-master.zip library by clicking sketch->Include library->add .zip library-> choose the DHTesp-master.zip file.
I compiled the code and loaded it onto the esp32 microcontroller.

### Circuit Diagram of microcontroller to analog device
Here is the circuit diagram. Credit : ESP IDF C_TUTORIAL.pdf page 268
<img width="631" alt="Screen Shot 2022-09-29 at 4 30 05 PM" src="https://user-images.githubusercontent.com/97559266/193135714-51792ac6-f1f1-4f29-b525-367ce653209c.png">

![circuitdiagramtemperature](https://user-images.githubusercontent.com/97559266/193134903-9373bb8e-3ebc-4db5-8bb0-f10f56880ad3.png)

### Software snippet
I copied the following code snippet to IDE and compile it. I verified there was no error.
<img width="1006" alt="Screen Shot 2022-09-29 at 9 23 55 AM" src="https://user-images.githubusercontent.com/97559266/193134860-801ed4e8-4aee-4c97-afed-d9df980121f9.png">

### Resulting console
Here is a screenshot showing final result.
<img width="1395" alt="temperatureandhumiditysensorworking" src="https://user-images.githubusercontent.com/97559266/193135080-76292ce5-8b89-43d9-b47c-c3840a6a03f8.png">


## Additional tutorial files
https://github.com/geliyangVU/VU_FALL22_IOT_CLASS/blob/main/Analog_Device_Tutorials/Joy_Stick_Tutorial.md
