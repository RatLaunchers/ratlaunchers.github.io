---
layout: post
title:  Care for a Slice of Pi?
description: An update on our electronics and firmware progress
header: assets/images/gallery/2021-12-30/rasppi.png
---
With the competition well underway, let’s take another look at our electronics! They’re almost done - they just need to undergo testing, have their issues rectified, and then be mounted onto the satellite! 

## Raspberry Pi Zero 2 W
![icon](/assets/images/gallery/2021-12-30/rasppi.png)
The firmware on our Raspberry Pi Zero 2W was written in Python and runs on Raspberry Pi OS. It is programmed to log values from our GPS, compass, pressure, humidity, and temperature sensors as well as take pictures from our Pi camera module for our secondary mission. All of the data is logged to a CSV file for analysis post launch.

### Interfacing with Sensors

The BN-880 GPS receiver was pretty simple to set up with the sensor attached to our Raspberry Pi’s serial interface and controlled by the Linux GPSD service. Interacting with the GPSD daemon was done using the [gps3](https://pypi.org/project/gps3/) Python library which has a useful threaded data stream which makes grabbing our GPS data really easy. The HMC5883 compass found on the same module was controlled over our Raspberry Pi’s I2C pins and utilizing the [smbus2](https://pypi.org/project/smbus2/) library and some basic trigonometry allowed us to find our compass heading. Grabbing temperature and humidity values from our DHT11 was simplified with Adafruit’s [DHT library](https://pypi.org/project/Adafruit_Python_DHT/). The sensor that proved to be the most difficult to interface with was our Adafruit LPS25 pressure sensor module. With the Raspberry Pi’s main I2C pins being used for our compass sensor, we had to configure the Raspberry Pi so that we could use the EEPROM pins as a second pair of I2C pins. Our troubles with the LPS25 did not end there as there was a lack of libraries available for the sensor using regular Python so we had to consult the sensor’s datasheet and the CircuitPython LPS library to figure out how to interact with the sensor with smbus2.

### Raspberry Pi Camera

The Raspberry Pi camera module ran into some issues due to current issues in the Raspberry Pi Linux kernel and libcamera stack on the Raspberry Pi Zero 2W. To fix these issues we are using the legacy version of Raspberry Pi OS with its older camera stack. Our firmware is programmed to take a picture every 10 seconds for our secondary mission.

## Arduino Nano
![icon](/assets/images/gallery/2021-12-30/arduinonano.png)
We also have an Arduino Nano based backup system on our satellite to record key data even if the Raspberry Pi system fails. It is equipped with a DHT11 temperature and humidity sensor, a BMP280 pressure and temperature sensor, and an SD card breakout board. The DHT11 sensor simply connects to the Arduino via a single digital pin, while the BMP280 uses the I2C interface, on pins A4 and A5 of the Arduino. Since it was possible to leverage pre-existing libraries for reading both sensors and for writing to the SD card, writing the firmware was fairly straightforward. The Arduino is programmed to read data from both sensors every second, writing the data to the SD card for analysis post flight.
