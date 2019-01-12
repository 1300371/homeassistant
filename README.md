# Home Assistant Guidelines

# Hardware 
- Raspberry Pi 3B+
- External HDD
- ESP82XX-base chipset
- FTDI _Serial-to-USB_ (required to flash ESP8266)

# Install Raspbian on Pi
To preserve the SD card, use an external HDD.  
Need to have a hard drive with a dedicated power supply or that spins up disks before the Pi boot sequence (see https://www.raspberrypi.org/blog/pi-3-booting-part-i-usb-mass-storage-boot/).

## Prepare HDD Drive
- Download image: https://www.raspberrypi.org/downloads/
- Write image to HDD with Etcher: https://www.balena.io/etcher/
- Update `config.txt` if needed: https://www.raspberrypi.org/documentation/configuration/config-txt/
- Add `wpa_supplicant.conf` and `ssh` if needed: https://www.raspberrypi.org/documentation/configuration/wireless/headless.md

### File `wpa_supplicant.conf`
Create a file `wpa_supplicant.conf` in the `/boot` directory.
```
network={
    ssid="wifi ssid"
    psk="wifi password"
}
```
https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md

### File `ssh`
Create an empty file `ssh` in the `/boot` directory.  
https://www.raspberrypi.org/documentation/remote-access/ssh/README.md#3-enable-ssh-on-a-headless-raspberry-pi-add-file-to-sd-card-on-another-machine

## Boot the Pi

Do not need a SD card, the _3B+_ will boot automatically on HDD.

## Setup the Pi
Setup the raspberry (hostname, timezone, ...)
> sudo raspi-config

## Upgrade the Pi
> sudo apt-get update  
> sudo apt-get upgrade

# Install Docker 
With the great install script:
> curl -fsSL https://get.docker.com | sudo bash

# Install hass.io
https://github.com/home-assistant/hassio-build/tree/master/install#install-hassio  

Before install, need to install required dependencies.
> sudo apt-get install jq avahi-daemon dbus apparmor-utils network-manager

Install hass.io providing the Raspberry Pi 3 platform : `raspberrypi3`
> curl -sL https://raw.githubusercontent.com/home-assistant/hassio-build/master/install/hassio_install | sudo bash -s -- -m raspberrypi3

# Access HA
HA should be started and reachable at `http://<ip_of_raspberry>:8123`  
Hass.io should be present on the left menu.

# Go further

- [hass.io](hass.io/README.md)
- [Home Assistant](ha/README.md)
- [Node-RED](nodered/README.md)
- [Sonoff Basic](sonoff_basic/README.md)
- [Tasmota](tasmota/README.md)