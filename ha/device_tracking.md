# Device Tracking
https://www.home-assistant.io/components/device_tracker/

## Bluetooth
https://www.home-assistant.io/components/device_tracker.bluetooth_tracker/
````yaml
device_tracker:
  # Bluetooth
  - platform: bluetooth_tracker
    interval_seconds: 30
````

To improve first detection, scan Bluetooth devices with the phone while HA is restarting.  
_Sadly, you can't combine multiple MAC adresses on one device in HA. So a _[group](https://www.home-assistant.io/components/group/)_ must be created to handle multiple tracking._