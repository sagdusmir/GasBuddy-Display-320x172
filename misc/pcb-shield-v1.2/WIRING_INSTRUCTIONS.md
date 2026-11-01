Here's the complete wire list, checked against the v1.2 board.

**Scale (J4, labeled SCALE)**
- Red wire to pad 1 (5V)
- Black wire to pad 2 (GND)
- White wire (scale RX) to pad 3
- Yellow wire (scale TX) to pad 4

The 1k resistors are already on the board, so nothing goes in between.

**USB-C charger input (J5, labeled CHG_IN)**
- Charger IN+ to pad 1 (it's fed from VBUS through D1 on the board)
- Charger IN− to pad 2 (GND)

**Pololu switch output (J6, labeled PSW)**
- Pololu VOUT to pad 1 (VBAT)
- Pololu GND to pad 2

**Off-board wiring, module to module**
- Battery + to charger BAT+
- Battery − to charger BAT−
- Charger BAT+ to Pololu VIN
- Charger BAT− to Pololu GND

**Headers to the ESP32 (just plug in, no wires)**
- J1 covers VBUS, GND, TXD, RXD, GPIO4, GPIO5 and GPIO6.
- J2 is the single VBAT pin.

The buzzer, D1–D3, R1/R2 and the S7V8F5 are soldered directly onto the shield. So that's 8 wires to the shield, plus the 4 short connections between battery, charger and Pololu.