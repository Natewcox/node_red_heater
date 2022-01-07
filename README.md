# node_red_heater

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

### Wiring

![image](https://user-images.githubusercontent.com/97216517/148473859-1b3ecf92-2f21-41be-9374-aacceda0c65e.jpeg)

### Installing

* Flash the latest Raspberry Pi imiage to the SDCard
* Install the DHT sensor and relay.
* Add drawing
* Turn on the Raspberry and perform the initial startup. Network is a must.
* Install Node-Red per Nodered.org The recommended software has Node-Red but is missing a few parts. Use the full install to insure you have everything.
```
bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)
```
*Turn on Node-Red start at boot.
```
sudo systemctl enable nodered.service
```
* If you plan to communicate between Pis, I recommend Mosquitto.
* https://mosquitto.org/blog/2013/01/mosquitto-debian-repository/
* Locate your IP address.
```
hostname -I
```
### Node-Red
* Once Node-red is running, access it through any web browser on the same wifi using the.ip.add:1880
* In the dropdown, Click Manage Pallets to add the node contrib-homekit-bridged or in terminal
```
npm install node-red-contrib-homekit-bridged
```
* Also add contrib-dht-sensor
```
npm install node-red-contrib-dht-sensor
```
* A library is required to control the DHT sensor found here. http://www.airspayce.com/mikem/bcm2835/
* Reboot
```
sudo reboot
```
Access Node-Red again and select import and copy and past
```

```


## Help

This is best to be used as an example. I tried to use a mixture of change nodes and function nodes to provide different ways to change the msg.payload

## Authors

Preston - Testing


## Version History

0.1 - Ruff draft
