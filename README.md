# node_red_heater

Using Node-Red to control a heater to connect to Apple Homekit

## DESCRIPTION

I use HomeKit for my home automations and I am wanted to share how I use Node-Red to add each element. This first repository is my main hub and my porch heater. Not every user has Apple devices so I use this Raspberry as a dashboard to control the heater and a button to tell my Garage Door Raspberry to open.

## GETTING STARTED


![image](https://user-images.githubusercontent.com/97216517/148344058-215eebcf-89ab-4d1f-bc3b-b1bbfe6c1695.jpeg)


### MATERIALS

1. Raspberry Pi
2. SD Card
3. DHT11 or 22 Temp and Humidity Sensor
4. 5v 30a Relay
5. Wire

### WIRING

![image](https://user-images.githubusercontent.com/97216517/148473859-1b3ecf92-2f21-41be-9374-aacceda0c65e.jpeg)

### INSTALLS

* Fallow the directions at [RaspberryPi.org](https://www.raspberrypi.org) to:
  1. Flash the latest Raspberry Pi imiage to the SDCard
  2. Perform initial startup. Network and Update is a must.

* Install Node-Red. The recommended software for the Raspberry includes Node-Red but is missing a few parts. Use the full install to have all files and updates.

```
bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)
```

Enable Node-Red at boot.

```
sudo systemctl enable nodered.service
```
If you plan to communicate between Pis, I recommend Mosquitto.
  * https://mosquitto.org/blog/2013/01/mosquitto-debian-repository/

Locate your IP address.

```
hostname -I
```

### Node-Red

* Once Node-red is running, access it through any web browser on the same wifi using the.ip.add:1880
  - If you wish the dash board nodes to work correctly, that Pallet must be added. Details will be added soon.
  - 

In the dropdown, Click Manage Pallets to add the node contrib-homekit-bridged or in terminal

```
npm install node-red-contrib-homekit-bridged
```

Also add contrib-dht-sensor

```
npm install node-red-contrib-dht-sensor
```

A library is required to control the DHT sensor found here. http://www.airspayce.com/mikem/bcm2835/

```
sudo reboot
```

Access Node-Red again and select import. Paste the code below.

```
[
    {
        "id": "f5930c9938a6d843",
        "type": "tab",
        "label": "Flow 1",
        "disabled": false,
        "info": "",
        "env": []
    },
    {
        "id": "6a8d3ef1.88061",
        "type": "homekit-bridge",
        "bridgeName": "Heater",
        "pinCode": "571-61-681",
        "port": "",
        "allowInsecureRequest": false,
        "manufacturer": "N8s Controls",
        "model": "Pi Zero",
        "serialNo": "3",
        "firmwareRev": "",
        "hardwareRev": "",
        "softwareRev": "",
        "customMdnsConfig": false,
        "mdnsMulticast": true,
        "mdnsInterface": "",
        "mdnsPort": "",
        "mdnsIp": "",
        "mdnsTtl": "",
        "mdnsLoopback": true,
        "mdnsReuseAddr": true,
        "allowMessagePassthrough": true
    },
    {
        "id": "d02a9326a17fba35",
        "type": "ui_tab",
        "name": "Home",
        "icon": "dashboard",
        "disabled": false,
        "hidden": false
    },
    {
        "id": "0cb8bd93f080ed18",
        "type": "ui_base",
        "theme": {
            "name": "theme-dark",
            "lightTheme": {
                "default": "#0094CE",
                "baseColor": "#0094CE",
                "baseFont": "-apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen-Sans,Ubuntu,Cantarell,Helvetica Neue,sans-serif",
                "edited": true,
                "reset": false
            },
            "darkTheme": {
                "default": "#097479",
                "baseColor": "#ff3a2f",
                "baseFont": "-apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen-Sans,Ubuntu,Cantarell,Helvetica Neue,sans-serif",
                "edited": true,
                "reset": false
            },
            "customTheme": {
                "name": "Untitled Theme 1",
                "default": "#4B7930",
                "baseColor": "#4B7930",
                "baseFont": "-apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen-Sans,Ubuntu,Cantarell,Helvetica Neue,sans-serif"
            },
            "themeState": {
                "base-color": {
                    "default": "#097479",
                    "value": "#ff3a2f",
                    "edited": true
                },
                "page-titlebar-backgroundColor": {
                    "value": "#ff3a2f",
                    "edited": false
                },
                "page-backgroundColor": {
                    "value": "#111111",
                    "edited": false
                },
                "page-sidebar-backgroundColor": {
                    "value": "#ffffff",
                    "edited": false
                },
                "group-textColor": {
                    "value": "#ff827b",
                    "edited": false
                },
                "group-borderColor": {
                    "value": "#555555",
                    "edited": false
                },
                "group-backgroundColor": {
                    "value": "#333333",
                    "edited": false
                },
                "widget-textColor": {
                    "value": "#eeeeee",
                    "edited": false
                },
                "widget-backgroundColor": {
                    "value": "#ff3a2f",
                    "edited": false
                },
                "widget-borderColor": {
                    "value": "#333333",
                    "edited": false
                },
                "base-font": {
                    "value": "-apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen-Sans,Ubuntu,Cantarell,Helvetica Neue,sans-serif"
                }
            },
            "angularTheme": {
                "primary": "indigo",
                "accents": "blue",
                "warn": "red",
                "background": "grey",
                "palette": "light"
            }
        },
        "site": {
            "name": "Node-RED Dashboard",
            "hideToolbar": "false",
            "allowSwipe": "false",
            "lockMenu": "false",
            "allowTempTheme": "true",
            "dateFormat": "DD/MM/YYYY",
            "sizes": {
                "sx": 48,
                "sy": 48,
                "gx": 6,
                "gy": 6,
                "cx": 6,
                "cy": 6,
                "px": 0,
                "py": 0
            }
        }
    },
    {
        "id": "db2cc99cbb67813e",
        "type": "ui_group",
        "name": "Garage",
        "tab": "d02a9326a17fba35",
        "order": 1,
        "disp": true,
        "width": "6",
        "collapse": false,
        "className": ""
    },
    {
        "id": "25a18f27c6ee6709",
        "type": "ui_group",
        "name": "Heater",
        "tab": "d02a9326a17fba35",
        "order": 2,
        "disp": true,
        "width": "6",
        "collapse": false,
        "className": ""
    },
    {
        "id": "5398308def1dc2ad",
        "type": "mqtt-broker",
        "name": "Heat",
        "broker": "10.0.0.56",
        "port": "1883",
        "clientid": "",
        "autoConnect": true,
        "usetls": false,
        "protocolVersion": "4",
        "keepalive": "60",
        "cleansession": true,
        "birthTopic": "",
        "birthQos": "0",
        "birthRetain": "false",
        "birthPayload": "",
        "birthMsg": {},
        "closeTopic": "",
        "closeQos": "0",
        "closeRetain": "false",
        "closePayload": "",
        "closeMsg": {},
        "willTopic": "",
        "willQos": "0",
        "willRetain": "false",
        "willPayload": "",
        "willMsg": {},
        "sessionExpiry": ""
    },
    {
        "id": "a99fd29a.401ce8",
        "type": "homekit-service",
        "z": "f5930c9938a6d843",
        "isParent": true,
        "hostType": "0",
        "bridge": "6a8d3ef1.88061",
        "accessoryId": "",
        "parentService": "",
        "name": "Porch Heater",
        "serviceName": "Thermostat",
        "topic": "",
        "filter": false,
        "manufacturer": "N8s Controls",
        "model": "Default Model",
        "serialNo": "Default Serial Number",
        "firmwareRev": "",
        "hardwareRev": "",
        "softwareRev": "",
        "cameraConfigVideoProcessor": "",
        "cameraConfigSource": "",
        "cameraConfigStillImageSource": "",
        "cameraConfigMaxStreams": "",
        "cameraConfigMaxWidth": "",
        "cameraConfigMaxHeight": "",
        "cameraConfigMaxFPS": "",
        "cameraConfigMaxBitrate": "",
        "cameraConfigVideoCodec": "",
        "cameraConfigAudioCodec": "",
        "cameraConfigAudio": false,
        "cameraConfigPacketSize": "",
        "cameraConfigVerticalFlip": false,
        "cameraConfigHorizontalFlip": false,
        "cameraConfigMapVideo": "",
        "cameraConfigMapAudio": "",
        "cameraConfigVideoFilter": "",
        "cameraConfigAdditionalCommandLine": "",
        "cameraConfigDebug": false,
        "cameraConfigSnapshotOutput": "disabled",
        "cameraConfigInterfaceName": "",
        "characteristicProperties": "{\"TargetHeatingCoolingState\":{\"validValues\":[0,1]},\"CurrentHeatingCoolingState\":{\"validValues\":[0,1]}}",
        "waitForSetupMsg": false,
        "outputs": 2,
        "x": 650,
        "y": 200,
        "wires": [
            [
                "1a8059d6b8099fc7"
            ],
            []
        ]
    },
    {
        "id": "475c6486a8f64adb",
        "type": "rpi-dht22",
        "z": "f5930c9938a6d843",
        "name": "",
        "topic": "rpi-dht22",
        "dht": "11",
        "pintype": "0",
        "pin": "17",
        "x": 360,
        "y": 160,
        "wires": [
            [
                "86131b4730f3ab4d",
                "8a69deb8e0dd5ede"
            ]
        ]
    },
    {
        "id": "86131b4730f3ab4d",
        "type": "function",
        "z": "f5930c9938a6d843",
        "name": "",
        "func": "var output = {\n    \"payload\": {\n    \"CurrentTemperature\": msg.payload,\n    \"CurrentRelativeHumidity\": msg.humidity,\n    \"TargetTemperature\" : 70\n}\n}\n\nreturn output;\n",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 460,
        "y": 200,
        "wires": [
            [
                "a99fd29a.401ce8"
            ]
        ]
    },
    {
        "id": "8a69deb8e0dd5ede",
        "type": "function",
        "z": "f5930c9938a6d843",
        "name": "",
        "func": "msg.payload = msg.payload * 1.8 + 32;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 460,
        "y": 120,
        "wires": [
            [
                "2e3642e73b65ebda",
                "c8b19c47bb940a86"
            ]
        ]
    },
    {
        "id": "c8b19c47bb940a86",
        "type": "ui_text",
        "z": "f5930c9938a6d843",
        "group": "25a18f27c6ee6709",
        "order": 2,
        "width": "3",
        "height": "1",
        "name": "",
        "label": "Humidity",
        "format": "{{msg.humidity}}%",
        "layout": "row-spread",
        "className": "",
        "x": 640,
        "y": 140,
        "wires": []
    },
    {
        "id": "18dfa3422482643e",
        "type": "inject",
        "z": "f5930c9938a6d843",
        "name": "",
        "props": [
            {
                "p": "payload"
            },
            {
                "p": "topic",
                "vt": "str"
            }
        ],
        "repeat": "60",
        "crontab": "",
        "once": true,
        "onceDelay": 0.1,
        "topic": "",
        "payloadType": "date",
        "x": 210,
        "y": 160,
        "wires": [
            [
                "475c6486a8f64adb"
            ]
        ]
    },
    {
        "id": "7be10ae5c03d8229",
        "type": "trigger",
        "z": "f5930c9938a6d843",
        "name": "",
        "op1": "1",
        "op2": "0",
        "op1type": "str",
        "op2type": "str",
        "duration": "1",
        "extend": false,
        "overrideDelay": false,
        "units": "hr",
        "reset": "",
        "bytopic": "all",
        "topic": "topic",
        "outputs": 1,
        "x": 990,
        "y": 220,
        "wires": [
            [
                "c0e0fcb3dd5f9896",
                "ceb47ba8a1853a64",
                "fd888b851c31cf14"
            ]
        ]
    },
    {
        "id": "c0e0fcb3dd5f9896",
        "type": "rpi-gpio out",
        "z": "f5930c9938a6d843",
        "name": "",
        "pin": "6",
        "set": "",
        "level": "0",
        "freq": "",
        "out": "out",
        "bcm": true,
        "x": 1220,
        "y": 200,
        "wires": []
    },
    {
        "id": "b9d041cdb37b3bd4",
        "type": "ui_button",
        "z": "f5930c9938a6d843",
        "name": "",
        "group": "25a18f27c6ee6709",
        "order": 3,
        "width": 0,
        "height": 0,
        "passthru": false,
        "label": "Start Heat",
        "tooltip": "",
        "color": "White",
        "bgcolor": "",
        "className": "",
        "icon": "",
        "payload": "{\"On\":true}",
        "payloadType": "json",
        "topic": "topic",
        "topicType": "msg",
        "x": 810,
        "y": 240,
        "wires": [
            [
                "7be10ae5c03d8229"
            ]
        ]
    },
    {
        "id": "2c3227ab276d7f3b",
        "type": "ui_led",
        "z": "f5930c9938a6d843",
        "order": 4,
        "group": "25a18f27c6ee6709",
        "width": 0,
        "height": 0,
        "label": "Heater Timer",
        "labelPlacement": "left",
        "labelAlignment": "left",
        "colorForValue": [
            {
                "color": "#ff0000",
                "value": "false",
                "valueType": "bool"
            },
            {
                "color": "#008000",
                "value": "true",
                "valueType": "bool"
            }
        ],
        "allowColorForValueInMessage": false,
        "shape": "circle",
        "showGlow": true,
        "name": "",
        "x": 1610,
        "y": 300,
        "wires": []
    },
    {
        "id": "2e3642e73b65ebda",
        "type": "ui_digital_display",
        "z": "f5930c9938a6d843",
        "name": "",
        "group": "25a18f27c6ee6709",
        "order": 5,
        "width": 0,
        "height": 0,
        "digits": "3",
        "decimals": 1,
        "x": 660,
        "y": 100,
        "wires": []
    },
    {
        "id": "ceb47ba8a1853a64",
        "type": "change",
        "z": "f5930c9938a6d843",
        "name": "",
        "rules": [
            {
                "t": "change",
                "p": "payload",
                "pt": "msg",
                "from": "1",
                "fromt": "num",
                "to": "true",
                "tot": "bool"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 1260,
        "y": 260,
        "wires": [
            [
                "2c3227ab276d7f3b"
            ]
        ]
    },
    {
        "id": "fd888b851c31cf14",
        "type": "change",
        "z": "f5930c9938a6d843",
        "name": "",
        "rules": [
            {
                "t": "change",
                "p": "payload",
                "pt": "msg",
                "from": "0",
                "fromt": "num",
                "to": "false",
                "tot": "bool"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 1260,
        "y": 320,
        "wires": [
            [
                "2c3227ab276d7f3b",
                "ebaa1b27e93660d1"
            ]
        ]
    },
    {
        "id": "44d66b47142aefed",
        "type": "mqtt out",
        "z": "f5930c9938a6d843",
        "name": "Heat",
        "topic": "heat",
        "qos": "",
        "retain": "",
        "respTopic": "",
        "contentType": "",
        "userProps": "",
        "correl": "",
        "expiry": "",
        "broker": "5398308def1dc2ad",
        "x": 810,
        "y": 640,
        "wires": []
    },
    {
        "id": "1ed2ce12a8264d36",
        "type": "ui_button",
        "z": "f5930c9938a6d843",
        "name": "",
        "group": "db2cc99cbb67813e",
        "order": 0,
        "width": 0,
        "height": 0,
        "passthru": false,
        "label": "Garage Door",
        "tooltip": "",
        "color": "",
        "bgcolor": "",
        "className": "",
        "icon": "",
        "payload": "true",
        "payloadType": "bool",
        "topic": "topic",
        "topicType": "msg",
        "x": 630,
        "y": 640,
        "wires": [
            [
                "44d66b47142aefed"
            ]
        ]
    },
    {
        "id": "1a8059d6b8099fc7",
        "type": "function",
        "z": "f5930c9938a6d843",
        "name": "",
        "func": "if (msg.hap.allChars[\"Target Heating Cooling State\"] == 1)\nreturn msg;\nelse\nreturn null",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 820,
        "y": 200,
        "wires": [
            [
                "7be10ae5c03d8229"
            ]
        ]
    },
    {
        "id": "ebaa1b27e93660d1",
        "type": "change",
        "z": "f5930c9938a6d843",
        "name": "",
        "rules": [
            {
                "t": "set",
                "p": "TargetHeatingCoolingState",
                "pt": "msg",
                "to": "0",
                "tot": "num"
            },
            {
                "t": "set",
                "p": "CurrentHeatingCoolingState",
                "pt": "msg",
                "to": "0",
                "tot": "num"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 660,
        "y": 440,
        "wires": [
            [
                "a99fd29a.401ce8"
            ]
        ]
    },
    {
        "id": "eaf3fb20b9c0dbed",
        "type": "comment",
        "z": "f5930c9938a6d843",
        "name": "dht11 & 22 temp humidity sensor",
        "info": "dht11 & 22 temp humidity sensor",
        "x": 210,
        "y": 240,
        "wires": []
    },
    {
        "id": "e5e6d3f5a746242b",
        "type": "comment",
        "z": "f5930c9938a6d843",
        "name": "Dashboard Elements",
        "info": "",
        "x": 650,
        "y": 60,
        "wires": []
    },
    {
        "id": "0efb9c7ceab786b5",
        "type": "comment",
        "z": "f5930c9938a6d843",
        "name": "Trigger output. Off after Trigger Timer",
        "info": "",
        "x": 1110,
        "y": 140,
        "wires": []
    },
    {
        "id": "55206107133afd88",
        "type": "comment",
        "z": "f5930c9938a6d843",
        "name": "Change Homekit Output to LED dashboard values",
        "info": "",
        "x": 1390,
        "y": 400,
        "wires": []
    },
    {
        "id": "a0f08bde23b48bb8",
        "type": "comment",
        "z": "f5930c9938a6d843",
        "name": "Trigger timed out, change to Homekit Values to signal it to show off",
        "info": "",
        "x": 700,
        "y": 520,
        "wires": []
    },
    {
        "id": "bc8ddc17a5464a43",
        "type": "comment",
        "z": "f5930c9938a6d843",
        "name": "To garage door pi to have this dashboard open Garage Door",
        "info": "",
        "x": 720,
        "y": 720,
        "wires": []
    }
]
```


## Help

This is best to be used as an example. I tried to use a mixture of change nodes and function nodes to provide different ways to change the msg.payload

## Authors

Preston - Testing


## Version History

0.1 - Ruff draft
