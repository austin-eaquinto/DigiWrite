# DigiWrite

![Status](https://img.shields.io/badge/status-work%20in%20progress-orange) ![Platform](https://img.shields.io/badge/platform-ESP32--S3-blue) ![Display](https://img.shields.io/badge/display-ST7796S-purple) ![License](https://img.shields.io/badge/license-MIT-green)

> 🚧 **Work in progress.** This project is under active development. Pin assignments,
> class structure, and APIs may change, and nothing here is production-ready yet.

## Overview
DigiWrite is an embedded firmware project for the ESP32-S3 that aims to recognize
handwriting directly on a touchscreen. The current goal is for users to write individual letters
freehand on the ST7796S display and have them interpreted and converted into digital text.

## Current Status
**Working on now:** there is a bug between `TouchScreen` driver and `Canvas` classes causing a delay in processing the physical input.

**Not started yet:** letter recognition and text output.

### Roadmap
- [x] Wire up the display and touch controller on a shared SPI bus
- [x] `DisplayScreen` class: address window and bounded drawing
- [x] `TouchScreen` class: coordinate capture and data logging
- [x] Touch interrupt handler (T_IRQ)
- [ ] Stroke capture and normalization
- [ ] Single-letter recognition
- [ ] Convert recognized letters to on-screen text
- [ ] Documentation, demo, and cleanup

## Hardware Requirements
**Microcontroller:** ESP32-S3 DevKit C-1 N8R8<br>
**Display/Touch:** ST7796S TFT touchscreen<br>
**Additional Components:** 1x 10kΩ pull-up resistor (T_IRQ line to 3.3V)<br>
**Power:** 5V via VIN pin

### Pin Connections (subject to change)

| ST7796S Pin | ESP32 GPIO | Description |
|-------------|------------|-------------|
| **Touch Controller** | | |
| T_IRQ | 36 | Touch interrupt, 10kΩ pull-up to 3.3V |
| T_DO | 11 | Touch SPI MISO |
| T_DIN | 13 | Touch SPI MOSI |
| T_CLK | 12 | Touch SPI clock |
| T_CS | 10 | Touch chip select |
| **Display** | | |
| SDO (MISO) | 11 | Display SPI MISO, shared with T_DO |
| SDI (MOSI) | 13 | Display SPI MOSI, shared with T_DIN |
| SCK | 12 | Display SPI clock, shared with T_CLK |
| CS | 5 | Display chip select |
| DC/RS | 17 | Data/command select |
| RESET | 4 | Display reset |
| LED | 2 | Backlight: GPIO for PWM dimming or 3.3V for constant on |
| **Power** | | |
| VCC | VIN | 5V power |
| GND | GND | Ground |

## Classes (WIP)
| Name | Purpose | Status |
|------|---------|--------|
| `main.cpp` | Calls classes and runs the program | Stub |
| `TouchScreen` | Handles coordinate math and data logging | In progress |
| `DisplayScreen` | Creates an address window so data displays within set bounds | In progress |
| `Canvas.cpp` | In the process of designing this to handle and display user input through the other classes | In progress |

## Contributing
Feedback and suggestions are welcome while the design is still taking shape.
Please open an issue before submitting a large pull request.

## License
MIT
