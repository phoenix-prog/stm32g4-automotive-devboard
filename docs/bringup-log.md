# Rev A Bring-up Log

Fill this in as you work. Every entry: date, what you did, what you measured, instrument, photo or capture file, pass/fail.

## Board info

| Board | Serial / marking | Assembled by | Date |
|---|---|---|---|
| | | | |

## 1. Visual and passive checks (unpowered)

- [ ] Visual inspection under magnification: solder bridges, orientation of ICs, diodes, TVS, electrolytics
- [ ] Resistance input → GND, 5 V → GND, 3.3 V → GND (no shorts)

## 2. First power (current-limited PSU)

| Step | Limit | Expected | Measured | Pass |
|---|---|---|---|---|
| Vin 12 V, current limit ~100 mA | | | | |
| 5 V rail | | | | |
| 3.3 V rail | | | | |
| Ripple on 5 V / 3.3 V (scope, ground spring) | | | | |

## 3. Input stage (requirements PWR-xx)

| ID | Test | Result | Capture |
|---|---|---|---|
| PWR-02 | | | |
| PWR-03 | | | |
| PWR-08 | | | |

## 4. MCU

- [ ] SWD connects, device ID read
- [ ] HSE oscillates (scope capture)
- [ ] System bootloader via BOOT0
- [ ] Blinky from register-level firmware

## 5. USB and CAN

- [ ] USB enumerates (DFU)
- [ ] CAN-05 classic CAN test
- [ ] CAN-06 CAN FD test
- [ ] CANH/CANL scope capture: dominant/recessive levels, edges

## Anomalies

| # | Symptom | Root cause | Fix / rework | Rev B change |
|---|---|---|---|---|
| | | | | |
