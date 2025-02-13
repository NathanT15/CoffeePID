# CoffeePID

An ESP8266 / Arduino based "PID" controller for your coffee machine controlled via a web interface. 


## Overview

This project builds on the CoffeePID project by [1024kilobyte](https://1024kilobyte.com). It fully automates a traditaional heat exchanger espresso machine by 
- controlling the boiler via PID and a relay 
- measuring flowrate of coffee with a scale 
- controlling the group head solenoid valve via a relay

## Hardware

- an [ESP8266 microcontroller board](https://www.aliexpress.us/item/3256801450319446.html?spm=a2g0o.order_list.0.0.4cb41802ARtZmn&gatewayAdapt=glo2usa&_randl_shipto=US)
- 2 MAX31865 breakout boards
- 2 PT100 RTD elements
- a SSR-25DA relay
- a generic [relay module board](https://www.aliexpress.us/item/2251832463344334.html?spm=a2g0o.order_list.0.0.4cb41802ARtZmn&gatewayAdapt=glo2usa&_randl_shipto=US)
- an [0.91" OLED display](https://www.aliexpress.us/item/3256804189335493.html?spm=a2g0o.order_list.0.0.4cb41802ARtZmn&gatewayAdapt=glo2usa&_randl_shipto=US)
- a [1kg load cell with HX711 amp](https://www.aliexpress.us/item/2251832859722659.html?spm=a2g0o.order_list.0.0.4cb41802ARtZmn&gatewayAdapt=glo2usa&_randl_shipto=US)
- pressure transducers
- a power supply

The MAX31865 is connected via SPI to the ESP8266, the pinout is defined in the header of the arduino file. You can also set the relay pin there.

# Setup / Install

As the project is based on the Arduino environment, you need to install some prerequisites to use this project. Those are:

- Arduino IDE
- ESP8266-extension to the Arduino IDE
- LittleFS-extension to the Arduino IDE

You should then be able to checkout this project and open the "CoffeePID.ino"-file in your Arduino IDE. Then if a compatible ESP8266-board is connected, you should be able to transfer the data-folder to the LittleFS area (Tools-menu: ESP8266 LittleFS Data Upload). And finally you just have to transfer the sketch to the ESP via the upload button in the Arduino IDE. On first startup the CoffeePID is starting its own wifi called "CoffeePID", the password is "coffeepid", you may take a look at the serial monitor to check for any issues. After connecting to this network the ESP can be reached via the url [http://coffeepid.local](http://coffeepid.local). You can change the wifi settings in the settings tab of the website.

To simplify the usage I created two QR codes you can use to connect to the CoffeePID wifi and then visit its homepage. You can print them and place them somewhere close to your coffee machine for even quicker access to CoffeePID. If you change the accesspoint settings you obviously have to create your own QR code to connect.

## QR Code to connect to the Wifi

![WiFi Accespoint credentials](images/CoffeePID_wifi_ap_qr_code.png)

## QR Code to open the CoffeePID frontend

![http://coffeepid.local](images/CoffeePID_frontend_qr_code.png)

# Development

As the webserver is optimized to only deliver *.gz-compressed files you have to re-compress any file after you changed it. To make this more convenient I added a shell-script to the root of the project called "optimize.sh". It should work without any changes on Mac and Linux systems, as long as you have the used tools installed, like purgecss and uglifycss. Before executing the script you need to unpack the "app.html.gz" to "app.html" inside the "www"-folder.
