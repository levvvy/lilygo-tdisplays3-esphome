# LILYGO® T-Display-S3 ST7789 ESPHome
This repository provides an [ESPHome](https://esphome.io/) configuration for the [LILYGO® T-Display-S3](https://github.com/Xinyuan-LilyGO/T-Display-S3)
ESP32-S3 board using patched TFT_eSPI.

## Video
https://user-images.githubusercontent.com/933803/227752679-9e2bbd61-53a5-4db2-9612-4751dc330378.mp4

## Pin schema
<center>
  <img src="https://user-images.githubusercontent.com/933803/227753586-71e51665-4944-4798-b52a-e430b9fb78e7.jpg" width="700px">
</center>

## Installation
You will first need to do a manual installation by putting the example.yaml file into your esphome folder then using the modern format in ESPHome to get a local copy of the firmware and finally use https://web.esphome.io/ to install over USB.

<details>
<summary>⚠ Click to expand/collapse the code block ⚠</summary>

```yaml
esphome:
  name: s3

external_components:
  - source: github://landonr/lilygo-tdisplays3-esphome
    components: [tdisplays3]

esp32:
  board: esp32-s3-devkitc-1
  variant: esp32s3
  framework:
    type: arduino

# Enable Home Assistant API
api:

ota:
  password: "6ada29f6f41ce1685d29d406efd25fa4"

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

time:
  - platform: homeassistant
    id: ha_time

switch:
  - platform: gpio
    pin: GPIO38
    name: "Backlight"
    id: backlight
    internal: true
    restore_mode: RESTORE_DEFAULT_ON

font:
  - file: "gfonts://Roboto"
    id: roboto
    size: 30

display:
  - platform: tdisplays3
    id: disp
    update_interval: 1s
    rotation: 270
    lambda: |-
      it.printf(20, 70, id(roboto), Color(255, 0, 0), id(ha_time).now().strftime("%Y-%m-%d %H:%M:%S").c_str());
</details>
```
</details>


### Method

Follow these steps to set up and flash the firmware on your LILYGO® TTGO T-Display-S3 board:

1. Download a copy of this repository and place the `tdisplays3` folder in your ESPHome folder. Also, place the `example.yaml` and `secrets.yaml` files into the ESPHome folder, making sure to change the `example.yaml` API and `secrets.yaml` details to your own credentials.
2. From your ESPHome dashboard, create a local copy of the S3 firmware by clicking the three dots > **Install** > **Manual Download** > **Modern Format**.
3. To set the board into flash mode, hold the button on the left of the USB port while plugging in the USB cable that is connected to your desktop machine.
4. Navigate to [https://web.esphome.io/](https://web.esphome.io/) in a compatible browser (Chrome, Edge, etc.) and click **Connect**. Select the corresponding COM Port and click **Connect** again.
5. When the board has connected, click **Install** and select the firmware that you have created. This will erase the board and write the new firmware.
6. When the firmware has been written to the board, you will need to unplug and reconnect the USB cable.
7. After that, you can upload firmware updates using Wi-Fi without repeating this process.


## Table of Contents

1. [Features](#features)
2. [Prerequisites](#prerequisites)
3. [Installation](#installation)
4. [Configuration](#configuration)
5. [Usage](#usage)

## Features

- [x] 🖥️ 1.54-inch ePaper display with 200x200 resolution
- [x] 🌐 Wi-Fi connectivity using ESP32-S3
- [x] 🔄 Over-The-Air (OTA) updates
- [x] 🕒 Real-Time Clock (RTC) support
- [x] 🔋 Battery level monitoring

## Prerequisites

Before you begin, make sure you have the following installed on your system:

1. [Python 3.7 or higher](https://www.python.org/downloads/)
2. [ESPHome](https://esphome.io/) (version 1.20.0 or higher)
3. [PlatformIO](https://platformio.org/) (for advanced users)
