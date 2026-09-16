# G32 Connected Grill Monitor and Display MINI


[![GitHub release](https://img.shields.io/github/v/release/sagdusmir/G32-Grill-Display-320x172-BT?style=flat-square&logo=github&color=blue)](https://github.com/sagdusmir/G32-Grill-Display-320x172-BT/releases/latest)
[![GitHub Release Date](https://img.shields.io/github/release-date/sagdusmir/G32-Grill-Display-320x172-BT?style=flat-square&logo=github&color=blue)](https://github.com/sagdusmir/G32-Grill-Display-320x172-BT/releases)
[![GitHub commit activity (branch)](https://img.shields.io/github/commit-activity/t/sagdusmir/G32-Grill-Display-320x172-BT/main?style=flat-square&logo=github&color=blue)](https://github.com/sagdusmir/G32-Grill-Display-320x172-BT/commits/main/)
![GitHub license](https://img.shields.io/github/license/sagdusmir/G32-Grill-Display-320x172-BT?style=flat-square&logo=gnu&color=green)
[![Grill make](https://img.shields.io/badge/grill-OW_G32_Connected-critical)](https://www.grillsportverein.de/forum/threads/otto-wilde-g32-smarthome.369079/page-999)
[![HA support](https://img.shields.io/badge/Home_Assistant-recommended-informational?style=flat-square&logo=home-assistant&logoColor=white&color=orange)](https://home-assistant.io)

This repository is a stripped down version of https://github.com/sagdusmir/G32-Grill-Display-480x320-BTpref , but offers a better experience regarding power management.


Focus: **mobile, cloud-independent replacement** for the official Otto Wilde app / Grill Buddy — no cloud login, no Otto Wilde servers. Direct BLE connection to the grill (tested with firmware **v1.4.5**; older "v13" not compatible).

<img alt="Teaser Gauges" src="https://github.com/user-attachments/assets/7477aff2-aa70-4a29-8a00-d886d874ef73" height="150">
<img alt="Teaser Temperature Alarm" src="https://github.com/user-attachments/assets/cb68fa71-7baf-4253-ba44-360a564703f2" height="150" />
<img alt="Teaser Info Page" src="https://github.com/user-attachments/assets/b5609668-ac7d-4246-a799-ebf88fbedc3b" height="150">


Bare device during testing.<br>

# Table of Contents

1. [Features](#features)
   - [Implemented functionality](#implemented-functionality)  
   - [What is missing?](#what-is-missing)
   - [Limitations](#limitations)
3. [Hardware](#hardware)
   - [BOM](#bom)
   - [Component Details](#component-details)
   - [Wiring and Assembly](#wiring-and-assembly)
      - [Wiring](#wiring)
      - [Assembly](#assembly)
4. [Uploading the software to the ESP](#uploading-the-software-to-the-esp)
5. [Troubleshooting](#troubleshooting)
6. [Acknowledgments](#acknowledgments)
7. [Disclaimer](#disclaimer)

## Features

### Implemented functionality

- **Automatic detection** of a near by G32 Connected
- Real-time temperatures for up to **4 grill zones** + **4 external probes**
- **Gas level** monitoring (if GasBuddy is installed)
- **Alarms** — visual indicator + optional buzzer for temperature limits and other alarms
- Touchscreen configuration
  - tap gauges to configure a temperature alarm (if the feature has not been disabled)
  - tap the rightmost status bar to see some other details
- Multiple **color schemes** (predefined + easy to add your own)
- **Connection & status icons** (BLE, WiFi, battery SOC)
- **Optional battery monitoring** the state of charge (SOC) of a connected battery can be displayed
- **Optional MEATER® integration** with **automatic detection** shows tip temperatures & battery SOC instead of G32 probes when connected. There is an alert if temperature specs are exceeded.
- **Optional Home Assistant** connectivity that exposes most of the measurements and allows confguring some settings of the device that can not be controlled using the UI on the device itself (min SOC level, min gas bottle level, color scheme, hide SOC, hide gas bottle level). At the moment HA will list about 38 entities for this device.

See [changelog.md](changelog.md).

### What is missing?
* **Meater 2 plus (aka PRO) support:** Meater 2 plus units are currently not supported
* **Gas Buddy:** calibration of a new gas bottle
* **G32 light:** setting the brightness level for turning on the light in the lid

### Limitations
* Everything that was mentioned above under [What is missing?](#what-is-missing)
* Volume level of the optional buzzer is a bit low.
* Meater probes can only connect to a single device at a time. However, this does not prevent using a Meater Block.


## Hardware
### BOM

| Component                                    | Qty | Source                                   | Costs        |
|----------------------------------------------|-----|------------------------------------------|--------------|
| ESP32 Dev Board                              | 1   | Amazon, AliExpress                       |   ~15€ - 20€ |
| Battery                                      | 1   | AliExpress                               |    ~8€ - 12€ |
| Power Switch with Reverse Voltage Protection | 1   | somewhere online                         |    ~5€ - 10€ |
| USB 5V 2A Boost Converter + Charger circuit  | 1   | AliExpress                               |     ~2€ - 5€ |
| USB-C Connector                              | 1   | Amazon, eBay, AliExpress                 |       ~2€    |
| 2 pin Wire Connectors                        | n   | Amazon, eBay, AliExpress                 |       ~2€    |
| Diode                                        | 1   | eBay, somewhere online                   |       ~1€    |
| Screws	                                      | 4	  | hardware store, eBay, Amazon, AliExpress |       ~1€    |
| Buzzer	                                      | 1	  | Amazon, eBay, AliExpress                 |       ~1€    |
| some wires (soft silicone wire recommended)  | n   | AliExpress, Amazon, eBay                 |       ~2€    |
| Kapton tape or electrical tape               | ?   | AliExpress, Amazon, eBay                 |       ~0€    |
| Case                                         | 1   | a friend with a 3d printer               |    a beer    |
| USB-C Connection Cable                       | 1   | your existing collection of cables       |       ~0€    |


### Component Details

* __ESP32 Dev Board__<br>
  You need a "__Waveshare ESP32-C6-Touch-LCD-1.47__". It is equipped with an ESP32-C6, WiFi, Bluetooth, a 320x172 Pixel 1.47" touchscreen, and everything you need. No additional memory card required.


* __Battery__
  A 3.7V LiPo/Li-Ion Battery (1 cell) will power the ESP32 Dev Board. Because of space constraints I am going with a battery of type 702080  (7mm x 20mm x 80mm) with a capacity of 1500mAh.

* __Power Switch with Reverse Voltage Protection__<br>
  To minimize power draw, I am using a Pololu Mini Pushbutton Power Switch,Reverse Voltage Protection,LV (Pololu 2808) which should reduce power draw as much as possible. Unfortunately the module is a bit pricey.

* __5V 2A Boost Converter + Charger circuit__<br>
  I recommend using a cheap board that has an auto power-save feature. The one that I ultimately decided on goes under the name "Type-C USB 5V 2A Boost Converter Step-Up Power Module Lithium Battery Charging Protection Board LED Display USB Charger". The boost portion is actually not used because I wanted to keep it simple and have the SOC measurement working without adding another voltage divider for the voltage at the battery.
  Arduino PowerBoost 500C / 1000C modules seem to __NOT__ offer an automatic power-save feature, so this would completely drain the battery in a few days.
  <br><img alt="charger module" src="https://github.com/user-attachments/assets/db2495e7-48c3-438e-8649-f1bb896ee21a" width="200">


* __USB-C Connector__<br>
  To power the charger circuit it is very helpful to have a male USB-C plug breakout board to supply power. The solder pads / USB port on the backside of my pcb were only used for power output and I found no accessible pads to provide power directly to the charger circuit.
  <br><img alt="usb-c plug breakout board" src="https://github.com/user-attachments/assets/3e43f463-0009-4022-a160-d33692dad432" width="200">

* __2 pin Wire Connectors__<br>
  I used a few micro JST1.25 2pin connectors (male + female) to keep things modular. At least the battery should be easy do disconnect so you do not have to solder the wires while it is connected.

* __Diode__<br>
  A Schottky Diode with a low voltage drop of 0.3-0.4V (e.g. 1N5819) to separate the charging power path a bit from the rest because the documentation of most charge controllers will not be that detailed.

* __Buzzer__<br>
  A __passive__ piezo buzzer.<br>Configured pins are GPIO5 amd GPIO6. The buzzer should be rather small to fit inside tha case (e.g. ⌀13mm x 2.5mm or similar). The smaller the buzzer, the easier it is to mount the ESP32 Dev-Board in the enclosure. Even a "Universal Passive Buzzer 12085" (12mm x 8.5mm) will fit if you keep wires short.

* __Case__<br>
  There is a 3D model of a case in the `misc` folder. Using the case.m3f file is the easiest. If that does not work for you, you can give the two .stl files a try. I placed the main case with the bottom flat on the print bed. Enabled raft and manually added tree support from the bed to the underside of the power button, to the top of the usb-port cutout and in a straight vertical line in the middle of the back of the case so it does not tip over while printing. For the battery cover I placed the short straight edge on the build plate and manually added tree support to each untgerside of the clips and in a straight vertical line in the middle of the back to add some stability. I included some images in the repository that show where I painted support structures. __NOTE__: Do not try to operate the button before installing the Pololu. You will probably snap it if there is nothing to limit its way of travel.
  <br><img alt="Teaser Testing Case Design Render" src="https://github.com/user-attachments/assets/e653098a-848d-4d84-96ad-7d0f5163ddc0" height="175">

### Wiring and Assembly

#### Wiring
Important:<br>
the Pololu push button will point to the outside of the case, so make sure to have the wires on the opposite side pointing
towards the other comonents.
Space is limited, so connect the USB-C breakout board to the charger as shown in the wiring draft and solder wires from the
top of the pcb horizontally to the right (for both: charger module and USB-C breakout board). If they point in any other direction, you will struggle to stuff everything into the case. 

- connect Pololu VOUT and GND to ESP32 BAT and GND
- connect Pololu VIN and GND in parallel with the battery to the battery pads of the charger module
- connect ESP32 VBUS and GND to the power input of the charger module with the Schottky diode as shown

The Pololu can be *carefully* slot into place (tight fit) with the wires pointing to the inside. The charger module with the installed USB plug should fit right inside the case (same orientation as in the wiring sketch). Place the piezo buzzer
on top and install the ESP32 Dev Board to close everything up. Use a bit of Kapton tape if exposed contacts might touch each other.
<br><img alt="wiring draft" src="https://github.com/user-attachments/assets/c269ee88-f03d-49cb-88c6-762994f9323e" width="200">

#### Assembly
- drop the battery into place so the connector sticks out the display casing<br>
  <img alt="assembly_1_install_the_battery" src="https://github.com/user-attachments/assets/f43e1ec5-d3b2-4285-81db-02590712703c" height="175">

- component wiring overview for orientation<br>
  <img alt="assembly_2_wiring_overview" src="https://github.com/user-attachments/assets/f0d8183d-8fa4-4e52-bfec-3b7fd0f4cf96" height="175">

- install the power switch by sliding it all the way down between the mounting posts (tight fit, and the top is intended to stick out a bit)<br>
  <img alt="assembly_3_slide_pololu_down_the_case" src="https://github.com/user-attachments/assets/b486c4b0-cdd1-49fb-b5d4-5a63f61441a7" height="175">

- install the charger board with the USB-C breakout borad plugged in and push it down to make room for the buzzer and the wiring<br>
  <img alt="assembly_4_orientation_of_the_charger_board" src="https://github.com/user-attachments/assets/841de468-23a7-4f09-b329-ced60c68de37" height="175">
  <img alt="assembly_5_push_charger_board_down_so_there_is_place_for_the_buzzer_on_top" src="https://github.com/user-attachments/assets/5a39e3c0-c1a1-4d8f-835f-80496ff6fb09" height="175">

- put the buzzer on top of the charger board and install the display (do not pinch the wires or trap any of them between the display and the mounting posts)<br>
  <img alt="assembly_6_install_display_without_trapping_wires_below_the_mounting_posts" src="https://github.com/user-attachments/assets/3c0600a7-1d33-40e4-8706-9ef785acba9a" height="175">
  <img alt="Teaser Testing Case Design" src="https://github.com/user-attachments/assets/7748155b-8b2b-4c14-a970-0c6f3c926dd1" height="175">
  <img alt="impression" src="https://github.com/user-attachments/assets/a1ae70d3-7fb6-4171-a393-d219c019fa72" height="175">
  <img alt="impression" src="https://github.com/user-attachments/assets/66e71921-71ec-4c2d-8378-c14c80f37fdd" height="175">
  <img alt="impression" src="https://github.com/user-attachments/assets/fc15aabd-d76b-46d3-9666-4b7a5720aba8" height="175">
  <img alt="comparison" src="https://github.com/user-attachments/assets/809fd282-7746-416c-8c64-a635fd3c5cf7" height="175">
  <img alt="alternative case design idea" src="https://github.com/user-attachments/assets/e1d44edf-de7c-4f18-817d-e06a43dc1bf2" height="175">


## Uploading the software to the ESP

1. Install ESPHome CLI
   ```bash
   pip install esphome
   ```
2. Clone this repository and change directory into that folder
   ```bash
   git clone https://github.com/sagdusmir/G32-Grill-Display-320x172-BT.git && cd G32-Grill-Display-320x172-BT
   ```
3. Connect the ESP32-C6 1.47 Inch Display Development Board via USB
4. Compile and flash the software
   ```bash
   esphome run g32-display-mini.yaml
   ```
   You may be asked how the connection should be established.
5. You might need to reset the device after flashing to get the display to work (push the RST button).

## Troubleshooting

1. Starting with esphome 2026.4.0 the display driver had to be changed and the output on the display might look garbled at first. Disconnecting and reconnecting power should fix this issue.
   
2. During validation of the yaml file, you might see something like `[max_connections] is an invalid option for [esp32_ble]`. The "max_connections" option has been moved from "esp32_ble_tracker:" to "esp32_ble:". Both variants are included in the YAML and you need to switch to the other variant by adding / removing a comment (#). Do not mess up the indentation. This is caused by a breaking change in esphome.

3. If compiling and flashing the ESP32 succeeds, but the screen is looking distorted (the left portion is partially readable while the right portion shows mostly pixel noise"), simply look at the "dimensions" in the "display" section and swap the values for "width:" and "height:". This is caused by a breaking change in esphome.

4. If you get A LOT of strange syntax errors, try to clean up the configured build folder via
   ```bash
   esphome clean g32-display-mini.yaml
   ```





## Acknowledgments
This project would not have been possible without the work of the community. Special thanks go to:

[Esaracci](https://community.home-assistant.io/u/esaracci/) (using this hardware with esphome)

[Pulpyy](https://community.home-assistant.io/u/pulpyy) (using this hardware with esphome)

[JBecker32/G32-Display-480x320-BT](https://github.com/JBecker32/G32-Display-480x320-BT) (the original software project)

[fschwarz86/g32](https://github.com/fschwarz86/g32)

[ralmoe/g32-docker-client](https://github.com/ralmoe/g32-docker-client)

[MortenVinding/MEATER.yaml](https://gist.github.com/MortenVinding/a513c0094d0df41a4425612257b3cabc) (Meater® accuracy)


## Disclaimer
This is third-party software developed by the community and is not officially developed or supported by Otto Wilde GmbH. Use at your own risk.

__This project is provided for educational and experimental purposes only.__


All hardware designs, schematics, code, instructions, and documentation are offered AS IS without any warranty of any kind, express or implied.
YOU BUILD AND USE THIS AT YOUR OWN RISK.
The author(s) and any contributors are not responsible for any injury, death, property damage, fire, electrical shock, data loss, voided warranties, legal violations, or any other consequences — direct, indirect, incidental, or consequential — that may result from building, modifying, or using this project or any derivative work.
Always follow local electrical/safety/building codes.


If you're not experienced with mains voltage, high current, lithium batteries, lasers, moving parts, etc., consult a qualified professional before proceeding.
Proceed only if you accept full personal responsibility.
