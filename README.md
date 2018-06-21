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
        sensitivity: 0.5
        measurement_std: 0.1
```
Configuration variables:
- **sensitivity**: (Optional, default 0.5) The sensitivity of the filter, in the range 0 - 1. A value of 0 means the filter ignores new values, whilst a value of 1 means the filter takes all new values.
- **measurement_std**: (Optional, default 0.1) The normalised measurement standard deviation. A sensor which is 10% inaccurate has a value of 0.1

## Simulated sensor
I am using a simulated sensor to generate the input data:
```yaml
sensor:
  - platform: simulated
    scan_interval: 1
    name: 'simulated relative humidity'
    unit: '%'
    period: 20
    amplitude: 25
    mean: 50
    spread: 25
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
<img src="https://github.com/robmarkcole/HASS-kalman-filter/blob/master/usage.png" width="350">
</p>
