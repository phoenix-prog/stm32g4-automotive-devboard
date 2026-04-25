# stm32g4-automotive-devboard
Open-source automotive development board for CAN bus applications
# STM32G4 Automotive Development Board

Open-source development board designed for automotive CAN bus applications, built to survive harsh vehicle electrical environments.

## 🚧 Status: In Development

**Current Phase:** Schematic Design (Week 1 of 12)  
**Target Completion:** July 2026

## Features

- **MCU:** STM32G431CBT6 (Cortex-M4F @ 170MHz, 128KB Flash, 32KB RAM)
- **Dual CAN:** Automotive-grade transceivers (TJA1051) with galvanic isolation
- **Power Input:** 6-36V with reverse polarity protection, TVS transient suppression
- **USB:** USB-C for programming, debugging, and serial communication
- **Storage:** Micro-SD card slot for data logging
- **RTC:** Real-time clock with CR2032 battery backup
- **Debug:** Tag-Connect compatible SWD pads + optional 10-pin header
- **Protection:** ESD protection on CAN and USB, automotive-grade components throughout

## Why This Board?

Hobby dev boards (Blue Pill, Arduino CAN shields) fail in real automotive environments due to:
- Poor power supply regulation (can't handle voltage transients)
- No ESD/EMI protection
- Non-automotive grade components
- Flimsy connectors that vibrate loose

This board is designed from the ground up for **in-vehicle development and testing**.

## Example Projects (Planned)

1. **CAN Bus Echo/Bridge** - Bidirectional CAN1 ↔ CAN2 gateway
2. **CAN Datalogger** - Timestamp and log all CAN traffic to SD card
3. **OBD-II Reader** - Query vehicle diagnostics (RPM, speed, temps, codes)

## Repository Structure