# CAT-01 YAESU FT-710

CAT-01 is a radio-specific CAT interface for connecting the **ESP32 CW Keyer V2** universal 3.3 V UART CAT port to the **Yaesu FT-710 CAT-3** interface.

> **Project status:** PCB production files completed. Hardware testing with the assembled PCB and FT-710 is still pending.

## Purpose

The ESP32 CW Keyer V2 uses 3.3 V UART levels on its universal CAT connector. The FT-710 CAT-3 interface uses 5 V TTL levels. CAT-01 provides the required interface between both devices.

The design uses an **SN74HCT125N** powered from 5 V for the Keyer-to-radio path and a resistor divider for the radio-to-Keyer path.

## Connections

### J1 — KEYER_CAT

| Signal | Function |
|---|---|
| +5V | Power for CAT-01 |
| KEYER_RX_3V3 | CAT data from radio to Keyer |
| KEYER_TX_3V3 | CAT data from Keyer to radio |
| GND | Ground |

Always follow the **signal names printed on the final PCB silkscreen** when wiring the connector.

### J2 — FT-710 CAT-3

| CAT-01 signal | FT-710 TUNER/LINEAR CAT-3 connection |
|---|---|
| GND | Pin 3 — GND |
| FT710_TXD_5V | Pin 4 — TXD from FT-710 |
| FT710_RXD_5V | Pin 5 — RXD to FT-710 |

**Important:** FT-710 TUNER/LINEAR **pin 1 (+13 V) must not be connected to CAT-01**.

## Signal paths

**Keyer → FT-710**

`KEYER_TX_3V3 → SN74HCT125N → R3 100 Ω → FT710_RXD_5V → FT-710`

**FT-710 → Keyer**

`FT710_TXD_5V → R1/R2 level divider → KEYER_RX_3V3 → ESP32 CW Keyer V2`

## Main components

| Reference | Value / type |
|---|---|
| U1 | SN74HCT125N, DIP-14 |
| C1 | 100 nF |
| R1 | 10 kΩ |
| R2 | 20 kΩ |
| R3 | 100 Ω |
| R4 | 1 kΩ |
| D1 | Power LED |

## Repository layout

The project will contain:

- `KiCad/` — editable KiCad schematic, PCB and project files
- `Gerbers/` — final manufacturing Gerber/drill package
- `Documentation/` — connection and production documentation
- `Photos/` — photographs of the assembled/tested adapter when available

## Manufacturing status

The final KiCad design was checked with:

- 0 DRC violations
- 0 unconnected items
- 0 schematic parity issues

A final visual PCB inspection was also performed and the routing near a via was corrected before regenerating the manufacturing files.

The Gerber package includes front/back copper, front/back solder mask, front/back silkscreen, Edge.Cuts, PTH drill, NPTH drill and Gerber job data.

## Hardware verification

The PCB has been sent for manufacture. The design should therefore currently be treated as **production files completed / hardware test pending**.

After the first assembled CAT-01 has been tested with the ESP32 CW Keyer V2 and a Yaesu FT-710, this section will be updated with the measured/test results and photographs.

## Related project

CAT-01 is intended to be used with the **ESP32 CW Keyer V2**. The Keyer keeps a universal CAT connector so that separate radio-specific adapters can be developed without changing the complete Keyer PCB.

## Disclaimer

This is an amateur-radio DIY hardware project. Verify connector pinout, supply voltage and signal levels before connecting the adapter to a transceiver. In particular, do not connect the FT-710 +13 V pin to CAT-01.
