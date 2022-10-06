# Anjay esp32 client experiment  #

In this tutorial we will setup and test a LWM2M anjay client on a ESP32 chip and communicate with the leshan server I setup earlier on a raspberry pi. 
- Reference from professor Paul Schragger  https://github.com/pschragger/IOT_Tutorials_for_VU/tree/main/RPI_BUILD_LWM2M_DEVICE
## Prerequistes #
### Information about my laptop
- My laptop is a MacBook air M1 2020 version.
- IDE:  The Arduino IDE version 2.0.0 MacOS version 10.14
- Adapter: Belkin USB C Hub, 5-in-1 MultiPort Adapter Dock.
- Microcontroller: ESP32-WROVER_DEV
- 2 Jumper Wires
- Breadboard from ESP32 kit
- 1 10k ohm resister
- 1 red LED



## To follow this tutorial you will need: 
A laptop with ssh installed, raspberry Pi dietPi accessible via ssh on wifi or ethernet, leshan server repository (https://www.eclipse.org/leshan/) at [ Leshan Github ]
## A list of tutorial you will need to complete before starting this experiment: 
- Setup Router Tutorial :
https://github.com/geliyangVU/VU_FALL22_IOT_CLASS/blob/main/Setup_Router_Tutorial/README.md
- Setup Raspberry Pi : 
https://github.com/geliyangVU/VU_FALL22_IOT_CLASS/blob/main/Setup_RaspberryPI/RPI_OS_Setup.md
- Setup Leshan LWM2M server: https://github.com/geliyangVU/VU_FALL22_IOT_CLASS/blob/main/Setup_LWM2M/LWM2M_leshanServer_Setup.md
- Setup Analog devices: https://github.com/geliyangVU/VU_FALL22_IOT_CLASS/blob/main/Analog_Device_Tutorials/Temperature_humidity_sensor_Tutorial.md

## Steps ##

## Install C compiler ##

1.  Test to see if the c compiler is already installed  using 

```
gcc -v
```
<img width="803" alt="1 Installgcc" src="https://user-images.githubusercontent.com/97559266/194380912-10c3ef84-5fda-43f9-b92d-6dbd2327c450.png">

2. If installed then go to the next step if not then use 

```
sudo dietpi-software`
```
<img width="815" alt="2 verifiedgccisinstalled_installpackagesusingcommand" src="https://user-images.githubusercontent.com/97559266/194380995-4182ff0e-bcf9-4a72-a79f-cfc48070ef9a.png">

## Install utils and libraries to build anjay ###

You can peform this install in any directory.  YOu are using the linux apt-get command a root using sudo.

``` 
sudo apt-get install git build-essential cmake libmbedtls-dev zlib1g-dev
```

## Build and install the avs_commons system ##


1. clone the avs_commons repo
```
cd ~/projects
git clone https://github.com/AVSystem/avs_commons
```
<img width="798" alt="3 cloneavs_commonsrepo" src="https://user-images.githubusercontent.com/97559266/194381186-76075b24-0760-4f8c-8048-0baaf6a3dde5.png">

2. Build and install the avs_commons library
```
cd ~/projects/avs_commons
cmake . && make && sudo make install
```

<img width="794" alt="4 buildavs_common" src="https://user-images.githubusercontent.com/97559266/194381234-d8db4ea1-d467-45c6-acfc-19386f1b7c10.png">

You have now built and installed the avs_commons library into share directories

## Build and install the ANJAY Library ##

1. retrieve the anjay code
```
cd ~/projects
git clone https://github.com/AVSystem/Anjay
```
<img width="596" alt="5 gitcloneanjay" src="https://user-images.githubusercontent.com/97559266/194381263-dc7b2257-41f3-4cce-8d23-40ddcc8ac7d0.png">


2. build the anjay code
```
cd ~/projects/Anjay
git submodule update --init
cmake . -DDTLS_BACKEND="mbedtls"
make -j
```
<img width="820" alt="6 buildanjaycode" src="https://user-images.githubusercontent.com/97559266/194381280-f7813f37-c03f-404c-9583-3b80745202f7.png">
<img width="879" alt="7 buildanjaycode" src="https://user-images.githubusercontent.com/97559266/194381343-9644409d-7520-495d-82ea-964bcc7c69f4.png">

3. try the anjay demo

-- view the leshan test server at https://leshan.eclipseprojects.io/#/clients
-- run the demo and see your machine listed in the leshsn server
```
./output/bin/demo --endpoint-name $(hostname) --server-uri coap://leshan.eclipseprojects.io:5683
```

<img width="663" alt="8 buildanjayclient" src="https://user-images.githubusercontent.com/97559266/194381390-cc51cee2-0e4c-45e3-a3bc-781cb8f79539.png">

### Installing Anjay library objects
https://avsystem.github.io/Anjay-doc/Compiling_client_applications.html
```
cd ~/projects/Anjay
cmake -DCMAKE_INSTALL_PREFIX=/home/dietpi/projects/Anjay-esp32-client . && make &&  make install
```

If the build does not work then delete the Anjay-esp32-client directory and clone a prebuilt version using:

```
cd projects
git clone --recurse-submodules --remote-submodules https://github.com/pschragger/Anjay-esp32-client
```

## Build the ANJAY client ##

1. move to the anjay-esp32-client directory that was clone earlier
```
cd ~/projects/Anjay-esp32-client
```

2. Setup the local enironment for using the esp tools
```
cd ~/projects/Anjay-esp32-client
. $HOME/esp/esp-idf/export.sh
idf.py set-target esp32 
```
3. setup the device requirements
     ```
     cd ~/projects/Anjay-esp32-client
     idf.py menuconfig
     ```
     - navigate to "Component->" and select config/anjay-esp32-client:
<img width="967" alt="10 configmenushown" src="https://user-images.githubusercontent.com/97559266/194381550-897d440f-f464-4409-828d-cdee825c3450.png">

     Setup your config to be:
     (anjay-esp32-client) Endpoint name
     (coap://{LESHAN_SERVER_IP}:5683) Server URI
     Choose socket (UDP)  --->
     Choose security mode (Non-secure connection)  --->


     - navigate to "Board - > "

     -  navigate to "Client options ->"
          - Change Server URI from coaps://try-anjay.avsystem.com:5684 to  coaps://YOUR_LESHAN_SERVER_IP_ADDR:5684
	    I used coaps://192.168.8.224:5684
	    Your IP my be different
	    <img width="676" alt="11 select anjay-esp32-client" src="https://user-images.githubusercontent.com/97559266/194381743-067bde26-2b4c-474d-96f7-afb8f7d211aa.png">

     -  navigate to "WiFi ->"
         To enter your IOT ROUTER WIFI SSID and key to allow the esp32 acccess to your router and PI.
	 <img width="681" alt="14 ChangeserverUritobeLeshanServerIpaddress" src="https://user-images.githubusercontent.com/97559266/194381795-e87d9260-16e8-4bc8-9de9-b8452411591a.png">
   <img width="682" alt="16 change wifi ssid" src="https://user-images.githubusercontent.com/97559266/194381883-466bd271-61c1-45dc-81f2-7acfce28e34d.png">
<img width="679" alt="17 change wifi password" src="https://user-images.githubusercontent.com/97559266/194381900-58de3046-2373-45be-9b47-01a106c7b83e.png">

## Configuration for light control 

- open the configuration menu

- go to component config

- select anjay-esp32—client

- make sure to select Unknown board (otherwise I was not able to see the light control option)

- Select light control enabled

- a new menu will pop up at the bottom of the page

- select enable red color and change the port by pressing the red color pin( New) shown on the second image
Here is an image showing my setup
<img width="795" alt="LightControlMenuTogonextSetting" src="https://user-images.githubusercontent.com/97559266/194382838-dd7e9ea6-2aee-458d-bd1f-2471a5a0a8d3.png">

<img width="793" alt="SetLightControlPin" src="https://user-images.githubusercontent.com/97559266/194383427-0ffc4fc5-d854-4cf7-beb0-d285cff11442.png">


4. Build the code for the device using
    
    ```
     cd ~/projects/Anjay-esp32-client
     idf.py build
     ```


5. find the port and flash the device

   - find port number by using
   ```
   ls -l /dev/ttyUSB*
   ```
   it returns something like
   crw-rw---- 1 root dialout 188, 0 Jul  8 06:17 /dev/ttyUSB0
   so the port number is 0

   - change the port number in this line to load the code
    idf.py -p  port_number flash
    with port nubmer = 0 I used:
     ```
     cd ~/projects/Anjay-esp32-client
     sudo chmod 666 /dev/ttyUSB0
     idf.py -p 0 flash
     ```
     You should see flashing
     <img width="686" alt="23 loadthecodeontoesp32" src="https://user-images.githubusercontent.com/97559266/194383814-64c91fb1-8761-48f9-a59b-35af9bf9767e.png">


6. Go to Leshan server in your browser.
   You should be able to see the client connected
   <img width="1440" alt="22 serverregistered" src="https://user-images.githubusercontent.com/97559266/194383787-134ec225-b3fb-4a60-95c4-cfdba943e475.png">
7. Go to light control home page
<img width="1436" alt="LightControlHome" src="https://user-images.githubusercontent.com/97559266/194383951-cf86d9b8-6dd1-4342-9f0e-9399de00fbfd.png">
 click on W inside On/Off tab
<img width="1440" alt="LightControlwindow" src="https://user-images.githubusercontent.com/97559266/194384150-06b27a2e-e6b7-425b-996b-fb7e3c13f466.png">
Toggle the value by entering true/false in the input test or by toggling the box near the input area.

Here is the circuit diagram showing 

![circuitforlight](https://user-images.githubusercontent.com/97559266/194389440-099bcb0a-efa4-4ce1-8acb-e4cb29f9f8b0.jpeg)


https://user-images.githubusercontent.com/97559266/194389402-6f466bee-f9cc-49e7-a1f0-410dea40c355.mp4



## Configuration for push button 
1.
- open the configuration menu

- go to component config

- select anjay-esp32—client

- make sure to select Unknown board

- Select push button

- a new menu will pop up at the bottom of the page

Here is an image showing my setup
<img width="800" alt="SetPushButtonPin" src="https://user-images.githubusercontent.com/97559266/194389775-bfc88005-5c95-40a8-a8b9-98d3c202c266.png">

2. Build the code for the device using
    
    ```
     cd ~/projects/Anjay-esp32-client
     idf.py build
     ```

3. find the port and flash the device

   - find port number by using
   ```
   ls -l /dev/ttyUSB*
   ```
   it returns something like
   crw-rw---- 1 root dialout 188, 0 Jul  8 06:17 /dev/ttyUSB0
   so the port number is 0

   - change the port number in this line to load the code
    idf.py -p  port_number flash
    with port nubmer = 0 I used:
     ```
     cd ~/projects/Anjay-esp32-client
     sudo chmod 666 /dev/ttyUSB0
     idf.py -p 0 flash
     ```
     You should see flashing
     <img width="686" alt="23 loadthecodeontoesp32" src="https://user-images.githubusercontent.com/97559266/194383814-64c91fb1-8761-48f9-a59b-35af9bf9767e.png">


4. Go to Leshan server in your browser.
   You should be able to see the client connected
   <img width="1440" alt="22 serverregistered" src="https://user-images.githubusercontent.com/97559266/194383787-134ec225-b3fb-4a60-95c4-cfdba943e475.png">
5. Go to push button home page
<img width="1436" alt="PushButtonHomeScreen" src="https://user-images.githubusercontent.com/97559266/194390136-5b042df7-4374-4f77-9739-cddce672e91d.png">

 click on R inside Digital Input Counter tab
 Expand the tabs
 <img width="1433" alt="PushButtonExpansion" src="https://user-images.githubusercontent.com/97559266/194390350-a0a4ef4b-4d4e-475b-8689-7d2972c29bca.png">
Pushed the button a few time and verified that counter was updated
<img width="1433" alt="PushButtonFinalIncrementation" src="https://user-images.githubusercontent.com/97559266/194390172-c082ad40-ed22-44ae-8fd8-b180ffe81aec.png">


Here is the circuit diagram

![circuitforpushbutton](https://user-images.githubusercontent.com/97559266/194390543-c809ee0c-691a-434e-90f4-7ccbaf54cfee.jpeg)









