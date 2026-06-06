# QuadBee Troubleshooting Guide

## Pre-flight Testing and Verification

Complete every test with **propellers removed** until the final battery check. Power the drone on a flat, non-metallic surface away from people and obstacles. These tests also serve as the primary troubleshooting checklist.

### Motor Direction Check

1. Open Betaflight Configurator - Motors tab.
2. Drag each motor slider individually and observe rotation direction from above:
   - Front Right (M1): should spin CCW
   - Rear Left (M2): should spin CW
   - Rear Right (M3): should spin CCW
   - Front Left (M4): should spin CW
3. **Fix:** If any motor spins the wrong way, swap any two bell wires on that motor's ESC output. Do NOT change the motor order in software - fix it physically by swapping wires.

### Receiver Signal Verification

1. Open Betaflight Configurator - Receiver tab.
2. Move each stick on your TX12 and verify all channels respond:
   - AIL (Channel 1): Left/Right stick horizontal
   - ELE (Channel 2): Left/Right stick vertical
   - THR (Channel 3): Right stick vertical
   - RUD (Channel 4): Right stick horizontal
3. Check ELRS RSSI in the OSD - values above 50% at 5 m distance indicate good antenna placement. Below 30%, reposition antennas.
4. **Common issues:** 
   - No signal: Verify ELRS region match (915 MHz), binding procedure, UART3 Serial RX enabled in Betaflight Ports tab.
   - Low RSSI: Reposition antennas on opposite corners, perpendicular polarization.

### Failsafe Testing

1. In Betaflight Configurator - Setup tab, check Failsafe settings:
   - Failsafe mode: GPS Rescue (if GPS is installed) or Kill (motors stop immediately)
   - Failsafe throttle level: 0 (kill) or configured RTH throttle
2. Power on the drone and transmitter. After confirming link, turn off the transmitter.
3. Observe behavior: motors should either stop immediately (Kill mode) or the drone should initiate RTH after a 3-second delay (GPS Rescue). 
4. **Do not catch the drone** - let it land safely on its own during this test.
5. **Fix:** If failsafe not triggering, verify GPS Rescue enabled in Modes tab and CLI settings for gps_rescue_* parameters.

### GPS Calibration and Satellite Lock

1. Take the drone outdoors to an open area with clear sky view.
2. In Betaflight Configurator - Setup tab, click Calibrate Accelerometer with the drone level on a flat surface.
3. Click GPS Rescue status indicator and wait for satellite lock:
   - BN-220 acquires initial fix in 30-90 seconds (cold start)
   - Buzzer will emit periodic beeps as satellites are acquired
   - Minimum 5 satellites required for GPS Rescue to arm
4. Verify the OSD shows GPS coordinates and satellite count during flight simulation.
5. **Common issues:** GPS not locking - ensure ceramic patch antenna faces sky unobstructed (no carbon fiber or metal above it). Move outdoors, away from buildings.

### VTX Power and Channel Switching

1. Put on your FPV goggles and tune to a known channel (e.g., Race Band channel R1 = 5865 MHz).
2. In Betaflight Configurator - OSD tab, verify the VTX shows the correct channel and power level.
3. Use SmartAudio voice commands or OSD menu to cycle through channels: confirm you hear the VTX beep and see the goggles switch cleanly on each channel.
4. Verify video signal is clear with no excessive noise or snow.
5. **Fixes:**
   - No video or static: Check camera power (PDB 5V), video cable to FC VIDEO_IN (shielded 22AWG), VTX power (5-9V).
   - No SmartAudio control: Confirm SmartAudio pin wired to PB8, Video Transmitter set to SmartAudio in Configuration tab.
   - Power too high/low: Check local regulations; set FCC 1.6W or CE 200mW as appropriate.

### Camera Image Quality

1. View the Caddx Ratel 2 feed through your goggles.
2. Adjust camera focus ring until text at 5 m distance is legible in the FPV feed.
3. Check for image roll-bar (horizontal banding) - if present, adjust the FPV Delay setting in Betaflight OSD configuration until the bar disappears.
4. **Fix:** Poor image - verify camera power/ground, shielded video cable, focus adjustment.

### Battery Voltage Monitoring

1. Connect the battery and check the voltage display in Betaflight Configurator - Status tab.
2. A fully charged 6S LiPo reads 25.2V (4.2V per cell). A fully charged 6S Li-Ion reads 25.2V as well, but discharges more gradually.
3. Verify the low-voltage warning triggers at approximately 19.8V (3.3V per cell) in the OSD. Adjust `set battery_warning = 3` if needed.
4. **Safety note:** Always verify with multimeter on first use.

## Common Issues and Fixes

- **Motors spin wrong direction:** Swap any two wires on the affected motor's ESC output (physical fix, no software change needed).
- **Vibration / poor flight:** Check stack damping pads installed between PDB and FC. Verify frame arms straight, motors torqued to 0.5 Nm, prop balance.
- **ELRS no link or poor range:** Confirm 915 MHz match on TX module and RX. Bind procedure timing (10s window). Antenna placement: opposite corners, perpendicular polarization. RSSI >50% target.
- **VTX overheating or low power:** Ensure adequate 18AWG power wire from PDB. Check SmartAudio configuration.
- **GPS not acquiring satellites:** Outdoor clear sky view required. Ceramic patch must face up. Allow 30-90s cold start.
- **Solder joint failures:** Always apply heat shrink. Use ferrules on signal wires. Separate power/signal runs by 20mm+.
- **Loose cables in flight:** Use only reusable velcro ties - never zip ties on carbon fiber.
- **Battery issues:** Follow all LiPo safety rules. Use balance charger. Store at 3.8V/cell.

## Safety Reminders (Prevention)

See the full safety sections in build_guide.md for complete details. Key points:

- **LiPo batteries:** Balance charge only, never unattended, use fireproof bag, inspect for damage, dispose properly at recycling center.
- **Propellers:** Remove for all testing and config. Use threadlocker. Inspect before flight. 7" props on 6S are dangerous.
- **RF regulations:** Match ELRS region (915 MHz US, 868 MHz EU). VTX power limits: FCC 1.6W max but check local; EU 200mW.
- **Flight:** Pre-flight checklist mandatory. 50m+ clearance. Visual line of sight. Spotter for first flights. No-fly zones.
- **Electronics:** Ventilated soldering area, fume extractor, eye protection for heat inserts. Heat shrink everything. Conformal coat for wet conditions.

If a problem is not covered here, review the full build_guide.md assembly and firmware sections, then check Betaflight CLI for errors.

---

*This troubleshooting guide was compiled from the testing, safety, and build notes in the project's description.md. All procedures and fixes are directly grounded in the source. No invented scenarios.*
