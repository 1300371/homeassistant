# Roborock Vacuum


## Get your vacuum token
<small>Requires Android SDK Tools.</small>

1. Install _Mi Home 5.0.19 APK_
1. Login and check the vacuum
1. Use `adb` to backup app (Android SDK Tool)
    > adb backup com.xiaomi.smarthome    
    
    Will produces a `backup.ab` file.
1. Download [Android Backup Extractor](files/android-backup-tookit-20180521.zip)
1. Extract android backup file to archive file
    > java -jar abe.jar unpack backup.ab backup.ab.tar
1. Unzip the archive 
1. Open the SQLite file `apps/com.xiaomi.smarthome/db/miio2.db`
1. The _token_ is in the  `device_record`.`token` field

## HA configuration

````yaml
vacuum:
  - platform: xiaomi_miio
    host: 192.168.0.ip
    token: !secret roborock_token
````
Now, the vacuum can be requested by HA.


## Custom setting
Add a input select for zone cleaning.
````yaml
input_select:
  vacuum_room:
    name: Choose a room 
    options:
      - ...
      - Kitchen
      - Dining Room
    initial: ...
    icon: mdi:robot-vacuum
````

This entity can be added to the UI as a combo.  

Have to get somehow the map coordinates : https://community.home-assistant.io/t/howto-xiaomi-vacuum-zoned-cleaning/51293  

... and call HA service: `vacuum.send_command`
````json
{
  "entity_id": "vacuum.xiaomi",
  "command": "app_zoned_clean",
  "params": [[x1,y1,x2,y2,c], ...]
}
````
- `[x1,y1]` the bottom left corner
- `[x2,y2]` the top right corner
- `c` the number of pass
- can add multiple areas with the array

... and all of that can be automated of course: thanks to [NodeRED](../nodered/README.md) !

