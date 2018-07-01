# HASS-kalman-filter
Home-Assistant custom component adding a 1D Kalman filter. The defaul config options should give reasonable performance. If you wish top tweak the options you should first read this reference to understand the Kalman filter concept.

Place the `custom_components` folder in your configuration directory (or add its contents to an existing `custom_components` folder).

Add to your Home-Assistant config:

```yaml
sensor:
  - platform: filter
    name: "kalman filtered humidity"
    entity_id: sensor.simulated_relative_humidity
    filters:
      - filter: kalman
        sensitivity: 0.8
```
Configuration variables:
- **sensitivity**: (Optional, default 0.8) The sensitivity of the filter, in the range 0 - 1, with 0 being low sensitivity, and 1 being high sensitivity.

## Simulated sensor
I am using a simulated sensor to generate the input data:
```yaml
sensor:
  - platform: simulated
    scan_interval: 1
    name: 'simulated relative humidity'
    unit: '%'
    period: 20
    amplitude: 0
    mean: 50
    spread: 5
    seed: 999
```

I display the raw and filtered readings using a graph:
```yaml
history_graph:
  humidity:
    entities:
      - sensor.simulated_relative_humidity
      - sensor.kalman_filtered_humidity
```

<p align="center">
<img src="https://github.com/robmarkcole/HASS-kalman-filter/blob/master/usage.png" width="500">
</p>
