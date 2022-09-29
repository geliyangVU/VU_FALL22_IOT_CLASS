# Analog Device(Joystick) set up tutorial #

In this tutorial we will setup and test a joystick sensor on a ESP32. 
Reference from professor Paul Schragger to setup ESP32 Development Invironment  https://github.com/pschragger/IOT_Tutorials_for_VU/tree/main/RPI_ESP_IDF_tutorial

## Prerequistes/What is needed #
### Information about my tools
- My laptop is a MacBook air M1 2020 version.
- IDE:  The Arduino IDE version 2.0.0 MacOS version 10.14
- Adapter: Belkin USB C Hub, 5-in-1 MultiPort Adapter Dock.
- Microcontroller: ESP32-WROVER_DEV
- Joystick
- 5 Jumper Wires
- 5 Jumper wire M/M
- Breadboard from ESP32 kit



### Circuit Diagram
Here is the circuit diagram. Credit : ESP IDF C_TUTORIAL.pdf page 155
<img width="428" alt="Screen Shot 2022-09-29 at 4 37 10 PM" src="https://user-images.githubusercontent.com/97559266/193137213-2ebddbe5-22d4-41eb-ba2a-3b6d14d642de.png">
![circuitdiagramjoystick](https://user-images.githubusercontent.com/97559266/193137314-507a4e13-7209-4f02-888f-d6273c6e3434.png)



### Software snippet
I copied the following code snippet to IDE and compile it. I verified there was no error.
<img width="696" alt="Screen Shot 2022-09-29 at 4 39 51 PM" src="https://user-images.githubusercontent.com/97559266/193137450-ea3c6a5b-0d7a-48ee-8713-a65f8f1d3912.png">

### Resulting console
Here is a screenshot showing final result.
<img width="1380" alt="joystickworking" src="https://user-images.githubusercontent.com/97559266/193137333-58ca867d-d3b4-451f-b853-de1cd3b5f809.png">
