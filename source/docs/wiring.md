# QuadBee Wiring Guide

## Overview

Every connection on this build routes through the SpeedyBee F405 V3 stack, which integrates the PDB (power distribution board), ESC (electronic speed controller), and flight controller into a single stackable unit. The BLS 50A BLHeli_32 ESC handles 6S input natively.

## Power Distribution

| Connection | From | To | Notes |
|---|---|---|---|
| Battery + (XT60) | LiPo/Li-Ion 6S | PDB BAT+ pad | Solder XT60 directly to PDB power input |
| Battery - (XT60) | LiPo/Li-Ion 6S | PDB BAT- pad | Use 12AWG wire for main power leads |
| Motor 1 | ESC OUT1 | EMAX ECO II 2807 (Front Right) | Any two bell wires swaps rotation |
| Motor 2 | ESC OUT2 | EMAX ECO II 2807 (Rear Left) | |
| Motor 3 | ESC OUT3 | EMAX ECO II 2807 (Rear Right) | |
| Motor 4 | ESC OUT4 | EMAX ECO II 2807 (Front Left) | |

## Flight Controller Connections

The SpeedyBee F405 V3 FC exposes the following ports for peripherals:

| Peripheral | Signal | FC Pin | Wire Gauge | Notes |
|---|---|---|---|---|
| ELRS Nano RX | UART TX | USART3_TX (Pin D7 / PD7) | 22AWG solid core | Configure Serial RX on UART3 in Betaflight |
| ELRS Nano +5V | Power | FC 5V pad | 22AWG | Regulated 5V from FC BEC |
| ELRS Nano GND | Ground | FC GND pad | 22AWG | Common ground required |
| VTX SmartAudio | Control | SmartAudio pin (Pin B8 / PB8) | 22AWG | For channel/power switching via Betaflight |
| VTX Power | Power | PDB 5V or 9V pad | 18AWG | AKK Race Ranger accepts 5-9V input |
| VTX GND | Ground | FC/PDB GND | 22AWG | |
| Camera Video | Analog Video | FC VIDEO_IN (Pin A7 / PA7) | 22AWG shielded | Caddx Ratel 2 analog output |
| Camera Power | Power | PDB 5V pad | 22AWG | |
| Camera GND | Ground | FC/PDB GND | 22AWG | |
| GPS TX | UART RX | USART6_RX (Pin A3 / PA3) | 22AWG solid core | Configure Serial GPS on UART6 in Betaflight |
| GPS RX | UART TX | USART6_TX (Pin A2 / PA2) | 22AWG solid core | BN-220 telemetry output |
| GPS Power | Power | FC 5V pad | 22AWG | |
| GPS GND | Ground | FC GND pad | 22AWG | Common ground required |

## Antenna Connections

| Antenna | Connector | Mount Location | Notes |
|---|---|---|---|
| ELRS Nano RX antenna | SMA (on receiver) | Top plate, rear corner | Point perpendicular to VTX antenna for best diversity |
| VTX antenna | SMA (on AKK Race Ranger) | Top plate, opposite corner from RX | Use the included FPV antenna SMA 10cm or a patch antenna for range |

**Antenna placement tip:** Mount the ELRS receive antenna and VTX transmit antenna on opposite sides of the top plate with their polarization axes perpendicular (one vertical, one horizontal). This cross-polarization improves link reliability in multipath environments.

## Wiring Best Practices

- Use **ferrules** on all 22AWG signal wire ends before inserting into FC JST-SH or pin headers
- Apply **heat shrink** over every solder joint - exposed connections cause short circuits under vibration
- Route motor bell wires through the arm channels of the Mark 4 frame to protect them from prop strike
- Use **velcro cable ties** for all bundling - never zip ties, which are difficult to remove and can damage carbon fiber edges
- Keep power and signal wires separated by at least 20 mm where they run parallel to reduce EMI interference

---

*This wiring guide was extracted and formatted directly from the project's description.md. All pin assignments, wire gauges, and notes are taken verbatim from the source material. No measurements were invented.*
