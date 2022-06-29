# Stealthburner_Toolhead_PCB

# **THE PROJECT IS NOT FINISHED**

# [中文版本/Chinese Version](readme_cn.md)

## Overview
This project contains a 3Dprinter Toolhead PCB for VORON StealthBurner Toolhead

The board has

* RP2040 Microcontroller, connect to Raspberry PI with USB
* TMC2209 for extruder motor
* MAX31865 RTD-to-Digital Converter
* SHT20 humidity&temperature sensor
* ADXL345 accrometer
* Two 5pins fan connecter, fit with 2/3/4 wires, 12/24V fans
* A 3pins probe connecter
* A normal NTC Thermistor connector
* A 2pins X Endstop connector
* A 3pins 5V WS2812(Neopixel) LED connector
* A 24V heater connector

## [Config Referencce](klipper_config.conf)

## Details
### Microcontroller
You can easily buy a RP2040 chip by about 1USD, it's much cheaper than similar STM32 series MCU today

the RP2040 has some UART interfaces ans a USB port, the USB is used for this design

### MAX31865
the on-board MAX31865 chip supports 2/3/4 wires, PT100/PT1000 RTD. please notice that you should choose the reference resistor(430R/4.3K) and a capacitor(100nF/1uF) based on your RTD value. If you use an 3wire RTD, please connect the FORCE2 pin to PORCE+, otherwise connect it to GND. Please make sure that your wiring is correct. Check the [Datasheet](https://datasheets.maximintegrated.com/en/ds/MAX31865.pdf) and [Here](Document/max31865.md) for more information.

### SHT20
This sensor is used to monitor chamber temp.

Though SHT20 is an NRND product now, we have no choice because klipper frimware only support SHT20. DS18B20 sensors are only supported on the "host mcu". A NTC thermistor should work too, so if a RTD sensor is used to measure hotend temp, you can have a try.

### ADXL345
is for resonances measurement. Both ADXL343 and ADXL345 should work

### FAN Connecter
support 2wires, 3wires(with speed monitor pin), 4wires(with PWM input and speed monitor)

12V/24V voltage can be set by the jumper. Check [Here](Document/fan.md) for more information.

### Heater
be careful about selection on MOSFET, a N-Channel MOSFET with low RDSon at 4.5V

### DC-DC
many models can be used, as long as they have same pin out

| options |
| --- |
| BL9342(by Shanghai Belling) |
| LMR54410(by TI)(Not tested) |
| LMR14006(by TI)(Not tested) |

please check the schmatic for details