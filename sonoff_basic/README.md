# Sonoff Basic
_Revision: Sonoff RF R2 POWER V1.0 PCB - **ESP8285** Chipset_  
Need to be flashed with custom firmware to prevent the switch to connect the Itead cloud.

## Resources
- https://github.com/arendst/Sonoff-Tasmota
- https://www.domo-blog.fr/comment-flasher-le-firmware-du-sonoff-basic-pour-lutiliser-sur-jeedom/


## Tasmota
https://github.com/arendst/Sonoff-Tasmota

### Tasmota firmware
https://github.com/arendst/Sonoff-Tasmota/releases

## ESPTool 
https://github.com/arendst/Sonoff-Tasmota/wiki/Esptool#esptool-executable-windows--linux

### Scheme
<img src="https://www.domo-blog.fr/wp-content/uploads/2018/09/sonoff-cablage-schema-commet-flash-jeedom-domotique-domoblog-domolab.jpg" alt="scheme" width="600px"/>

_Source [Domoblog](https://www.domo-blog.fr/comment-flasher-le-firmware-du-sonoff-basic-pour-lutiliser-sur-jeedom/)_

### Physical switch
https://github.com/arendst/Sonoff-Tasmota/wiki/Sonoff-Basic#new-board-layout
A physical switch can be added to the Sonoff devices.  
Can be achieved connecting GPIO2 labeled `IO2` and `GND` (requires additional soldering - _can be tricky_).

### Firmware mode
https://github.com/arendst/Sonoff-Tasmota/wiki/Esptool#put-device-in-firmware-upload-mode

_On ESP8285, the green LED don't blink in firmware mode._

### Erase firmware
Can be useful if WiFi issue.

```
esptool -cp COM5 -cb 115200 -ce -v
```
```
esptool.py --port COM5 erase_flash
```

### Flash firmware
1. Plug the FTDI (without power supply) to the Sonoff device
1. Push (and hold) the Sonoff button
1. Plug in the FTDI to the PC
1. Launch the following command (supposing you downloaded the Tasmota firmware into the same directory)  
    
    _EXE version_
    ```
    esptool.exe -cp COM5 -cb 115200 -bm dout -cf sonoff.bin -v
    ```
    _Python version_
    ```
    esptool.py --port COM5 write_flash -fs 1MB -fm dout 0x0 sonoff.bin
    ```
1. As soon as the firmware update begins, the button can be released.

```
esptool v0.4.13 - (c) 2014 Ch. Klippel <ck@atelier-klippel.de>
setting flash mode from qio to dout
opening bootloader
resetting board
trying to connect
trying to connect
Uploading 534032 bytes from sonoff.bin to flash at 0x00000000
................................................................................ [ 15% ]
................................................................................ [ 30% ]
................................................................................ [ 45% ]
................................................................................ [ 61% ]
................................................................................ [ 76% ]
................................................................................ [ 91% ]
..........................................                                       [ 100% ]
starting app without reboot
closing bootloader
 
```

### Setting up

Connect to the new WiFi AP : `sonoff-...`

1. Setup the WiFi connection to home network
1. Setup MQTT broker 

### Troubleshooting
* Sonoff don't connect to WiFi configured network
    1. After flashing, unplug FTDI from USB
    2. Plug FTDI to USB
    3. Disconnect VCC from Sonoff (3V3)
    4. Reconnect VCC
    5. Sonoff should connect to WiFi

* Display logs from Sonoff device
    1. Launch Putty
    2. Setup a serial connection
    ```
    Serial line: COM5
    Speed: 115200
    ```

### Miscellaneous
* Sonoff take 30-45 seconds to reboot and reconnect to WiFi network


### Add to HomeAssistant
`configuration.yaml`:
````yaml
switch:

  - platform: mqtt
    name: "Sonoff "
    state_topic: "stat/sonoff/POWER"
    value_template: "{{ value_json.POWER }}"
    command_topic: "cmnd/sonoff/POWER"
    payload_on: "ON"
    payload_off: "OFF"
````