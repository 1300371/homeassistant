# File `configuration.yaml`

## Geoposition
Set position on earth if [sun](https://www.home-assistant.io/components/sun/) component is used.
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

## Custom Panel
To add item to the left menu.
````yaml
panel_iframe:
  configurator:
    title: Configurator
    icon: mdi:wrench
    url: http://localhost:3218
````

## Use secrets
<small>https://www.home-assistant.io/docs/configuration/secrets/</small>  

`configuration.yaml`
```yaml
api_password: !secret my_api_password
```
`secrets.yaml`
````yaml
my_api_password: abcd6547
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

## Switch theme on sun events
Configure themes : https://www.home-assistant.io/components/frontend/  

Then automation can be done using _service_ `frontend.set_theme` via [NodeRED](../nodered/README.md)
