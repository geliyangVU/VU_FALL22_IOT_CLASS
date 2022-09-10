# Information about my laptop
My laptop is a MacBook air M1 2020 version.
The router I am using is a GL.iNet model: GL-MT300N-V2.
The Raspberry Pi I am using is 4 Model B 8gb.



# Setup RaspberryPI Tutorial
Reference: https://github.com/pschragger/IOT_Tutorials_for_VU/tree/main/RPI_BOOT_WIFI_tutorial


## Purpose
Install DietPi on a Raspberry PI via WIFI ready to install other software
Install a version of a Linux operating system on the PI


## Prerequisites

To accomplish finishing the setup you will need:

A laptop or desktop to act as your development platform
A Raspberry PI ( 3 B+ or 4 )
A Class 10 microSD 8gb or better with the maximum being a 32gb microsd card ( Check https://www.mymemory.co.uk/blog/the-best-memory-cards-for-raspberry-pi/ for the best cards to use with a PI )
WIFI ROUTER and configuration info. I am using a travel or IOT router to create a local portable network that I can reconfigure to work in various locations using hardwire ethernet or wifi repeater functions to provide wan internet access. You need your personal routers SSID and your WIFI key info to configure your pi for access. If you need help setting up your WIFI router then follow this tutorial.<a href="https://github.com/geliyangVU/VU_FALL22_IOT_CLASS/tree/main/Setup_Router_Tutorial" target="_blank">Wifi_setup_Link</a>


## Setup steps

### Setup your working environment on your laptop

Prepare your device to with an archiver extractor - on windows I used BreeZip http:www.breezip.com but others are available from https://www.7-zip.org . On MacOS V11 it extracted using tools already installed but an unarchiver is available at https://theunarchiver.com for your mac if extraction is not working.
Prepare you laptop with a sd card writer such as: balenaEtcher https://www.balena.io/etcher/

## Download and configure DietPi on your laptop
### Download DietPi image and unzip the folder
<img width="919" alt="Screen Shot 2022-09-10 at 2 30 18 PM" src="https://user-images.githubusercontent.com/97559266/189497383-52c160e5-ec04-4f4f-b871-16a1ffa8ccf3.png">

## Open BalenaEtcher software and select the DietPi image and SD card location.

<img width="793" alt="Screen Shot 2022-09-10 at 2 48 03 PM" src="https://user-images.githubusercontent.com/97559266/189497504-fa7c3e27-aabb-4855-a8a2-4b5f754501db.png">


## Start flashing.
<img width="801" alt="StartFlashing" src="https://user-images.githubusercontent.com/97559266/189497573-a6421ab8-2c7f-4e3e-863f-a9e633be27f6.png">



## Finish flashing.
<img width="801" alt="FinishFlashing" src="https://user-images.githubusercontent.com/97559266/189497585-35298909-b6ce-4386-9be9-fd00e5a6ef67.png">


#### Close the BalenaEtcher software and unplug your sd card and plug it back again to verify that DietPI images are actually loaded onto the sd card

## Make sure to move dietpi.txt and dietpi-wifi.txt files to a different directory before editing(Otherwise you may encounter issues with file permissions)
Here is what I did, I copied them into a separate folder and edited these two files and copied them back.
<img width="1295" alt="Move2txtfiletoadifferentlocation" src="https://user-images.githubusercontent.com/97559266/189497655-bf76edbf-2fb2-4767-9cdf-19cc42ab99bb.png">

## Make the following changes to these two files.

<img width="950" alt="Screen Shot 2022-09-10 at 2 56 30 PM" src="https://user-images.githubusercontent.com/97559266/189497798-ba015d21-563b-498d-ae8c-3aa490b07a71.png">
Credit:IoT inclass work document from professor Paul Schragger.

Below are two screenshots taken from my work.

<img width="1141" alt="COnfigfordietPi" src="https://user-images.githubusercontent.com/97559266/189497763-8a219e1d-9af2-4c4a-8840-2d3fcf0253d5.png">

<img width="975" alt="EditDietPiWifiCONFIG" src="https://user-images.githubusercontent.com/97559266/189497756-274f3d42-7f9d-45d6-99ad-5a956d00a9f4.png">

## Copy dietpi.txt and dietpi-wifi.txt back and make sure to replace them in your sd card folder.

Here is the screen shot I took:
<img width="1004" alt="makesuretoreplacethem" src="https://user-images.githubusercontent.com/97559266/189497932-f34cde3e-dcb6-4653-8b61-5c6f3f98533e.png">

<img width="1030" alt="doublecheckthatthosetwofilesareupdated" src="https://user-images.githubusercontent.com/97559266/189497940-6d037e62-72dc-4c7c-92a8-98b58422ca53.png">
Make sure that the edits were saved!

#### Insert the sd card to your raspberry Pi and power it. The red and green leds will turn on. You should wait until the green light has finished flashing and the whole process may take 10 minutes 


## Go to the admin page of router and look for the IP address for the raspberry pi
In my case, my dietPi has an ip address of 192.168.8.1 

<img width="1374" alt="VerifiedthatDietPiisupandRunning" src="https://user-images.githubusercontent.com/97559266/189498203-d745e7d6-103a-4ba1-93f8-1494bea8e136.png">
You can see from the above picture that my raspberry pi has an ip address of 192.168.8.150
In order to ssh to my Raspberry Pi, I opened my terminal, and typed the following command:ssh root0192.168.8.150
the password I used was dietpi

<img width="1082" alt="Screen Shot 2022-09-10 at 2 25 00 PM" src="https://user-images.githubusercontent.com/97559266/189498265-9e1e3a7d-a13f-4685-a422-5d03e37cb08b.png">
I was able to get to the following UI, the upper left corner said: RPi 4 Model B (aarch64) with IP : 192.168.8.150
<img width="1059" alt="Screen Shot 2022-09-10 at 2 19 03 PM" src="https://user-images.githubusercontent.com/97559266/189498289-050ed282-77aa-4fb7-a214-9f82e9ac9af6.png">
It took me a while to get used to this UI and I was able to find the DietPi-Config from the menu.

<img width="1054" alt="Screen Shot 2022-09-10 at 2 20 05 PM" src="https://user-images.githubusercontent.com/97559266/189498446-7d83ec32-5cab-4643-b44c-744bcf9f15ae.png">

## Go to the Security Options to change password and hostname

Then I changed the password under Security Options.

<img width="1052" alt="Screen Shot 2022-09-10 at 2 20 21 PM" src="https://user-images.githubusercontent.com/97559266/189498475-ffac06a1-320a-4441-b05c-c56bff73fdee.png">
Change password and Hostname.

<img width="1083" alt="Screen Shot 2022-09-10 at 2 23 06 PM" src="https://user-images.githubusercontent.com/97559266/189498514-988dde46-17b3-4713-b013-670f98af5887.png">

<img width="1084" alt="Screen Shot 2022-09-10 at 2 23 23 PM" src="https://user-images.githubusercontent.com/97559266/189498520-963faa1c-c4ff-4a0e-8a77-21cd7bfde526.png">

The last thing I did was to confirm the password changed.

<img width="1062" alt="Screen Shot 2022-09-10 at 2 20 57 PM" src="https://user-images.githubusercontent.com/97559266/189498541-b6e27b08-5c3c-42ef-8a30-6fc3e8c137ba.png">










