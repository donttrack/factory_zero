Modbus RTU communication with ESP32/ESP32S3 and ttl to rs485 module, to use in home assistant / esphome for the Factory Zero Energy Module with

- Mitsubishi Procon A1M mini
- Mitsubischi Ecodan heatpump
- Brink Flair 300 WTW
- Tongdy CO2 Air quality transmitter
- ABB B23 meter

# Platforms
Currently supported ESP32 platforms.
By default ESP32 (MH-ET-LIVE) is used. If you want to use Lilygo T7-S3 ESP32S3, edit the line files: [ ]
Newer ESP configurations will be added and files updated.

```
substitutions:
  name: ecodan
  friendlyName: Ecodan heatpump
  esp_ip: "ESP Host IP"
  esp_ssid: "WiFi Network Name"
  wifi_signal_db: "WiFi Signal (dB)"
  wifi_signal_proc: "WiFi Signal (%)"
  ssid: "SSID"
  brink_speed_supply_fan: "Supply Fan Speed"
  brink_speed_exhaust_fan: "Exhaust Fan Speed"
  timezone: "Europe/Amsterdam"
  heating_room: "heating_room"
  heating_flow: "heating_flow"
  heating_curve: "heating_curve"
  cooling_room: "cooling_room"
  cooling_flow: "cooling_flow"
  floor_dryup: "floor_dryup"

esphome:
  name: ${name}
  friendly_name: ${friendlyName}

ota:
  - platform: esphome
  # password: !secret heatpump_ota_password

api:
  reboot_timeout: 0s
  # encryption:
  #   key: !secret heatpump_encryption_key

# -------------------------------------------------------------------
# Language & Board Notes
# ESP32-S3 Lite (M5stack atom s3 lite
# Uploading wrong firmware may brick the device.
# -------------------------------------------------------------------

packages:
  remote_package:
    url: https://github.com/donttrack/factory_zero
    ref: main
    refresh: 0s
    files:
      - esphome/labels/.procon-labels-en.yaml
      - esphome/.procon.base.yaml
      - esphome/boards/board-m5stack-atoms3-lite.yaml
      - esphome/confs/wifi.yaml
      - esphome/.procon.abb_b23.yaml
      # - esphome/.procon.climate.yaml
      - esphome/labels/brink-labels-nl.yaml
      - esphome/.brink.base.yaml
      - esphome/brink-300.yaml
      - esphome/.tongdy_tg9.yaml
      # - esphome/modbus_scan.yaml
      # - esphome/confs/status_led_rgb.yaml

    # -------------------------------------------------------------------
    # Optional packages (uncomment if needed)
    #
    # Language Packs:
    # - esphome/.procon.finder.yaml
    # - esphome/labels/.procon-labels-en.yaml
    # - esphome/labels/.procon-labels-nl.yaml
    #
    # Base:
    # - esphome/.procon.base.yaml
    #
    # Boards:
    # - esphome/boards/board-m5stack-atoms3-lite.yaml
    #
    # Zone 2 (dual-zone heatpump):
    # - esphome/.procon.zone2.yaml
    #
    # Climate sensor (heating only: curve, room, flow):
    # - esphome/.procon.climate.yaml
    #   Requires extra HA automation code in homeassistant/automations_climate.yaml
    #
    # -------------------------------------------------------------------

# -------------------------------------------------------------------
# Local development/testing (use instead of remote_package)
# -------------------------------------------------------------------
# packages:
#   substitutions: !include labels/.procon-labels-nl.yaml
#   device_base1:  !include .procon.base.yaml
#   # device_base2: !include boards/board-esp32.yaml
#   # device_base2: !include boards/board-esp32S3.yaml
#   # device_base2: !include boards/board-m5stack-atom.yaml
#   device_base2:  !include boards/board-m5stack-atoms3-disp.yaml
#   device_base3:  !include .procon.climate.yaml

# -------------------------------------------------------------------
# WiFi Configuration
# -------------------------------------------------------------------
# wifi:
#   ssid: !secret wifi_ssid
#   password: !secret wifi_password
#   fast_connect: on
#
#   # Static IP example:
#   # manual_ip:
#   #   static_ip: 192.168.xx.zz
#   #   gateway: 192.168.xx.1
#   #   subnet: 255.255.255.0
#
#   # For non-.local domains:
#   # domain: .local

# -------------------------------------------------------------------
# Optional API encryption key
# -------------------------------------------------------------------
# api:
#   encryption:
#     key: !secret procon_api_key

# Translations
Currently supported languages are en, nl.
