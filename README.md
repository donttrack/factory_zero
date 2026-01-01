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
packages:
  remote_package:
    url: https://github.com/donttrack/factory_zero
    ref: main
    refresh: 0s
    files: [ esphome/labels/.procon-labels-en.yaml, 
             esphome/.procon.base.yaml, 
             esphome/boards/board-esp32.yaml 
           ]
      ## Language Packs:
      # esphome/.procon.finder.yaml
      # esphome/labels/.procon-labels-en.yaml
      # esphome/labels/.procon-labels-nl.yaml
      #
      ## Base:
      # esphome/.procon.base.yaml
      #
      ## Boards:
      # esphome/boards/board-m5stack-atom.yaml
      #
      ## Zone 2, If you have 2 zones on the heatpump enable this:
      # esphome/.procon.zone2.yaml
      #
      ## Climate sensor, only heating (curve, room, flow) is supported at the moment with zone_1:
      # esphome/.procon.climate.yaml
      ## you need to add extra code homeassistant/automations_climate.yaml your automation.yaml in HA directory
      ##
      ## Measuring power and energy
      ## EASTRON 3ph SDM, If you have a 3phase Eastron kWh meter on the heatpump enable this:
      # esphome/.procon.sdm.yaml
      ## set parity to none on the kWh meter. Baudrate to 9600
      ## FINDER 1ph 7E 64 8 230 0210. If you have 2 of these kWh meters on the heatpump enable this:
      # esphome/.procon.finder.yaml
      ## set parity to none on the kWh meter. Baudrate to 9600
      ##

## for developing/testing, uncomment local includes and comment out remote_package part.
#packages:
#  substitutions: !include labels/.procon-labels-nl.yaml
#  device_base1:  !include .procon.base.yaml
##  device_base2:  !include boards/board-m5stack-atom.yaml
#  device_base3:  !include .procon.climate.yaml
```

# Translations
Currently supported languages are en, nl.
In order to change language, edit the line files: `esphome/procon.yaml`

## Contact
Contact me: alphonsuijtdehaag at gmail dot com, if you are interested in a PCB with a ESP32 (lilygo ESP32S3-T7) or M5stack RS485 with Atom s3 lite

[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/ebbenberg)
