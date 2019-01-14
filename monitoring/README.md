# Monitoring

Monitoring Raspberry Pi and Docker containers.

## Prometheus
Prometheus is an open-source systems monitoring and alerting toolkit.  
https://prometheus.io/docs/prometheus/latest/installation/#using-docker  
_ARM image_
```
carlosedp/prometheus
```

## node_exporter
Monitoring machine (_Raspberry_) metrics.
https://github.com/prometheus/node_exporter  
_ARM image_
```
Bundled in hass.io
```
_<small>See [Addons](../hass.io/README.md#addons)</small>_

## cAdvisor
Container :) that collects, aggregates, processes, and exports information about running containers.
https://github.com/google/cadvisor#quick-start-running-cadvisor-in-a-docker-container
_ARM image_
```
budry/cadvisor-arm
```

## Grafana
The open platform for beautiful analytics and monitoring.
http://docs.grafana.org/installation/docker/
_ARM image_
```
Bundled in hass.io
```
_<small>See [Addons](../hass.io/README.md#addons)</small>_