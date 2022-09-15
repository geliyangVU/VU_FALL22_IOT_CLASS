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

## Problem encountered
VUGUEST firewall blocks icmp message that ping uses.
I resolved this issue using my home wifi.
Reference from professor
https://www.speedguide.net/faq/how-to-become-pingable-behind-a-routerfirewall-376


<img width="806" alt="knownhosterror" src="https://user-images.githubusercontent.com/97559266/190444528-c45ebe1a-c1d9-443c-9335-ce005ea4e80a.png">

I encountered this error of knownhost. I solved it by editing the known_hosts file under ~/.ssh/known-hosts
Here are some  screenshot showing my editing process.

As you can see in the following image, there exists a host with IP address 192.168.8.150 which causes the error
<img width="1375" alt="changeknownhost" src="https://user-images.githubusercontent.com/97559266/190445178-a2c8d53a-e992-4708-ba09-36c99c349a2d.png">

I used nano to edit this file by deleting the last line containing the 192.168.8.150.

<img width="790" alt="changeKnownhostusingNano" src="https://user-images.githubusercontent.com/97559266/190445423-dc73a713-f7ff-4e28-85db-3f9655afec7c.png">
Verified that the last line is gone.
<img width="1375" alt="knownhostchanged" src="https://user-images.githubusercontent.com/97559266/190445902-d0f73389-d8a2-42d6-a27e-019f691763ac.png">

## Resolve the wifi issue using home wifi.
I saved the file and retry to connect this DietPi IP address and it worked.

I was able to successfully connect to my dietPi.
<img width="1424" alt="successfulconnect to pi" src="https://user-images.githubusercontent.com/97559266/190446059-3fe7bad3-fe45-4794-b089-a20afbd304bf.png">

I adjusted the dietpi and unix user password for my dietPi as I did earlier in this tutorial.
<img width="1279" alt="Screen Shot 2022-09-14 at 9 41 33 PM" src="https://user-images.githubusercontent.com/97559266/190446295-1cff8821-fa09-43f2-a156-2f9b0da9c910.png">

The last step for this was to select the Go>>Start installation for selected software. I built the minimum linux image and here were the screenshots.
<img width="1439" alt="gotoinstall" src="https://user-images.githubusercontent.com/97559266/190446615-c7cb68f9-c48a-412f-bbdf-74a90fded468.png">


I was able to see the linux terminal using my mac's terminal.
I will continue to do installation later this week
<img width="1440" alt="linux terminal shown" src="https://user-images.githubusercontent.com/97559266/190446627-caf83611-0f94-4278-97bc-00158d1b2cdf.png">

## scp linux command

I have established the scp communication between my mac and RaspberryPi.
Here are the steps I followed. 



<img width="682" alt="Screen Shot 2022-09-15 at 12 26 09 PM" src="https://user-images.githubusercontent.com/97559266/190460914-2083081f-1ce7-436a-a2b1-499f9a4c6b77.png">
<img width="749" alt="Screen Shot 2022-09-15 at 12 27 48 PM" src="https://user-images.githubusercontent.com/97559266/190460947-b048ce62-4a92-441e-af31-30a19c493742.png">

The first screenshot showed the terminal from my mac. The second screenshot showed the terminal from DietPi
It said that the scp command not found on dietPi so I went to search on StackOverFlow to resolve.
This is the command I found helpful.


If you work with Debian or Ubuntu and clones, install this package:

    apt-get install openssh-client


Reference: https://stackoverflow.com/questions/17131048/error-when-using-scp-command-bash-scp-command-not-found

After I installed the openssh-client on my DietPi. I was able to send file from my mac's terminal to dietPi.
The second screenshot showed the result.



