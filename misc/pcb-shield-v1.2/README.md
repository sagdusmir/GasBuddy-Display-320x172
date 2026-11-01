# ESP32-C6 Scale Shield v1.2 (2026-11-01)

A 2-layer, 1.6 mm through-hole shield for the Waveshare **ESP32-C6-Touch-LCD-1.47**. It is based on v1.1, which has the on-board Pololu S7V8F5.

## Changes vs v1.1
1. **Header pads only for the ESP32 pins that are used.** Each pad stays at its exact original position (17.78 mm between the rows, 2.54 mm pitch, first pin 12.60 mm from the USB edge).
   - J1 (the VBUS row on the dev board's silkscreen): VBUS, GND, TXD, RXD, GPIO4, GPIO5, GPIO6 (pins 1-4 and 9-11).
   - J2 (the VBAT row): **VBAT only** (pin 1). One GND on J1 is enough electrically, so the extra GND pads are gone.
   - Removed: RST, IO1-3, 3V3, SCL, SDA, IO13, IO12, IO9, IO8, IO7 and both J2 GNDs.
2. **All four M2 mounting holes removed.** Each corner now has a **concave notch** of R2.5 mm around the dev board's post/hole centres, so the shield clears the case posts or standoffs under the dev board's mounting holes. The hole centres are 3.77 mm from the long edges and 2.75 mm from the short edges.
   - R2.5 clears a standoff up to about 5 mm across.
   - A larger notch would cut into the J1 GPIO6 pad, which sits 0.42 mm from the notch edge.
3. **Layout**
   - SCALE, CHG_IN and PSW pads moved to a column on the left edge, in the space freed from J2. They are **no longer under the S7V8F5**.
   - Labels are 0.8 mm text on both sides.
   - D1-D3 and R1/R2 moved 1.2 mm right.
   - GND pour on both layers.
   - Re-routed with no vias.
4. Silkscreen version is v1.2.

## Files
- `esp32c6-scale-shield-v1.2.kicad_pro / .kicad_pcb`: the KiCad 9 project. The netlist is in `tools/gen.py`.
- `gerbers.zip`: Gerbers and Excellon drill files (PTH; there are no NPTH holes now), ready for JLCPCB.
- `renders/top.png`, `renders/bottom.png`: 3D renders.
- `drc-report.txt`: **0 violations, 0 unconnected**.
- `tools/`: the generator (`gen.py`), the freerouting DSN/SES files, `ses_import.py`, and the Pololu dimension photo.

## Mounting
The shield sits **under** the dev board, display up. Viewed from the shield top with the USB edge up, J1 (VBUS) is on the right and J2 (VBAT) is on the left.
- Use female/stacking headers: a 1x4 and a 1x3 on J1, and a 1x1 on J2 (or a full 1x11 strip that only touches the populated holes).
- U1, the S7V8F5, is mounted piggyback on a 1x4 header near the USB end.
- Height: the buzzer is about 8 mm and the module stack about 6 mm, so the headers between the shield and the dev board need to be at least about 8-11 mm tall.

## Pin map
| Shield pad | ESP32 pin | Net / use |
|---|---|---|
| J1-1 | VBUS | D1, D2 anodes |
| J1-2 | GND | GND |
| J1-3 | TXD (GPIO16) | R2 to SCALE RX |
| J1-4 | RXD (GPIO17) | R1 to SCALE TX |
| J1-9 | GPIO4 | U1 SHDN (EN) |
| J1-10 | GPIO5 | BZ1 + |
| J1-11 | GPIO6 | BZ1 - |
| J2-1 | VBAT | PSW OUT, D3 anode |

## External pads (left column, 1.0 mm hole, 1.8 mm pad)
- **SCALE**: 5V (5V_SCALE), GND, RX (from ESP TXD through R2), TX (to ESP RXD through R1)
- **CHG_IN**: + (D1 cathode), - (GND)
- **PSW** (Pololu power switch): OUT (= VBAT), GND

## Circuit
- D1 1N5819: VBUS to CHG_IN+
- D2: VBUS to 5V_IN; D3: VBAT to 5V_IN
- U1 S7V8F5: VIN = 5V_IN, VOUT = 5V_SCALE, SHDN = GPIO4, GND
- R1 1k: RXD to SCALE_TX; R2 1k: TXD to SCALE_RX
- BZ1 piezo between GPIO5 and GPIO6

## BOM
| Ref | Qty | Part |
|---|---|---|
| D1-D3 | 3 | 1N5819, DO-41 |
| R1, R2 | 2 | 1 kOhm, axial 0207 |
| BZ1 | 1 | Passive piezo, 12 mm, 7.6 mm pin pitch |
| U1 | 1 | Pololu S7V8F5 (#2123) + 1x4 straight header |
| J1/J2 | - | Female/stacking headers: 1x4 + 1x3 + 1x1 |

## Design rules
- Tracks: 0.3 mm signal and 0.8 mm power, 0.2 mm clearance.
- Copper-to-edge clearance: 0.3 mm (it was 0.5 mm; lowered because of the notches).
- Silk text: 0.7-0.8 mm on most labels; the U1 pin labels stay at 0.6 mm because of the 2.54 mm pitch.

## Caveats and sources
- GPIO4 is also the onboard TF card's chip select (SD_CS).
- GPIO5 and GPIO6 are the QMI8658 IMU interrupt lines (INT1/INT2).
- Sources:
  - Waveshare wiki and official DXF: https://www.waveshare.com/wiki/ESP32-C6-Touch-LCD-1.47 and `ESP32-C6-Touch-LCD-1.47-2D3D.zip`
  - Pololu S7V8F5: https://www.pololu.com/product/2123
