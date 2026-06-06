# QuadBee - Defend Your Country!

Slava Ukraini!
All funds gained from donations and affiliate commission will be going to Ukraine.

## Maker Portal readiness

This repository was created/connected by the Maker Portal software steward so the project has a GitHub source-of-truth record.

- `bom.csv` is exported from the Maker Portal BOM table when BOM rows exist.
- `docs/` contains build/instruction material from the local project folder when available.
- release assets contain a baseline source/archive snapshot for traceability.

## Project description

## 🇺🇦 QuadBee — defend your country

QuadBee is an open-source **7" 6S ExpressLRS FPV quad** built around the Mark 4 frame, SpeedyBee F405 V3 stack, and EMAX ECO II 2807 motors. Print it, build it, fly it — or donate, and I'll build one for Ukraine.

***Any and all hardware and drones assembled from donations to this project are sent to Ukraine after they're built and tested.***

![](https://media.printables.com/media/prints/1457783/rich_content/000b431e-011b-46d6-8779-7590901f4f62/image.png#%7B%22uuid%22%3A%2209374099-4b33-4e1a-b2fa-325ef20c07e6%22%2C%22w%22%3A960%2C%22h%22%3A640%7D)

After the Ukrainian army successfully deployed thousands of drones in the field, I wanted to enable regular people to learn, build, and prepare. Homemade drones are effective, and 3D printers have been absolutely crucial — both in the field and for educational use. The goal of QuadBee is to make it realistic for any maker to build their own drone: for fun, for the FPV experience, or as the starting point for something more serious — defensive, reconnaissance, or humanitarian.

## 📦 Resources

<MAKER:bom-pdf/>
<MAKER:github/>
<MAKER:guides/>

## 💛 How to support

If you'd like to help fund new components and new designs, any amount goes a long way:

- [**Join the club as a Peeky Blinder supporter**](https://www.printables.com/model/1457783-quadbee-defend-your-country#join.@TomKnox.1573)
- [**Donate through PayPal**](https://www.paypal.com/paypalme/TomKnox3d?country.x=SE&locale.x=en_US)

All donations and affiliate commission go directly into hardware for Ukraine.

![](https://media.printables.com/media/prints/1457783/rich_content/c178e49d-30a0-4702-9a48-fb4c65175ba1/image-1.png#%7B%22uuid%22%3A%22adcc0f5a-1e02-4177-98a8-7c8872579452%22%2C%22w%22%3A697%2C%22h%22%3A565%7D)

## 🖨 Print settings

These are the settings that have given the best success on field-grade parts:

- **Material:** PC-CF, PA-CF, ASA, ABS, PCTG or PETG (TPU for the antenna brackets)
- **Layer height:** 0.2 mm
- **Wall count:** 4
- **Solid top/bottom layers:** 5
- **Infill:** 35%
- **Infill pattern:** Gyroid, Honeycomb, Triangle or Cubic
- **Extrusion width:** 0.4 mm

> TODO: confirm typical print time and part weight for the standard 7" frame.

## 🛠 Tools you'll need

There's a fair amount of soldering and heat-insert work in this build — if you're new to either, see <MAKER:guide name="soldering"/>.

<MAKER:tools/>

## 🔧 Build notes

A few things worth knowing before you order parts:

- **Frame size.** The standard build is the 7" Mark 4. There's also a 5" arm variant in the BOM for tighter, more agile builds.
- **Battery choice.** LiPo 6S 7000–10000 mAh gives the best punch for FPV/freestyle. Li-Ion 6S2P is the right call if you're optimising for long-range or surveillance flights.
- **Payload.** A redesigned payload system is in progress. The payload units currently linked in the BOM are interim options that work today.
- **ELRS region.** Build uses 915 MHz ExpressLRS. Match your transmitter module to the receiver region you order — don't mix 868 / 915 / 2.4 GHz.

## ⚡ Wiring Diagram

Every connection on this build routes through the SpeedyBee F405 V3 stack, which integrates the PDB (power distribution board), ESC (electronic speed controller), and flight controller into a single stackable unit. The BLS 50A BLHeli_32 ESC handles 6S input natively.

### Power Distribution

| Connection | From | To | Notes |
|---|---|---|---|
| Battery + (XT60) | LiPo/Li-Ion 6S | PDB BAT+ pad | Solder XT60 directly to PDB power input |
| Battery - (XT60) | LiPo/Li-Ion 6S | PDB BAT- pad | Use 12AWG wire for main power leads |
| Motor 1 | ESC OUT1 | EMAX ECO II 2807 (Front Right) | Any two bell wires swaps rotation |
| Motor 2 | ESC OUT2 | EMAX ECO II 2807 (Rear Left) | |
| Motor 3 | ESC OUT3 | EMAX ECO II 2807 (Rear Right) | |
| Motor 4 | ESC OUT4 | EMAX ECO II 2807 (Front Left) | |

### Flight Controller Connections

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

### Antenna Connections

| Antenna | Connector | Mount Location | Notes |
|---|---|---|---|
| ELRS Nano RX antenna | SMA (on receiver) | Top plate, rear corner | Point perpendicular to VTX antenna for best diversity |
| VTX antenna | SMA (on AKK Race Ranger) | Top plate, opposite corner from RX | Use the included FPV antenna SMA 10cm or a patch antenna for range |

> **Antenna placement tip:** Mount the ELRS receive antenna and VTX transmit antenna on opposite sides of the top plate with their polarization axes perpendicular (one vertical, one horizontal). This cross-polarization improves link reliability in multipath environments.

### Wiring Best Practices

- Use **ferrules** on all 22AWG signal wire ends before inserting into FC JST-SH or pin headers
- Apply **heat shrink** over every solder joint — exposed connections cause short circuits under vibration
- Route motor bell wires through the arm channels of the Mark 4 frame to protect them from prop strike
- Use **velcro cable ties** for all bundling — never zip ties, which are difficult to remove and can damage carbon fiber edges
- Keep power and signal wires separated by at least 20 mm where they run parallel to reduce EMI interference

## 🔨 Assembly Steps

Follow these steps in order. Complete each step fully before moving to the next.

### Phase 1: Frame Preparation

**Step 1 — Inspect all frame parts.** Unpack the Mark 4 7" frame and verify you have: center plate, four arms (each with integrated motor mount), top plate, and all included hardware. Check each arm for straightness — bent arms cause vibration and handling issues.

**Step 2 — Install heat inserts into 3D-printed parts.** If you are printing the frame instead of using carbon fiber arms, insert M3 brass heat inserts into every threaded hole using a soldering iron set to 350°C. Press each insert straight until flush with the surface. Let cool for 10 seconds before applying torque.

**Step 3 — Attach arms to center plate.** Align each arm with the center plate mounting holes. Insert M3 standoffs through the center plate, then secure each arm with M3 countersunk screws. Torque to 0.5 Nm — overtightening cracks carbon fiber or strips printed threads. The Mark 4 uses a standard X-configuration: arms at approximately 45° angles from the forward axis.

### Phase 2: Motor Installation

**Step 4 — Mount motors to arms.** Each EMAX ECO II 2807 motor has four M3 mounting holes matching the arm motor pads. Secure each motor with M3 screws and nylon lock washers. Torque to 0.5 Nm. Verify all four motors sit level with the arm top surface.

**Step 5 — Identify motor rotation direction.** The EMAX ECO II 2807 6S 1300KV motors are not pre-marked CW/CCW. You will determine correct rotation during Betaflight configuration (see Testing section). For now, note which motor is in each position:

| Position | Motor | Expected Rotation (top view) |
|---|---|---|
| Front Right (M1) | CCW | Counter-clockwise |
| Rear Left (M2) | CW | Clockwise |
| Rear Right (M3) | CCW | Counter-clockwise |
| Front Left (M4) | CW | Clockwise |

**Step 6 — Route motor bell wires.** Feed each motor's three bell wires through the arm channels toward the center PDB. Leave approximately 150 mm of wire at the ESC end for soldering. Secure wires inside the arms with small velcro ties so they cannot rattle loose during flight.

### Phase 3: ESC/PDB Stack Assembly

**Step 7 — Assemble the SpeedyBee stack.** The SpeedyBee F405 V3 stack consists of three plates that bolt together:
   - **Bottom plate:** PDB with BLS 50A ESC pads (motor outputs, battery input)
   - **Middle plate:** FC mounting layer with vibration dampening silicone pads
   - **Top plate:** Flight controller board

Stack the plates in order. Insert M3 standoffs through all three layers and secure with M3 screws. Use the included silicone damping balls or pads between the PDB and FC to isolate vibration — this is critical for clean IMU readings.

**Step 8 — Solder motor bell wires to ESC pads.** On the bottom of the PDB, you will find four sets of three solder pads labeled OUT1 through OUT4. Solder each motor's three bell wires to its corresponding output:
   - OUT1 → Front Right motor (any wire order)
   - OUT2 → Rear Left motor
   - OUT3 → Rear Right motor
   - OUT4 → Front Left motor

Strip 3 mm of insulation from each bell wire end, tin with solder, then press onto the pad and heat. Apply heat shrink over each joint immediately after soldering. If any motor spins in the wrong direction during testing, swap any two wires on that motor's ESC output — you do not need to desolder; simply pull two wires free and cross them.

**Step 9 — Solder battery leads to PDB.** Strip 5 mm from each end of the XT60 connector leads. Solder the red (positive) lead to the BAT+ pad and the black (negative) lead to the BAT- pad on the PDB. These pads handle up to 50A continuous — use generous solder for a solid mechanical connection. Cover both joints with heat shrink rated for at least 200°C.

### Phase 4: Flight Controller Peripherals

**Step 10 — Install ELRS Nano receiver.** Mount the ExpressLRS Nano 915 MHz receiver on the top plate using double-sided foam tape. Position it near a rear corner of the top plate, away from the VTX antenna. Solder three wires to the receiver's FC-side pins:
   - RX pin → USART3_TX on FC (22AWG)
   - +5V pin → 5V pad on FC (22AWG)
   - GND pin → GND pad on FC (22AWG)

Screw the included SMA antenna onto the receiver's RP-SMA port hand-tight, then give a gentle quarter-turn with finger pressure — do not use tools on the SMA thread. Route the three signal wires along the edge of the top plate and secure with velcro ties.

**Step 11 — Install AKK Race Ranger VTX.** Mount the VTX on the top plate near the front or side, as far from the ELRS receiver antenna as possible. Connect:
   - SmartAudio pin → SmartAudio pad on FC (22AWG)
   - Power (+) → PDB 5V or 9V pad (18AWG recommended for VTX current draw)
   - Ground (-) → GND pad (22AWG)

Screw the FPV antenna onto the VTX's SMA port. The AKK Race Ranger outputs up to 1.6W — ensure your antenna is rated for this power level. Route the video cable from the camera to the VTX video input (if using a standalone VTX with video passthrough; the AKK Race Ranger typically connects directly to the camera output).

**Step 12 — Install Caddx Ratel 2 camera.** Mount the camera on the front of the frame facing forward. The Caddx Ratel 2 uses a standard FPV camera mount pattern. Connect:
   - Video out → FC VIDEO_IN pin (use shielded cable, 22AWG)
   - Power (+) → PDB 5V pad (22AWG)
   - Ground (-) → GND pad (22AWG)

Route the video cable along the top plate edge toward the VTX. If the camera has adjustable focus, set it now: power the battery, view the feed through your goggles, and adjust the focus ring until the image is sharp at flying distance.

**Step 13 — Install Beitian BN-220 GPS module
