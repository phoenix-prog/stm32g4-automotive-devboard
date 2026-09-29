# Rev A Requirements

**Status:** DRAFT — freeze and tag `rev-a-requirements` before opening KiCad.

Every requirement has an ID and a verification method. If you can't say how you'll check a requirement on the bench, it isn't a requirement yet.

Items marked **[DECIDE]** are open. Resolve them before freezing.

---

## 1. Purpose

A bench and in-vehicle development board for register-level STM32G4 firmware and CAN work, whose input stage survives a 12 V vehicle supply.

It is **not** a safety-relevant ECU. It may reset during deep crank. See [ADR 0002](decisions/0002-power-architecture.md).

## 2. Power input

| ID | Requirement | Verification |
|---|---|---|
| PWR-01 | System voltage: 12 V nominal. 24 V systems are out of scope. | — |
| PWR-02 | Operate without reset across 9–16 V continuous input. | Bench PSU sweep 9→16 V; 3.3 V rail and NRST on scope |
| PWR-03 | Survive reverse polarity indefinitely (P-channel MOSFET, high side). | Apply −16 V for 60 s; board then operates normally |
| PWR-04 | Survive the clamped-residual load dump (~35 V), assuming vehicle centralised suppression. Beyond this envelope an active clamp is needed and is out of scope. | Analysis: TVS V_CL at pulse current < buck abs-max with margin |
| PWR-05 | Battery-facing clamp is a load-dump-rated TVS (SM8S / SLD class), unidirectional. Standard SMBJ/SMCJ are not acceptable here. | BOM review |
| PWR-06 | TVS stack holds: 16 V (op max) < V_RWM < V_BR < V_CL(actual) < downstream abs-max. V_CL(actual) = V_CL_rated − R_D × (I_PP_rated − I_PP_actual). | Calculation in ADR 0002 |
| PWR-07 | **[DECIDE]** Survive (not operate through) a 24 V jump start for 60 s. If yes, V_RWM ≥ 24 V, which pushes V_CL up — re-check PWR-06. | Bench PSU at 24 V for 60 s |
| PWR-08 | During crank the board may reset. It must recover cleanly when input returns (brown-out reset enabled, no latch-up, no stuck rail). | Bench PSU dip to ~3 V for 1–2 s, repeat 5×; board reboots every time |
| PWR-09 | Input filter: bulk capacitance (≥ 63 V rated) + series ferrite or inductor. | BOM + layout review |
| PWR-10 | Input stage and bulk capacitors rated for the full input envelope with voltage derating. | BOM review |

## 3. Rails

| ID | Rail | Loads | Design ceiling | Verification |
|---|---|---|---|---|
| RAIL-01 | 5 V | TJA1051 VCC, 3.3 V regulator input, header | 500 mA **[confirm budget]** | Electronic/resistor load to ceiling; ripple on scope |
| RAIL-02 | 3.3 V | MCU, TJA1051 VIO, LEDs, header | 500 mA **[confirm budget]** | As above |
| RAIL-03 | 5 V source ORing: board runs from USB VBUS alone on the bench, from the vehicle input alone, or from both, with no back-feed into USB or into the input stage. | — | — | Test all three source combinations; measure reverse current into VBUS |

Rule: regulator rated output ≈ 2–3× expected load.

## 4. MCU

| ID | Requirement | Verification |
|---|---|---|
| MCU-01 | STM32G431CBT6 (LQFP48). One FDCAN. See [ADR 0001](decisions/0001-mcu.md). | — |
| MCU-02 | HSE crystal for FDCAN bit timing. **[DECIDE]** frequency (8 / 16 / 24 MHz). | Scope HSE; FDCAN bit time measured on bus |
| MCU-03 | NRST with RC and button. BOOT0 pulled to a defined state, with a jumper or button for the system bootloader. | Boot into system bootloader and into flash |
| MCU-04 | All unused GPIO routed to 2.54 mm headers. | Continuity check against pin map |
| MCU-05 | Decoupling per the ST hardware getting-started application note for STM32G4. | Schematic review against the app note |

## 5. CAN

| ID | Requirement | Verification |
|---|---|---|
| CAN-01 | One channel, TJA1051T/3 (VIO pin for 3.3 V logic, CAN FD capable). | — |
| CAN-02 | ESD protection diode on CANH/CANL. | BOM review |
| CAN-03 | Common-mode choke footprint with a 0 Ω bypass option. | Assemble both options; compare |
| CAN-04 | Split termination (2 × 60 Ω + capacitor to GND), switchable by jumper. | Measure bus resistance with jumper in and out |
| CAN-05 | Classic CAN at 500 kbit/s to a known-good node without errors. | 10 min traffic, zero error frames |
| CAN-06 | **[DECIDE]** CAN FD data-phase target (e.g. 2 Mbit/s). | Same test in FD mode |
| CAN-07 | Vehicle connector carries power, GND, CANH, CANL. **[DECIDE]** connector type (locking). | — |

## 6. USB, debug, indicators

| ID | Requirement | Verification |
|---|---|---|
| USB-01 | USB-C device, full speed. 5.1 kΩ pull-downs on CC1 and CC2. ESD protection on D+/D− and VBUS. | Enumerates on a C-to-C cable and a A-to-C cable |
| USB-02 | Firmware update over USB DFU (system bootloader). | Flash via STM32CubeProgrammer over USB |
| DBG-01 | One SWD connector: 10-pin 1.27 mm Cortex debug. Tag-Connect not fitted in Rev A. | First debug session via ST-LINK |
| IND-01 | LEDs: 3.3 V power, one user LED. | Visual |
| TP-01 | Test point on every rail, on input after protection, and on CANH/CANL. | Layout review |

## 7. Board

| ID | Requirement | Verification |
|---|---|---|
| BRD-01 | 4-layer, fab's standard stackup. Stackup and impedance recorded in the layout decision record. | Fab order + ADR |
| BRD-02 | Hand-assemblable: no QFN/BGA; passives 0603 or larger. | BOM review |
| BRD-03 | Mounting holes. **[DECIDE]** board outline. | — |

## 8. Out of scope for Rev A

- Second CAN channel (needs STM32G473/G474 or G491 — see ADR 0001)
- Galvanic isolation
- microSD, RTC, coin cell
- Operation through deep crank (buck-boost) — see ADR 0002
- 24 V systems
- Functional safety, supervision IC, safety partitioning
- OBD-II and datalogger example firmware
