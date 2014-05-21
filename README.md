# ThingML to fully exploit your Arduino Yun!

This repository contains a set of ThingML libraries and examples to program applications using the Arduino Yun.

## Why the Arduino Yun?

The Arduino Yun is an interesting platform because it is open-source, inexpessive, widely available, contains 2 different processors and has good connectivity (Ethernet, Wifi). The two processors are:
* An 8 bit microcontroller ATmega32u4 (16MHz, 32k flash, 2.5k RAM, 1k EEPROM, Serial ports, USB)
* Atheros AR9331 SoC running embedded linux (MIPS 400MHz, 16M flash, 64M RAM, SD Card, serial port, ethernet, wifi, ...)

On the Arduino Yun board, the two processor are connected via:
* Serial Ports: 
* SPI: the SPI pins of the ATmega32u4 are connected to some AR9331 gpio pins and an SPI interface has been implemented on the AR9331. This is used by avrdude to upload code to the ATmega32u4 when using the "run-avrdude" script.
* Reset: The reset pin of the ATmega32u4 is connected to an AR9331 gpio pin. This allows resetting the microcontroller from the AR9331 using the "reset-mcu" command.

In terms of connectivity, the arduino Yun can be connected to via USB, ethernet and/or wifi. The USB connection goes to the ATmega32u4 serial port and the Ethernet and Wifi are through the AR9331 processor.

A typical applications based on the Arduino Yun involves  

When developing an application with the Arduino Yun it is possible to distribute the application logic between the 

![Typical application using an Arduino Yun][Fig-Yun-App]


[Fig-Yun-App]: https://raw.githubusercontent.com/SINTEF-9012/Yun-ThingML/master/doc/Fig-Yun-App.png?token=756491__eyJzY29wZSI6IlJhd0Jsb2I6U0lOVEVGLTkwMTIvWXVuLVRoaW5nTUwvbWFzdGVyL2RvYy9GaWctWXVuLUFwcC5wbmciLCJleHBpcmVzIjoxNDAxMjczMzA1fQ%3D%3D--26c5877d0dd773c9d58a40b68a7b0c6e801bfd50
