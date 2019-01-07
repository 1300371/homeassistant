# Sonoff Basic

Need to be flashed with custom firmware to prevent the switch to connect the Itead cloud.

## Resources
- https://github.com/arendst/Sonoff-Tasmota
- https://www.domo-blog.fr/comment-flasher-le-firmware-du-sonoff-basic-pour-lutiliser-sur-jeedom/
- 

## Tasmota
https://github.com/arendst/Sonoff-Tasmota

### Tasmota firmware
https://github.com/arendst/Sonoff-Tasmota/releases

## ESPTool 
https://github.com/arendst/Sonoff-Tasmota/wiki/Esptool#esptool-executable-windows--linux

### Scheme
<img src="https://www.domo-blog.fr/wp-content/uploads/2018/09/sonoff-cablage-schema-commet-flash-jeedom-domotique-domoblog-domolab.jpg" alt="scheme" width="600px"/>

_Source [Domoblog](https://www.domo-blog.fr/comment-flasher-le-firmware-du-sonoff-basic-pour-lutiliser-sur-jeedom/)_

### Flash firmware
```
esptool -cp COM5 -cb 115200 -ce -v
```

### Setting up

Create a WiFi access point: 
```
SSID: indebuurt1
Password: VnsqrtnrsddbrN
`````

