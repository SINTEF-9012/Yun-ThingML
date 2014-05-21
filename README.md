Yun-ThingML: ThingML to fully exploit your Arduino Yun!
===========

This repository contains a set of ThingML libraries and examples to program applications using the Arduino Yun.

Why the Arduino Yun?
==

The Arduino Yun is an interesting platform because it is open-source, inexpessive, widely available, contains 2 different processors and has good connectivity (Ethernet, Wifi). The two processors are:
* An 8 bit microcontroller ATmega32u4 (16MHz, 32k flash, 2.5k RAM, 1k EEPROM, 2 serial ports)
* Atheros AR9331 SoC running embedded linux (MIPS 400MHz, 16M flash, 64M RAM, SD Card, serial port, ethernet, wifi, ...)

On the Arduino Yun board, the two processor are connected via:
* Serial Ports: 
* SPI: the SPI pins of the ATmega32u4 are connected to some AR9331 gpio pins and an SPI interface has been implemented on the AR9331. This is used by avrdude to upload code to the ATmega32u4 when using the "run-avrdude" script.
* Reset: The reset pin of the ATmega32u4 is connected to an AR9331 gpio pin. This allows resetting the microcontroller from the AR9331 using the "reset-mcu" command.

When developing an application with the Arduino Yun it is possible to have parts of the application runnning on the microcontroller
