# File `configuration.yaml`

## Geoposition
````yaml
homeassistant:
  # ...
  # Location required to calculate the time the sun rises and sets
  latitude: 
  longitude: 
  # Impacts weather/sunrise data (altitude above sea level in meters)
  elevation: 
  # metric for Metric, imperial for Imperial
  unit_system: metric
  # Pick yours from here: http://en.wikipedia.org/wiki/List_of_tz_database_time_zones
  time_zone: 
````
Set your position on earth if _sun_ component is used.

## Custom Panel
To add item to the left menu.
````yaml
panel_iframe:
  configurator:
    title: Configurator
    icon: mdi:wrench
    url: http://localhost:3218
````

## Activate Lovelace yaml mode
````yaml
lovelace:
  mode: yaml
````

## Define purge delay on recorder
````yaml
recorder:
  purge_keep_days: 90
````
