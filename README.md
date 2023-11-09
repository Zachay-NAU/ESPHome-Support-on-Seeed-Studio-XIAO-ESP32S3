# ESPHome-Support-on-Seeed-Studio-XIAO-ESP32S3
This GITHUB will walkthrough step-by-step on how to connect Seeed Studio XIAO ESP32S3 with ESPHome running on Home Assistant and send the sensor data/ control devices after connecting Grove modules to XIAO ESP32S3. So, let's get started!

## Introduction

## Install Home Assistant

Make sure you already have Home Assistant up and running. You can follow [this wiki](https://wiki.seeedstudio.com/ODYSSEY-X86-Home-Assistant) for a step-by-step guide on installing Home Assistant on an ODYSSEY-X86 SBC or this [link](https://www.mbreviews.com/how-to-home-assistant-seeed-mini-router/) for a detailed instruction use Home Assistant with a Seeed Mini Router.

## Install ESPHome on Home Assistant

ESPHome is available as a **Home Assistant Add-On** and can simply be installed via the add-on store.

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/3.png" width="700">

- **Step 1.** To quickly setup ESPHome on Home Asssistant, click the below button

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/4.png" width="300">

- **Step 2.** Once you see the following pop-up, click **OPEN LINK**

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/5.png" width="300">

- **Step 3.** Click **INSTALL**

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/6.png" width="700">

- **Step 4.** Enable all the options and click **START**

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/7.png" width="700">

- **Step 5.** Click **OPEN WEB UI** or **ESPHOME from the side-panel**

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/8.png" width="700">

You will see the following window if ESPHome is successfully loaded

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/9.png" width="700">

## Add Seeed Studio XIAO ESP32S3 (Sense) to ESPHome

- **Step 1.** Click **+ NEW DEVICE**

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/10.png" width="700">

- **Step 2.** Click CONTINUE

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/11.png" width="300">

- **Step 3.** Enter a **Name** for the device and enter WiFi credentials such as **Network name** and **Password**. Then click **NEXT**

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/12.png" width="300">

- **Step 4.** Select **ESP32-C3** and click

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/13.png" width="300">

- **Step 5.** Click **SKIP** because we will configure this board manually

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/14.png" width="300">

- **Step 6.** Click **EDIT** under the newly created board

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/15.png" width="300">

- **Step 7.** This will open a **YAML** file and this file will be used to set all the board configurations. Edit the content under **esp32** as follows

**Note:** Here we are using the latest version of [Arduino core](https://github.com/espressif/arduino-esp32/releases) for ESP32 and [ESP32 support for PlatformIO](https://github.com/platformio/platform-espressif32/releases)

- **Step 8.** Click **SAVE** and then click **INSTALL**

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/16.png" width="700">

- **Step 9.** Connect one end of a USB Type-C cable to Seeed Studio XIAO ESP32C3 and the other end to one of the USB ports on the reRouter CM4 1432
- 
<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/17.png" width="700">

```
esphome:
  name: esp32s3
  platformio_options:
    build_flags: -DBOARD_HAS_PSRAM
    board_build.arduino.memory_type: qio_opi
    board_build.f_flash: 80000000L
    board_build.flash_mode: qio 

esp32:
  board: esp32-s3-devkitc-1
  framework:
    type: arduino


# Enable logging
logger:

# Enable Home Assistant API
api:

ota:

wifi:
  ssid: "UMASS fried chicken"
  password: "Zacharyloveschicken"

  # Enable fallback hotspot (captive portal) in case wifi connection fails
ap:
  ssid: "Xiao-Esp32s3 Fallback Hotspot"
  password: "MoLTqZUvHwWI"

```

- **Step 10.** Click **Plug into the computer running ESPHome Dashboard**

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/18.png" width="300">

- **Step 11.** Select the connected port. It is likely to be ```/dev/ttyACM1 because /dev/ttyACM0``` is connected to the reRouter CM4 1432

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/19.png" width="700">

Now it will download all the necessary board packages and flash the ESPHome firmware into the XIAO ESP32C3. If the flashing is successful, you will see the following output. If you see something error, try to restart your xiao esp32c3 or enter bootloader mode by holding on the BOOT BUTTON and connect XIAO ESP32C3.

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/20.png" width="700">

- **Step 12.** The above window displays the real-time logs from the connected board. Close it by clicking **STOP**

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/21.png" width="700">

- **Step 13.** If you see the board status as **ONLINE**, that means the board is successful connected to WiFi

Now you can disconnect the XIAO ESP32C3 from the reRouter CM4 1432 and just power it via a USB cable. This is because from now on, if you want to flash firmware to the XIAO ESP32C3, you can simply do it OTA without connecting to the X86 board via a USB cable.

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/22.png" width="300">

- **Step 14.** Click the **three dots** and click **Install**

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/23.png" width="300">

- **Step 15.** Select **Wirelessly** and it will push the changes to the board wirelessly

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/24.png" width="300">

- **Step 16.** Go to **Settings** and select **Devices & Services**

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/25.png" width="700">

- **Step 17.** You will see **ESPHome** as a discovered integration. Click **CONFIGURE**

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/26.png" width="700">

- **Step 18.** Click **SUBMIT**

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/27.png" width="300">

- **Step 19.** Click **FINISH**

<img src="https://github.com/Zachay-NAU/ESPHome-Support-on-Seeed-Studio-XIAO-ESP32C3/blob/main/pictures/28.png" width="300">

## Pin Definitions



## Grove Compatibility List with ESPHome

Currently the following Grove modules are supported by ESPHome

Check [here](https://esphome.io/components/sensor/index.html#see-also)

Now we will select 6 Grove modules from the above table and explain how they can be connected with ESPHome and Home Assistant.

## Grove - Temperature and Humidity Sensor (BME680)

  ### Setup Configuration

  ### Visualize on Dashboard

## Grove -Smart Air Quality Sensor (SGP41)

  ### Setup Configuration

  ### Visualize on Dashboard

## OV2640 camera (XIAO ESP32S3 Sense)

  ### Setup Configuration

  ### Visualize on Dashboard

## PDM microphone for Voice Assistant

  ### Setup Configuration

  ### Visualize on Dashboard
















  
