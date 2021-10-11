# Schematic Design

- In this section we are going to look at how to start a design using a microcontroller
- Going to focus on what resources to refer for such a design


## Electronics knowledge requirement

- Need to be comfortable with basic Electronics components
    - Resistor
    - Capacitos
    - Inductor
    - Diode
    - Transistor
- No need to have advanced Electronics knowledge for most of the designs
- Power supply circuit is the most common analog heavy design
- Ability to understand datasheets is a must
- For more complex designs, it is vital to know advanced Electronics theories (Ex: High speed designs, impedance matching, etc.)


## Developing a Temperature Logger using STM microcontroller

Assume that following components are selected:

- Selected microcontroller: *STM32L053C8*
- Selected temperature sensor: *TMP112*
- Selected storage IC: *MX25V1635FM2I*
- Selected USB interface: *FT230XS-R*


## Microcontroller power and debug

- How to load the program?
- How to apply power to microcontroller?


## Connecting an LED

- Selecting a pin

## Connecting a push button

- Selecting a pin


## Connecting TMP112

- Using I2C communication
- Creating a part


## Connecting storage

- Using SPI communication


## Connecting USB interface

- Using UART communication


## Developing the PCB

- Converting the schematic into PCB
- Assigning footprints
- How to do the PCB design?


## Looking at reference designs

- A reference design is a gateway to any schematic design
- First focus on following three areas
    1. How to load the firmware?
    1. How to apply power?
    1. How to boot?

    - [STM32F407]()
    - [ATMega328P]()
    - [MSP430]()
    - [iMX8Q]()

- [Arduino schematic](https://www.arduino.cc/en/uploads/Main/Arduino_Uno_Rev3-schematic.pdf)


## Role of firmware in schematic design

- Interrupt pin selection
- Power down requirements
