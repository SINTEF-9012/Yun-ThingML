# Arduino Yun with ThingML

This repository contains a set of [ThingML][Link-ThingML] libraries and examples to program applications using the [Arduino Yun][Link-Yun].

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

The ATmega32u4 of the Arduino allows connecting a variety of sensors and actuators in order for the application to interract with the physical world. In that respect the Arduino Yun is similar to the "regular" Arduino borads like the Uno or Leonardo. The addition of the AR9331 processor makes it interesting when building applications which are "connected". The AR9331 acts as a gateway between the microcontroller and an IP network (Either using Ethernet or Wifi). The Bridge library on the Arduino Yun allows for communication between the two processors.

A shown on the figure, the strength of such a setup is that the code of the final application can be distributed to 4 different locations:
* The ATmega32u4 microcontoller

  The microcontroller is connected to all the sensors and actuators. It has limited processing ressources but can react in real-time to events from the sensors. It is typically the right place to deploy the real-time critical part of the application, some real-time control algorithms, etc... It is not well suited to store data, perform non-realtime data processing, format data, etc...

* The AR9331 Processor

  The AR9331 Processor is a gateway between the microcontroller and the external "Internet" part of the application. It has much more processing power than the microcontroller, some storage capabilities and connects to the Internet. The fact that it is on the same board is a great advantage because the application developper can assume a good reliability for the connection between the microcontroller and the AR9331 Processor. 

* Servers and databases
* The client




[Fig-Yun-App]: https://raw.githubusercontent.com/SINTEF-9012/Yun-ThingML/master/doc/Fig-Yun-App-600.png?token=756491__eyJzY29wZSI6IlJhd0Jsb2I6U0lOVEVGLTkwMTIvWXVuLVRoaW5nTUwvbWFzdGVyL2RvYy9GaWctWXVuLUFwcC02MDAucG5nIiwiZXhwaXJlcyI6MTQwMTI3Mzg2M30%3D--fcd1abca987eb52e17c15c80d097b48950a3b543

[Link-Yun]: http://arduino.cc/en/Main/ArduinoBoardYun?from=Main.ArduinoYUN

[Link-ThingML]: http://www.thingml.org 
