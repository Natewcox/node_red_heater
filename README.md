# node_red_heater



# Project Goal

Using Node-Red to control a heater to connect to Apple Homekit

## Description

I use HomeKit for my home automations and I am wanted to share how I use Node-Red to add each element. This first repository is my main hub and my porch heater. Not every user has Apple devices so I use this Raspberry as a dashboard to control the heater and a button to tell my Garage Door Raspberry to open.

## Getting Started


![image](https://user-images.githubusercontent.com/97216517/148344058-215eebcf-89ab-4d1f-bc3b-b1bbfe6c1695.jpeg)


### Dependencies

Raspberry Pi
SD Card
DHT11 or 22 Temp and Humidity Sensor
5v 30a Relay
Wire

### Installing

* Flash the latest Raspberry Pi imiage to the SDCard
* Install the DHT sensor and relay.
* Add drawing
Turn on the Raspberry and perform the initial startup. Network is a must.
Install Node-Red per Nodered.org The recommended software has Node-Red but is missing a few parts. Use the full install to insure you have everything.
Fallow the instruction so Node-Red starts at boot.
If you plan to communicate between Pis, I recommend Mosquitto. https://mosquitto.org/blog/2013/01/mosquitto-debian-repository/
Once Node-red is running, access it through any web browser on the same wifi using -the.ip.add:1880
In the dropdown, Click Manage Pallets to add the node contrib-homekit-bridged or in terminal
npm install node-red-contrib-homekit-bridged
Also add contrib-dht-sensor
npm install node-red-contrib-dht-sensor
A library is required to control the DHT sensor found here. http://www.airspayce.com/mikem/bcm2835/
Reboot
Import the JSON code in the file Import.

### Executing program

* How to run the program
* Step-by-step bullets
```
code blocks for commands
```

## Help

Any advise for common problems or issues.
```
command to run if program contains helper info
```

## Authors

Contributors names and contact info


## Version History
