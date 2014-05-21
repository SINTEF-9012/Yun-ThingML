# Using ThingML on the Arduino Yun

This repository contains a set of ThingML libraries and examples to program applications using the Arduino Yun.

## The Arduino Yun

The Arduino Yun is an interesting platform because it is open-source, inexpessive, widely available, contains 2 different processors and has good connectivity (Ethernet, Wifi). The two processors are:
* An 8 bit microcontroller ATmega32u4 (16MHz, 32k flash, 2.5k RAM, 1k EEPROM, Serial ports, USB)
* Atheros AR9331 SoC running embedded linux (MIPS 400MHz, 16M flash, 64M RAM, SD Card, serial port, ethernet, wifi, ...)

On the Arduino Yun board, the two processor are connected via:
* Serial ports: One of the serial port of the ATmega32u4 is connected to a serial port of the AR9331. This allows for bi-directional communication between the two CPUs. By default this serial link is used by the Arduino Yun Bridge library but if the Bridge service is stopped, it is possible to use this serial link for any purpose. On the Arduino side the serila port is "Serial1" and on the linux side it is the device "/dev/ttyATH0".
* SPI: the SPI pins of the ATmega32u4 are connected to some AR9331 gpio pins and an SPI interface has been implemented on the AR9331. This is used by avrdude to upload code to the ATmega32u4 when using the "run-avrdude" script.
* Reset: The reset pin of the ATmega32u4 is connected to an AR9331 gpio pin. This allows resetting the microcontroller from the AR9331 using the "reset-mcu" command.

In terms of connectivity, the arduino Yun can be connected to via USB, ethernet and/or wifi. The USB connection goes to the ATmega32u4 serial port and the Ethernet and Wifi are through the AR9331 processor.

## Typical application

A typical applications based on the Arduino Yun involves some sort of sensors and actuators connected to the Arduino Yun ATmega32u4 processor and some communication with the AR9331 processor to connect the ATmega32u4 to a backend server or a client via the Wifi or Ethernet network.

The figure bellow presents a typical setup:
![Typical application using an Arduino Yun][Fig-Yun-App]

When developing an application with the Arduino Yun it is possible to distribute the application logic between the 

[Fig-Yun-App]: https://raw.githubusercontent.com/SINTEF-9012/Yun-ThingML/master/doc/Fig-Yun-App-600.png?token=756491__eyJzY29wZSI6IlJhd0Jsb2I6U0lOVEVGLTkwMTIvWXVuLVRoaW5nTUwvbWFzdGVyL2RvYy9GaWctWXVuLUFwcC02MDAucG5nIiwiZXhwaXJlcyI6MTQwMTI3Mzg2M30%3D--fcd1abca987eb52e17c15c80d097b48950a3b543
