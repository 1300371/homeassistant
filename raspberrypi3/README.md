# Raspberry Pi 3 (B+)

## Miscellaneous commands

### Get the CPU temperature
> /opt/vc/bin/vcgencmd measure_temp

### Get the current CPU frequency
> sudo cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_cur_freq

### Know if Pi is currently under-voltage
> cat /sys/class/leds/led1/brightness

`255` means correct voltage  
`0` means under-voltage  

### Update swap size
Edit `/etc/dphys-swapfile`:
```
$ sudo nano /etc/dphys-swapfile
```
Reload configuration:
```
$ sudo dphys-swapfile setup
want /var/swap=1000MByte, checking existing: deleting wrong size file (104857600), generating swapfile ... of 1000MBytes
```

