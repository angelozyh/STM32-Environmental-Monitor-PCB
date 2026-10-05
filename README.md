# STM32 Environmental Monitor PCB

A custom 2-layer PCB designed in KiCad for an STM32-based environmental monitoring system. The board integrates an STM32 NUCLEO-F303K8, BME280 environmental sensor, dual SN74HC595 shift registers, a 4-digit 7-segment display, transistor-based digit drivers, and a pushbutton interface.

This project is the hardware implementation of my previously breadboarded STM32 environmental monitoring system. The project involved transitioning the working prototype to a custom PCB through schematic capture, footprint selection, PCB layout and routing, fabrication, hand assembly, board bring-up, troubleshooting, and final hardware validation.

## Demo

<p align="center">
  <img width="700" alt="STM32 Environmental Monitor Demo" src="https://github.com/user-attachments/assets/ca2668f1-1ec5-4a4f-b1e0-0834c702fe95" />
</p>


The pushbutton cycles the displayed measurement between temperature, humidity, and pressure.

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

Two SN74HC595 shift registers expand the available GPIO and provide the signals required to control the display. Four NPN transistors provide low-side switching for digit selection.

A pushbutton cycles the displayed measurement between:

- Temperature
- Humidity
- Pressure

UART communication is also available for system monitoring and debugging.

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

## Schematic

The original breadboard circuit was converted into a complete KiCad schematic before PCB layout.

<p align="center">
  <img width="900" alt="STM32 Environmental Monitor Schematic" src="https://github.com/user-attachments/assets/6bb69254-032c-4f98-ae5f-8a2b62d0e20f" />
</p>

## PCB Design

The PCB was designed in **KiCad 10** as a 2-layer carrier board for the STM32 environmental monitoring system.

<p align="center">
  <img width="700" alt="STM32 Environmental Monitor PCB Layout" src="https://github.com/user-attachments/assets/2747bafa-6a81-4873-bdef-29c602641dad" />
</p>


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

The board primarily uses through-hole components to simplify hand assembly, modification, and component replacement.

### 3D Preview

<p align="center">
  <img width="650" alt="STM32 Environmental Monitor 3D Render" src="https://github.com/user-attachments/assets/89402739-f14f-4fa0-8f0a-80f19b600566" />
</p>

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
13. Hand assembling and soldering the fabricated PCB
14. Performing electrical checks and initial board bring-up
15. Troubleshooting and correcting hardware issues
16. Validating the completed system

## Custom Footprints

Custom KiCad footprints were created where appropriate, including footprints for:

- STM32 NUCLEO-F303K8 carrier connections
- BME280 sensor module
- TO-92 transistor layout

Dimensions, pin spacing, drill sizes, and component orientation were checked against component and module documentation before PCB fabrication.

## Firmware

Firmware was developed in C using STM32CubeIDE and the STM32 HAL.

The firmware includes:

- GPIO control
- I2C communication
- BME280 sensor interfacing
- Timer interrupts
- 7-segment display multiplexing
- SN74HC595 shift-register control
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

## Assembly and Board Bring-Up

After fabrication, the PCB was assembled and soldered by hand. Socketed components were used where practical to simplify component replacement and troubleshooting.

Initial bring-up included:

- Visual inspection
- Continuity and short-circuit checks
- Power and ground verification
- STM32 power-up and firmware testing
- BME280 I2C communication testing
- Shift-register testing
- 7-segment display testing
- Pushbutton input testing
- UART debugging

<p align="center">
  <img width="650" alt="Finished Assembled PCB" src="https://github.com/user-attachments/assets/ca4c7ac2-859c-499e-bf24-5878283e3a44" />
</p>

## Hardware Revision

During initial board bring-up, testing identified missing power and ground connections in the shift-register circuitry.

The issue was diagnosed through electrical measurements and inspection of the schematic and PCB connections. Jumper wires were added to provide the required power and ground connections.

After the hardware correction, the board was retested and full system functionality was verified.

<p align="center">
  <img width="650" alt="PCB Hardware Revision - Correction Wires" src="https://github.com/user-attachments/assets/70c04cd5-b4af-4c3a-abc4-d039ae9c8ee3" />
</p>

The required connections will be incorporated directly into the PCB layout in a future board revision.

## Final Validation

Following the hardware correction, the completed PCB successfully demonstrated:

- BME280 temperature, humidity, and pressure measurements
- I2C communication
- SN74HC595 shift-register operation
- Timer-based 7-segment display multiplexing
- Pushbutton measurement selection
- UART monitoring and debugging
- Stable operation of the assembled system

The final PCB reproduces the functionality of the original breadboard prototype on a dedicated custom board.

## Tools

### Hardware Design and Assembly

- KiCad 10
- Digital multimeter
- Soldering equipment
- KiCad Gerber Viewer

### Embedded Development

- STM32CubeIDE
- STM32CubeMX
- STM32 HAL
- C
- Tera Term
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
- [x] PCB fabrication
- [x] PCB assembly
- [x] Initial board bring-up
- [x] Hardware troubleshooting and rework
- [x] Hardware validation
- [x] Final demonstration

## Future Improvements

A future PCB revision would incorporate the shift-register power and ground corrections identified during board bring-up directly into the PCB layout.

Additional improvements could include:

- Further optimization of component placement and routing
- Reduction of overall board size
- Improved silkscreen organization
- Additional test points for easier board bring-up and debugging
