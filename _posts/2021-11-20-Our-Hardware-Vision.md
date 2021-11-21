---
layout: post
title:  Our Hardware Vision
description: An in depth look at the hardware we'll be using this year
header: /assets/images/Our%20Hardware%20Vision%20-%2011_19_2021.png
---
![alt text](/assets/images/Our%20Hardware%20Vision%20-%2011_19_2021.png)
As part of the CanSat Design Challenge, our primary goals are to record air temperature and air pressure. As well, we have set a secondary mission for ourselves to record images and other data to assess wildfire risk based on variables such as plant colour, humidity, meteorological conditions, terrain, and more.

So what hardware are we going to use to achieve this mission? Let’s find out!

## Primary System:
![icon](https://s.cdnshm.com/catalog/ro/t/448291462/raspberry-pi-zero-2-w.jpg)
Our primary system is based on a Raspberry Pi Zero 2 W. We chose the Pi Zero form factor due to its compact nature, its low power draw, and support for the Raspberry Pi camera. The Zero 2 W was released in the middle of our hardware selection process and chose it over the original Zero and Zero W because of massively increased processing power and the small price increase over the previous generations. The Pi Zero will collect the data from the sensors and camera and store it onto a 32GB microSD card.

![icon](https://i.ebayimg.com/thumbs/images/g/HlgAAOSwIV5d-kFh/s-l96.jpg)
Because the primary mission is to collect the air temperature and pressure, we’ve used an Adafruit LPS25 Pressure Sensor and a DHT11 Temperature and Humidity Sensor. The LPS25 collects air pressure data and offers outstanding accuracy (±1 hPa) for a reasonable price. The DHT11s were graciously provided by our sponsor, the STEAM Project, and provides sufficiently accurate temperature data. In addition, the DHT11 provides the humidity data required in our secondary mission.

![icon](https://i.ebayimg.com/thumbs/images/g/vOsAAOSwBU9hHNi4/s-l96.jpg)
In order to gather the terrain data we need to achieve our secondary mission, we needed to determine the precise location of the launch site. As well, we need to orientate the pictures to apply wind direction in the simulation. Therefore, we decided to use a GPS and a compass module. We selected the Beitian BN-880 for availability, cost reasons, and for the fact that it integrates both a GPS and a compass into a singular, compact module.

Most importantly, our secondary mission necessitates the use of a camera. In order to be able to determine plant health and create the fire simulation model, a photo must be taken while the CanSat is in its descent phase. The camera we’ve chosen is the Raspberry Pi Camera Module 2 NoIR. Based on the Sony IMX219, it provides sufficiently detailed images at up to 3280 x 2464 resolution and we are able to utilise the absence of an IR filter to assess plant health. It conveniently interfaces with the Pi Zero via a ribbon cable plugged into its CSI-2 connector.

## Backup System:
![icon](https://arduino-tutorials.net/public/img/parts/arduino-nano-nl.jpg)
We decided to include a backup secondary system in order to provide redundancy in our CanSat. While not being able to capture all the data that the primary system can (such as taking photos) it’ll provide us with the enough data to fulfill the primary mission. This simplified system, in turn, requires little space, draws less power, and has less things to go wrong. This backup system will collect temperature, pressure, and humidity data and store it on an SD card.

![icon](https://i.ebayimg.com/thumbs/images/g/gpcAAOSwkSxbInM-/s-l96.jpg)
The data is collected by a pair of sensors: the BMP280 and another DHT11. The BMP280 will provide the pressure and temperature data. The Bosch-made BMP280 has incredible accuracy with a resolution of ±1 hPa and an ability to be used as an altimeter with ±1 meter accuracy. We chose to take the temperature data from the BMP280 (±1°C) because it is more accurate than the DHT11 (±2°C). The DHT11 will provide temperature data.

The secondary system utilises an Arduino Nano microcontroller (provided by the STEAM Project) in order to pull data from the sensors and store it on a microSD card. We didn’t need a more powerful, full-fledged computer and the Nano provides the ideal combination of size and IO. All this data will be stored on a 32GB microSD card via a microSD card breakout.

## Power:
Last, but most certainly not least, we have the power system. All of our sensors run off of 3.3V or 5V that will be supplied by their respective controllers. Both the Pi Zero and the Arduino Nano run off of 5V that will be supplied by an LM2596 buck converter. The buck converter will step the 9V supplied by the 9V battery down to 5V. 
