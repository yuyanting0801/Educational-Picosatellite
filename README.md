# References — device-level hardware notes

Hardware verification notes for the Educational Picosatellite interface board. One file per device, named after the chip. Each file is written against the manufacturer datasheet listed in it and follows the same shape: **pinout → design decisions → checks and notes** (plus bring-up where it matters).

| File | Device | Part | Board · ref | Datasheet | Covers |
|---|---|---|---|---|---|
| [PCA9554A.md](PCA9554A.md) | NXP 8-bit I²C I/O expander | PCA9554APW, TSSOP-16 | D1 · `U1` | NXP Rev. 10 | Address `0x38`, 220 Ω CAN_EN series resistors, pin map and reset state |
| [MCP2515.md](MCP2515.md) | Microchip stand-alone CAN controller | MCP2515-I/SO, SOIC-18 | D3b · `U1` | DS21801G | Correct SOIC-18 pinout, SPI interface, 8 MHz crystal, bit timing |
| [SN65HVD230.md](SN65HVD230.md) | TI 3.3 V CAN transceiver | SN65HVD230DR, SOIC-8 | D3b · `U2` | SLOS346O | `RS` 0 Ω = high-speed mode, Vref handling, split termination, PESD1CAN |
| [INA226.md](INA226.md) | TI current/power monitor | INA226AIDGS, VSSOP-10 | D3a · `U3` | SBOS547C | 5 mΩ shunt, Kelvin sensing, 10 Ω + 100 nF input filter, calibration |
| [LSM6DSO.md](LSM6DSO.md) | ST 6-axis IMU | LSM6DSOETR3, LGA-14L | D3b · `U5` | DS12140 Rev. 3 | Mode 1 I²C at `0x6A`, `CS` high, INT1 power-on constraint |
| [LIS2MDL.md](LIS2MDL.md) | ST 3-axis magnetometer | LIS2MDLTR, LGA-12L | D7 · `U1` | DocID030621 Rev. 5 | I²C `0x1E`, mandatory 220 nF `C1` (low ESR), pull-up margin |
| [RaspberryPi5.md](RaspberryPi5.md) | Raspberry Pi 5 (BCM2712) | — | L1 | Product Brief, HAT+ spec, mechanical drawing | 85 × 56 envelope, 58 × 49 hole array, 40-pin header, power, PCIe FFC |

## Board map

| Board | Role |
|---|---|
| **D1** | Left bridge board — CAN backbone, PCA9554A per-layer `CAN_EN`, split termination |
| **D2** | Right bridge board — power distribution, reserved CAN-B |
| **D3a** | L1 power sheet — 5 V entry, INA226 telemetry, watchdog, `J_PI` |
| **D3b** | L1 CAN/sensor sheet — MCP2515, SN65HVD230, LSM6DSO |
| **D7** | Magnetometer board — LIS2MDL on a 10 × 10 mm satellite board |

## Notes

- Figures are in [`reference_img/`](reference_img/); all image links are relative and resolve inside this folder.
- The references cite project-side files (`10_原理图.md`, `eda/*_netlist.txt`, `Datasheet/…`) by section and filename so the design intent stays traceable. Those files are not part of this folder.
- Each chip was checked pin-by-pin against its datasheet (the Raspberry Pi 5 entry is board-level); the "Checks and notes" section records what was verified and any remaining constraint.
- Files are hardware-focused. Register tables appear only where a hardware configuration depends on them (address, mode, bit timing, power-on state).
