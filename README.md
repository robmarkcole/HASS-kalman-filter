# HASS-kalman-filter
Home-Assistant custom component adding a 1D Kalman filter. The defaul config options should give reasonable performance. If you wish top tweak the options you should first read this reference to understand the Kalman filter concept.

Place the `custom_components` folder in your configuration directory (or add its contents to an existing `custom_components` folder).

Add to your Home-Assistant config:

```yaml
tbc
```
Configuration variables:
- **sensitivity**: (Optional, default 0.5) The sensitivity of the filter, in the range 0 - 1. A value of 0 means the filter ignores new values, whilst a value of 1 means the filter takes all new values.
- **measurement_std**: (Optional, default 0.1) The normalised measurement standard deviation. A sensor which is 10% inaccurate has a value of 0.1
