# OW GasBuddy Display and Home Assistant integration (WORK IN PROGRESS!!)


[![GitHub release](https://img.shields.io/github/v/release/sagdusmir/GasBuddy-Display-320x172?style=flat-square&logo=github&color=blue)](https://github.com/sagdusmir/GasBuddy-Display-320x172/releases/latest)
[![GitHub Release Date](https://img.shields.io/github/release-date/sagdusmir/GasBuddy-Display-320x172?style=flat-square&logo=github&color=blue)](https://github.com/sagdusmir/GasBuddy-Display-320x172/releases)
[![GitHub commit activity (branch)](https://img.shields.io/github/commit-activity/t/sagdusmir/GasBuddy-Display-320x172/main?style=flat-square&logo=github&color=blue)](https://github.com/sagdusmir/GasBuddy-Display-320x172/commits/main/)
![GitHub license](https://img.shields.io/github/license/sagdusmir/GasBuddy-Display-320x172?style=flat-square&logo=gnu&color=green)
[![Scale make](https://img.shields.io/badge/Scale-OW_GasBuddy-critical)](https://www.grillsportverein.de/forum/threads/otto-wilde-g32-smarthome.369079/page-999)
[![HA support](https://img.shields.io/badge/Home_Assistant-recommended-informational?style=flat-square&logo=home-assistant&logoColor=white&color=orange)](https://home-assistant.io)

This repository is a variation of the hardware used for https://github.com/sagdusmir/G32-Grill-Display-320x172-BT, and allows to use a OW GasBuddy without connecting it to a G32 gas grill. In case you own a 2nd or 3rd GasBuddy or your G32 broke down on you, this is for you.


Focus: **mobile, cloud-independent, G32-independent** GasBuddy display — no cloud login, no Otto Wilde servers, no G32. Gas weight is read from the scale over UART. Direct connection between GasBuddy and this device is required.

<img alt="Teaser Weight (stable)" src="https://github.com/user-attachments/assets/3c9aea37-8a9c-4735-af00-636dbedb936c" height="150">
<img alt="Teaser Weight (with estimations)" src="https://github.com/user-attachments/assets/fba590d7-4069-487e-86dd-4b6b0c9427ca" height="150">
<img alt="Teaser Info Screen" src="https://github.com/user-attachments/assets/2e43ae65-6193-4e49-8d6d-b8ed81eb401d" height="150">
<img alt="Teaser Calibration Wizard 1" src="https://github.com/user-attachments/assets/0c6052d1-c81f-4c70-a572-ac35e10ca549" height="150">
<img alt="Teaser Calibration Wizard 2" src="https://github.com/user-attachments/assets/8fd18e69-6506-4639-9411-7b2b00718376" height="150">
<img alt="Teaser Calibration Wizard 3" src="https://github.com/user-attachments/assets/f715eefd-7fc7-4a90-8829-cfd422277bed" height="150">
<img alt="Teaser Calibration Wizard 4" src="https://github.com/user-attachments/assets/69bfee5c-aaab-481d-b894-ae7fac2a446c" height="150">
<img alt="Home Assistant device page: Controls, Sensors and Diagnostic" src="https://github.com/user-attachments/assets/c1edc575-086f-45c1-95d1-62cefc462ac5" height="150">

<br>Bare device during testing.<br>

# Table of Contents

1. [Features](#features)
   - [Implemented functionality](#implemented-functionality)  
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

- **Gas level** monitoring (requires OW GasBuddy)
- **Alarms** — visual indicator and optional buzzer for gas level and battery SOC. While either value is at or below its limit, the passive buzzer repeats the alert tone every 5 seconds. It stays quiet for the first 15 seconds after boot.
- Touchscreen configuration
  - tap the topmost status bar to get to the details screen
  - from the details screen you can launch the calibration wizard (which can be aborted in the if you need to)
  - the configuration wizard if fully contional using the device stand alone (no Home Assistant required)
- Multiple **color schemes** (predefined + easy to add your own)
- **Connection & status icons** (WiFi, battery SOC, Warning)
- **Optional battery monitoring** the state of charge (SOC) of a connected battery can be displayed
- **Optional Home Assistant** connectivity that exposes most of the measurements and allows confguring some settings of the device that can not be controlled using the UI on the device itself (min SOC level, min gas bottle level, color scheme, hide SOC, hide gas bottle level, screen powersave).

See [changelog.md](changelog.md).

### Limitations
* Volume level of the optional buzzer is a bit low.

### Missing
* 3d model for case / mount
* validation of fully assembled hardware

## Hardware
### BOM

| Component                                    | Qty | Source                                   | Costs            |
|----------------------------------------------|-----|------------------------------------------|------------------|
| ESP32 Dev Board                              | 1   | Amazon, AliExpress                       |   ~15€ - 20€     |
| Connector to original GasBuddy               | 1   | Alibaba                                  |    ~2€ - arm+leg |
| Battery                                      | 1   | AliExpress                               |    ~8€ - 12€     |
| Power Switch with Reverse Voltage Protection | 1   | somewhere online                         |    ~5€ - 10€     |
| Step-Up/Step-Down Voltage Regulator          | 1   | somewhere online                         |    ~8€ - 10€     |
| USB 5V 2A Boost Converter + Charger circuit  | 1   | AliExpress                               |     ~2€ - 5€     |
| USB-C Connector                              | 1   | Amazon, eBay, AliExpress                 |       ~2€        |
| 2 pin Wire Connectors                        | n   | Amazon, eBay, AliExpress                 |       ~2€        |
| Diode                                        | 3   | eBay, somewhere online                   |       ~1€        |
| Screws	                                      | 4   | hardware store, eBay, Amazon, AliExpress |       ~1€        |
| Buzzer	                                      | 1	  | Amazon, eBay, AliExpress                 |       ~1€        |
| some wires (soft silicone wire recommended)  | n   | AliExpress, Amazon, eBay                 |       ~2€        |
| Kapton tape or electrical tape               | ?   | AliExpress, Amazon, eBay                 |       ~0€        |
| Case (WORK IN PROGRESS)                      | 1   | a friend with a 3d printer               |    a beer        |
| USB-C Connection Cable                       | 1   | your existing collection of cables       |       ~0€        |


### Component Details

* __ESP32 Dev Board__<br>
  You need a "__Waveshare ESP32-C6-Touch-LCD-1.47__". It is equipped with an ESP32-C6, WiFi, Bluetooth, a 320x172 Pixel 1.47" touchscreen, and everything you need. No additional memory card required. Attention: The non-touch version is a very different hardware.

* __Connector to original OW GasBuddy__<br>
  This is a "__LLT-M12-10004F3054__" (M12-4pin, female, UL2464 cable connector with thread lock) connector from LLT and might be hard to get. I found the manufacturer __Shenzhen Lilutong Electronic Technology Co., Ltd.__ on Alibaba. Feel free to <a href="https://www.sagdusmir.net" target="_blank"> contact me</a> in case you need one.
  <br>NOTE: I will stick to the colors used by OW. These connectors can be customised, and the the colors might not match, or can be swapped in comparison to the OW connector.
  <br><img alt="LLT M12 4pin female connector" src="https://github.com/user-attachments/assets/49f237e8-048e-4d0e-814c-4695a358cc5c" width="200">

* __Battery__
  A 3.7V LiPo/Li-Ion Battery (1 cell) will power the ESP32 Dev Board and the GasBuddy. Bigger is better and I went for 30000mAh. The GasBuddy alone consumes 145 mW of power.

* __Power Switch with Reverse Voltage Protection__<br>
  To minimize power draw, I am using a Pololu Mini Pushbutton Power Switch,Reverse Voltage Protection,LV (Pololu 2808) which should reduce power draw as much as possible. Unfortunately the module is a bit pricey.

* __Step-Up/Step-Down Voltage Regulator__<br>
  To provide power to the GasBuddy scale, I use a Pololu 5V Step-Up/Step-Down Voltage Regulator S7V8F5. This also has a shutdown input to turn power off.

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
  Schottky Diodes with a low voltage drop of 0.3-0.4V (e.g. 1N5819) to direct power flow.

* __Buzzer__<br>
  A __passive__ piezo buzzer.<br>Configured pins are GPIO5 amd GPIO6. The buzzer should be rather small (e.g. ⌀13mm x 2.5mm or similar). 

* __Case__<br>This is still a WORK IN PROGRESS
  
### Wiring and Assembly

#### Wiring

This is still a WORK IN PROGRESS

<br>
<br>Wiring when using the usb-c port for delivering power (the most basic option):
<br><img alt="wiring sketch with powering via usb-c" src="https://github.com/user-attachments/assets/e901f5aa-db8a-45a5-ae19-a759f69266a6" width="200">
<br>Wiring when using a rechargable battery:
<br><img alt="wiring sketch" src="https://github.com/user-attachments/assets/ecc2deb0-5185-4ecb-a9db-9589be89d1c9" width="200">
<br>Wiring when using a rechargable battery using the optional custom pcb:
<br><img alt="wiring sketch with optional custom shield pcb" src="https://github.com/user-attachments/assets/6bf8a9df-1d9a-4cea-9d7a-1408c1f8dcba" width="200">


#### Assembly

Upcoming, once the 3D model of the case is done.

## Uploading the software to the ESP

### Prebuilt firmware

Each [GitHub Release](https://github.com/sagdusmir/GasBuddy-Display-320x172/releases/latest) includes compiled images with placeholder Wi-Fi, OTA, and Home Assistant values. The extra `.espbinpatch` suffix is the same firmware as a `.bin` — patch those secrets, then flash. Do not flash the download as-is.

| File | When to use |
|---|---|
| `*.factory.bin.espbinpatch` | First flash on a new or empty device (erases everything) |
| `*.ota.bin.espbinpatch` | Later updates if the device already works (keeps Wi-Fi and other saved settings) |

1. Download the matching file from the latest release.
2. Use the ESP Bin Patcher link in the release notes (preconfigured) in **Chrome or Edge**.
3. Choose the downloaded file on that page.
4. Fill in the replacements (Wi-Fi SSID, Wi-Fi password, OTA password, Home Assistant API key).
   For the API key, paste your Home Assistant / ESPHome `api.encryption.key` (the Base64 value) as **New**.
5. Click **Patch firmware**, connect the board via USB, then **Install patched firmware**.
   - Factory file: choose **Erase everything**.
   - OTA file: choose **Keep saved settings**.

### Compile from source

1. Install ESPHome CLI
   ```bash
   pip install esphome
   ```
2. Clone this repository and change directory into that folder
   ```bash
   git clone https://github.com/sagdusmir/GasBuddy-Display-320x172.git && cd GasBuddy-Display-320x172
   ```
3. Connect the ESP32-C6 1.47 Inch Display Development Board via USB
4. Compile and flash the software
   ```bash
   esphome run gasbuddy-display.yaml
   ```
   You may be asked how the connection should be established.

## Troubleshooting

1. If compiling and flashing the ESP32 succeeds, but the screen is looking distorted afterwards, skimply turn the power off and on agaoin. Pressing the BOOT button in the device is not sufficient.

2. If you get A LOT of strange syntax errors, try to clean up the configured build folder via
   ```bash
   esphome clean gasbuddy-display.yaml
   ```





## Acknowledgments
This project would not have been possible without the work of the community. Special thanks go to:

[tobsch/g32-investigations](https://github.com/tobsch/g32-investigations) (additional information about BLE and serial communication)


## Disclaimer
This is third-party software developed by the community and is not officially developed or supported by Otto Wilde GmbH. Use at your own risk.

__This project is provided for educational and experimental purposes only.__


All hardware designs, schematics, code, instructions, and documentation are offered AS IS without any warranty of any kind, express or implied.
YOU BUILD AND USE THIS AT YOUR OWN RISK.
The author(s) and any contributors are not responsible for any injury, death, property damage, fire, electrical shock, data loss, voided warranties, legal violations, or any other consequences — direct, indirect, incidental, or consequential — that may result from building, modifying, or using this project or any derivative work.
Always follow local electrical/safety/building codes.


If you're not experienced with mains voltage, high current, lithium batteries, lasers, moving parts, etc., consult a qualified professional before proceeding.
Proceed only if you accept full personal responsibility.
