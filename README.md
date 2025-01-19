# Waste-Segregation-Robot-Using-Atmega2560

This project implements a waste segregation robot using the ATmega2560 microcontroller. The robot uses a color sensor to detect the color of the waste and segregate it accordingly.

## Project Structure

Waste-Segregation-Robot-Using-Atmega2560/
├── Debug/
│ ├── Color Sensor.d
│ ├── Color Sensor.eep
│ ├── Color Sensor.elf
│ ├── Color Sensor.lss
│ ├── Color Sensor.o
│ ├── Color Sensor.srec
│ ├── makedep.mk
│ └── Makefile  
 ├── Color Sensor.cpp
├── Color Sensor.cppproj
├── firebird_avr.h
├── lcd.h
├── LICENSE
└── README.md

## Dependencies

- AVR-GCC Toolchain
- AVRDUDE
- ATmega2560 Microcontroller
- Atmel Studio 6.1 or later

## Setup

1. Clone the repository.
2. Open the project in Atmel Studio 6.1 or later.
3. Ensure that the AVR-GCC toolchain is installed and configured in Atmel Studio.

## Building the Project

To build the project, follow these steps:

1. Open Atmel Studio.
2. Open the project by navigating to `File -> Open -> Project/Solution` and selecting `Color Sensor.cppproj`.
3. Build the project by navigating to `Build -> Build Solution` or pressing `F7`.

## Flashing the Microcontroller

To flash the compiled binary to the ATmega2560 microcontroller, use the following command:

```sh
avrdude -c <ATMEGA> -p m2560 -U flash:w:Debug/Color\ Sensor.hex
```

## Source Code Overview

# Color Sensor.cpp

- This file contains the main logic for the waste segregation robot. It includes the following key functions:

- lcd_port_config(): Configures the LCD port.
- color_sensor_pin_config(): Configures the color sensor pins.

## Excerpt from Color Sensor.cpp

#define F_CPU 14745600
#include <avr/io.h>
#include <avr/interrupt.h>
#include <util/delay.h>
#include <math.h> //included to support power function
#include "lcd.h"
#include "firebird_avr.h"

volatile unsigned long int pulse = 0; //to keep the track of the number of pulses generated by the color sensor
volatile unsigned long int red; // variable to store the pulse count when read_red function is called
volatile unsigned long int blue; // variable to store the pulse count when read_blue function is called
volatile unsigned long int green; // variable to store the pulse count when read_green function is called

void lcd_port_config (void)
{
DDRC = DDRC | 0xF7; //setting all the LCD pin's direction set as output
PORTC = PORTC & 0x80; //setting all the LCD pins are set to logic 0 except PORTC 7
}

void color_sensor_pin_config(void)
{
DDRD = DDRD | 0xFE; //set PD0 as input for color sensor output
PORTD = PORTD | 0x01; //Enable internal pull-up for PORTD 0 pin
}

## firebird_avr.h

- This header file contains definitions and macros specific to the Firebird V robot and the ATmega2560 microcontroller.

## lcd.h

- This header file contains functions for interfacing with the LCD.

## License

This project is licensed under the MIT License. See the LICENSE file for details.
