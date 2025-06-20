# A9Pro
A deep dive into the A9 Pro ANC earphones.

I've bought multiple units, one is white and branded "SONY" and the other one is unmarked (with a satin black finish)
The black unbranded one was listed as having a Jieli 7003 MCU, but they contain the same AB5682B IC.

## Main Chip: Bluetrum AB5682B

Both devices contain a chip marked ET581632B

### Decoding the Chip Markings

Based on [kagaimiq/bluetrum-tools](https://github.com/kagaimiq/bluetrum-tools):

- `ET581632B` decodes as:
  - `E` → Codename `EAGR` → **AB568x family**
  - `T5` → Unknown
  - `8` → Unknown
  - `1632` (Hexadecimal) → **5682** (Decimal)
  - `B` → Variant

The main IC is marked with the AB logo, so the chip is confirmed to be an AB5682B.

This is a pretty interesting MCU since it's a 32-bit 140MHz RISC-V processor with integrated NOR flash (16Mbit).
It's designed with smart wearables in mind. 

The [datasheet](Datasheets/MCU/AB5682B.pdf) is included in this repo.  (English)

## LCD Display

### General Info

- **Type**: Rectangular 1.46" IPS panel
- **Touch Controller**: CST08 (SPI, QFN3x3-20L)
- **Pin Count**: 15-pin FPC (shared 6 pins with touch)

| Unit   | LCD Ribbon Marking                | Touch Ribbon | Date Code     |
|--------|----------------------------------|---------------|---------------|
| "Sony" | HXW661257BXH145 CH.              | HXW661079V1.0 | 2025/02/28    |
| Black  | TX145B163 XH                     | MF-7221 HT    | 2024/08/10    |

## Touch Controller

- **Chip**: CST08
- **Interface**: SPI
- **Package**: QFN3×3-20L
- **Lines**: 6 pins on FPC

[Datasheet](Datasheets/TP/CST08C-Hynitron.pdf) for the TP controller. (Chinese)

## PMIC

- **Vendor**: LowPowerSemi (LPS)
- **Model**: LP7812C EK1
- **Function**: TWS charging case PMIC with two-way communication

I've found the [datasheet](Datasheets/PMIC/f54fe7033996903f5639f41d20033a11.pdf), a [pinout](Datasheets/PMIC/133637571110098771.jpg), and a [brochure](Datasheets/PMIC/a513f1c313a75f147b4eed0bbb0ec916.pdf) (Chinese)

## PCB

The PCB is marked ST8_YX_Y15仓_5682_V1.0 2024_08_07 for the black unit.

It has a bunch of test pads labeled:
#### Bottom Side

| Label  | Description        |
|--------|--------------------|
| DM     ||
| PINT   ||
| G      | GND                |
| UP     ||
| 3V3    ||
| 5V     ||
| PRST   ||
| PSCL   ||
| PSDA   ||
| SCL    ||
| RS     ||
| SDA    ||

#### Top Side

| Label  | Description        |
|--------|--------------------|
| CS     ||
| RST    | Reset              |
