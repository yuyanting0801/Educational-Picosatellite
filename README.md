# References — device-level hardware notes

Hardware verification notes for the Educational Picosatellite interface board. One file per device, named after the chip. Each file is written against the manufacturer datasheet listed in it and follows the same shape: **pinout → design decisions → checks and notes** (plus bring-up where it matters).

| File | Device | Part | Datasheet | Covers |
|---|---|---|---|---|
| [PCA9554APW.md](PCA9554APW.md) | NXP 8-bit I²C I/O expander | PCA9554APW, TSSOP-16 | [PCA9554_9554A.pdf](/Datasheet/PCA9554_9554A.pdf) | Address `0x38`, 220 Ω CAN_EN series resistors, pin map and reset state |
| [MCP2515.md](MCP2515.md) | Microchip stand-alone CAN controller | MCP2515-I/SO, SOIC-18 | [MCP2515.pdf](/Datasheet/MCP2515.pdf)  | Correct SOIC-18 pinout, SPI interface, 8 MHz crystal, bit timing |
| [SN65HVD230.md](SN65HVD230.md) | TI 3.3 V CAN transceiver | SN65HVD230DR, SOIC-8 | [SN65HVD230DR.pdf](/Datasheet/SN65HVD230DR.pdf)  | `RS` 0 Ω = high-speed mode, Vref handling, split termination, PESD1CAN |
| [INA226.md](INA226.md) | TI current/power monitor | INA226AIDGS, VSSOP-10 | [ina226.pdf](/Datasheet/ina226.pdf)  | 5 mΩ shunt, Kelvin sensing, 10 Ω + 100 nF input filter, calibration |
| [LSM6DSO.md](LSM6DSO.md) | ST 6-axis IMU | LSM6DSOETR3, LGA-14L | [LSM6DSOETR3.pdf](/Datasheet/LSM6DSOETR3.pdf)  | Mode 1 I²C at `0x6A`, `CS` high, INT1 power-on constraint |
| [LIS2MDL.md](LIS2MDL.md) | ST 3-axis magnetometer | LIS2MDLTR, LGA-12L | [LIS2MDLTR.pdf](/Datasheet/LIS2MDLTR.pdf)  | I²C `0x1E`, mandatory 220 nF `C1` (low ESR), pull-up margin |
| [RaspberryPi5.md](RaspberryPi5.md) | Raspberry Pi 5 (BCM2712) | — | — (six source PDFs listed in the file) | 85 × 56 envelope, 58 × 49 hole array, 40-pin header, power, PCIe FFC |

## Board map

| Board | Role |
|---|---|
| **Bridge_Left** | Left bridge board — CAN backbone, PCA9554A per-layer `CAN_EN`, split termination |
| **Bridge_Right** | Right bridge board — power distribution, reserved CAN-B |
| **Power.Pi_Level** | L1 power sheet — 5 V entry, INA226 telemetry, watchdog, `J_PI` |
| **CAN.Pi_Level** | L1 CAN/sensor sheet — MCP2515, SN65HVD230, LSM6DSO |
| **Mag_board** | Magnetometer board — LIS2MDL on a 10 × 10 mm satellite board |

