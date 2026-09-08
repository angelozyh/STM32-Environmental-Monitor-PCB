# STM32 Environmental Monitor PCB

A custom 2-layer PCB designed in KiCad for an STM32-based environmental monitoring system. The board integrates an STM32 NUCLEO-F303K8, BME280 environmental sensor, dual 74HC595 shift registers, a 4-digit 7-segment display, transistor-based digit drivers, and a pushbutton interface.

This PCB is the hardware implementation of my previously breadboarded STM32 environmental monitoring system. The goal of this project was to move from a working prototype to a custom PCB while gaining experience with schematic capture, footprint selection, PCB layout, routing, design-rule verification, and manufacturing preparation.

## Features

- STM32 NUCLEO-F303K8 development board
- BME280 temperature, humidity, and pressure sensor
- I2C communication between the STM32 and BME280
- 4-digit common-cathode 7-segment display
- Two SN74HC595 shift registers for display control
- Four NPN transistor low-side digit drivers
- Pushbutton user input
- Timer-interrupt-based display multiplexing
- UART interface for monitoring and debugging
- Socketed Nucleo, BME280, shift registers, and display for easy replacement
- M3 mounting holes for mechanical support

## System Overview

The STM32 reads environmental data from the BME280 over I2C and displays the selected measurement on a multiplexed 4-digit 7-segment display.

Two 74HC595 shift registers expand the available GPIO and provide the signals required to control the display. Four NPN transistors provide low-side switching for digit selection.

A pushbutton allows the displayed measurement to be changed between:

- Temperature
- Humidity
- Pressure

UART is also available for debugging and monitoring system operation.

## Hardware

| Component | Purpose |
| --- | --- |
| STM32 NUCLEO-F303K8 | Main microcontroller |
| BME280 | Temperature, humidity, and pressure sensing |
| 2x SN74HC595N | Serial-to-parallel output expansion |
| CC56-12SURKWA | 4-digit common-cathode 7-segment display |
| 4x NPN Transistors | Low-side digit switching |
| Pushbutton | User input |
| Resistors | LED current limiting and transistor biasing |
| 100 nF Capacitors | Local decoupling |

## PCB Design

The PCB was designed in **KiCad 10** as a 2-layer carrier board for the existing STM32 environmental monitoring system.

### Board Specifications

- 2-layer FR-4 PCB
- 1.6 mm board thickness
- 1 oz outer copper
- Lead-free HASL surface finish
- Front and back ground pours
- Plated through-holes and vias
- 0.8 mm / 0.3 mm drill vias
- Four 3.2 mm NPTH mounting holes for M3 hardware
- Copper keepout regions around metal mounting hardware

The board primarily uses through-hole components to make hand assembly, modification, and component replacement easier.

## PCB Design Process

The PCB development process included:

1. Converting the breadboard implementation into a complete KiCad schematic
2. Selecting and verifying component footprints using manufacturer datasheets
3. Creating custom footprints for board-specific components
4. Positioning components based on signal flow and mechanical requirements
5. Routing signals across the front and back copper layers
6. Adding ground planes
7. Adding mounting holes and mechanical copper keepouts
8. Configuring manufacturing constraints
9. Running KiCad Design Rule Checks (DRC)
10. Generating Gerber and Excellon drill files
11. Inspecting the manufacturing files in KiCad Gerber Viewer
12. Verifying the final board using the manufacturer's Gerber preview

## Custom Footprints

Custom KiCad footprints were created where appropriate, including footprints for:

- STM32 NUCLEO-F303K8 carrier connections
- BME280 sensor module
- TO-92 transistor layout

Dimensions, pin spacing, drill sizes, and component orientation were checked against component/module documentation before PCB fabrication.

## Firmware

The PCB is designed to work with firmware developed in C using the STM32 HAL.

The firmware includes:

- GPIO control
- I2C communication
- BME280 sensor interfacing
- Timer interrupts
- 7-segment display multiplexing
- 74HC595 shift-register control
- External button interrupts
- Button debouncing
- UART communication and debugging

## Design Verification

Before generating the manufacturing files, the PCB was checked using KiCad's Design Rule Checker.

Final manufacturing files were also visually inspected to verify:

- Board outline
- Front and back copper
- Ground pours
- Through-hole locations
- Via locations
- PTH and NPTH drill files
- Solder-mask openings
- Silkscreen placement
- Mounting-hole clearances

## PCB Layout

PCB layout images will be added here.

<!--
Example:

![PCB Layout](images/pcb-layout.png)
-->

## Schematic

Schematic images will be added here.

<!--
Example:

![Schematic](images/schematic.png)
-->

## Manufactured PCB

The PCB has been submitted for fabrication.

Photos of the manufactured board will be added once it arrives.

<!--
![Bare PCB](images/bare-pcb.jpg)
-->

## Assembly and Testing

**Status: Awaiting PCB fabrication**

Once the boards arrive, the PCB will be:

- Visually inspected
- Checked for shorts before power-up
- Assembled and soldered
- Tested for correct power and ground connections
- Tested with the STM32 NUCLEO-F303K8
- Tested with the BME280 over I2C
- Tested for 7-segment display operation
- Tested for pushbutton input
- Verified through UART debugging

Results, photographs, and any hardware revisions will be documented here after board bring-up.

## Tools

### Hardware Design
- KiCad 10
- Digital multimeter
- Soldering equipment

### Embedded Development
- STM32CubeIDE
- STM32CubeMX
- STM32 HAL
- C
- Git / GitHub

## Project Status

- [x] Breadboard prototype
- [x] Firmware development
- [x] Schematic capture
- [x] Footprint selection and verification
- [x] Custom footprint creation
- [x] PCB placement and routing
- [x] Design Rule Check
- [x] Gerber and drill generation
- [x] Manufacturing file verification
- [x] PCB submitted for fabrication
- [ ] PCB received
- [ ] PCB assembled
- [ ] Initial board bring-up
- [ ] Hardware validation
- [ ] Final demonstration

## Future Updates

Once the PCB is assembled and tested, this repository will be updated with:

- Bare PCB photographs
- Assembly photographs
- Completed hardware photographs
- Board bring-up results
- UART/debugging output
- Final demonstration video
- Any design issues discovered during testing
- Potential improvements for a future PCB revision
