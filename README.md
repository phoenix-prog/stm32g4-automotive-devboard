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

/hardware           - KiCad schematic, PCB layout, BOM, Gerbers
/datasheets       - Component datasheets
/firmware           - STM32CubeIDE projects
/examples         - Example firmware (CAN echo, logger, OBD-II)
/docs               - Getting started guide, design notes, test reports
/images             - Photos of assembled boards

## Development Timeline

| Week | Phase | Deliverable |
|------|-------|-------------|
| 1-2 | Schematic Design | Complete schematic, BOM with availability check |
| 3-4 | PCB Layout | 4-layer board layout, DRC clean, Gerbers |
| 5-6 | Manufacturing & Assembly | Order PCBs, assemble, bring-up testing |
| 7-8 | Debug & Rework | Fix hardware issues, test all peripherals |
| 9 | Firmware Example 1 | CAN echo/bridge working |
| 10 | Firmware Example 2 | CAN datalogger working |
| 11 | Firmware Example 3 | OBD-II reader working |
| 12 | Documentation & Release | Complete docs, publish v1.0 |

## Current Progress

- [x] GitHub repo created
- [x] KiCad project initialized
- [x] Folder structure
- [x] README with timeline
- [ ] Block diagram
- [ ] BOM with part availability
- [ ] Power supply schematic
- [ ] MCU schematic
- [ ] Peripheral schematics (CAN, USB, SD, RTC)
- [ ] PCB layout
- [ ] Manufacturing
- [ ] Bring-up
- [ ] Firmware examples
- [ ] Documentation

## Bill of Materials

See [hardware/bom.csv](hardware/bom.csv) for complete part list (in progress)

**Estimated Cost per Board:** ₹980 (~$12 USD)  
**PCB Cost (4-layer, qty 5):** ₹600 (~$7 USD)

## License

MIT License - see [LICENSE](LICENSE) file

**TL;DR:** Use this design for anything (commercial or personal), just keep the license notice.

## Author

**Vaibhav** - Hardware Design Engineer  
Pune, India

- GitHub: [@phoenix-prog](https://github.com/phoenix-prog)
- Project: Automotive embedded systems, CAN bus, EV charging infrastructure

---

**Started:** April 25, 2026  
**Last Updated:** April 25, 2026

*This is a learning project. Expect bugs in v1.0. All feedback welcome via GitHub Issues.*