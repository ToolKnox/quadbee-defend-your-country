# QuadBee — Firmware, Betaflight, and First-Arm Guide

QuadBee uses a SpeedyBee F405 V3 flight controller stack with Betaflight, ExpressLRS receiver, GPS, VTX/SmartAudio, and a 7 inch 6S motor setup.

## Safety first

- Remove propellers before every firmware, receiver, motor, and ESC test.
- Use a smoke stopper for first battery power.
- Never power a VTX without an antenna attached.
- Do not arm indoors or near people.

## Required tools

- Betaflight Configurator.
- ExpressLRS-compatible transmitter/module matching the receiver region.
- USB-C cable that supports data.
- Fully charged but safely handled 6S battery for ESC/motor tests.

## Flash Betaflight

1. Connect the SpeedyBee F405 V3 by USB.
2. If needed, hold the boot/DFU button while plugging in.
3. In Betaflight Configurator, flash the correct SpeedyBee F405 V3 target.
4. Connect after flashing and apply basic settings.

CLI baseline from the existing build guide:

```text
set board_name=SPEEDYBEEF405V3
set serialrx_provider=ExpressLRS
save
```

## Ports tab

| UART | Function | Setting |
|---|---|---|
| UART3 | ExpressLRS receiver | Serial RX enabled |
| UART6 | BN-220 GPS | GPS enabled |
| SmartAudio UART/pad | AKK Race Ranger VTX | VTX/SmartAudio enabled where wired |

Disable unused UART functions to avoid conflicts.

## Receiver binding

1. Configure the transmitter for ExpressLRS.
2. Power the receiver with props removed.
3. Put the receiver/module into bind mode according to the ELRS version used.
4. Confirm solid receiver LED after binding.
5. In Betaflight Receiver tab, verify AIL/ELE/THR/RUD move correctly.
6. Set channel endpoints near 1000/1500/2000.

## Motor and ESC verification

1. Remove props.
2. In Betaflight Motors tab, acknowledge the safety warning only after checking props are off.
3. Spin each motor one at a time at low throttle.
4. Confirm motor order matches the diagram in `build_guide.md`.
5. Confirm rotation direction. If wrong, use BLHeli/ESC configurator or swap two motor wires.

## GPS setup

1. Enable GPS on the UART used by BN-220.
2. Set protocol to UBLOX unless the module requires another setting.
3. Test outdoors with a clear sky view.
4. Wait for satellite count and lock before relying on GPS rescue.

## VTX / SmartAudio setup

1. Attach antenna before power.
2. Enable SmartAudio/VTX control on the configured UART or pad.
3. Set legal channel and power for your region.
4. Confirm OSD shows VTX channel/power if wired through the FC.

## First arm checklist

1. Props still removed.
2. Receiver channels correct.
3. Modes configured for ARM, ANGLE/HORIZON/ACRO as desired, BEEPER if fitted.
4. Failsafe configured and tested.
5. Accelerometer calibrated on a level surface.
6. Motors spin in correct order and direction.
7. Battery voltage reads correctly.
8. Only then install props for a short outdoor hover test.

## Field pre-flight

- Frame screws tight.
- Arms straight.
- Antennas attached.
- Battery strap secure.
- Props undamaged and installed in correct direction.
- ELRS link and RSSI/LQ healthy.
- GPS lock if using GPS features.
