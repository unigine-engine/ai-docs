# Unigine::Plugins::Weather::WeatherLayer Class (CS)


This is a base class for weather layers. Layers comprise a vertical profile of the [weather region](../../../../api/library/plugins/weather/class.region_cs.md). Different cloud or precipitation layers may exist at various heights. There are three types of layers available:


- **Base Layer** - layer with no visual representation, it defines weather parameters such as [visibility range](#setVisibility_float_void), [temperature](#setTemperature_float_void), [humidity](#setHumidity_float_void).
- **Cloud Layer** - layer that controls clouds within the region (via the [WeatherLayerCloud](../../../../api/library/plugins/weather/class.weatherlayercloud_cs.md) class).
- **Precipitation Layer** - layer that controls precipitation within the region (via the [WeatherLayerPrecipitation](../../../../api/library/plugins/weather/class.weatherlayerprecipitation_cs.md) class).


## WeatherLayer Class

### Enums

## WEATHER_LAYER_TYPE

| Name | Description |
|---|---|
| **BASE** = 0 | **Base Layer** - layer with no visual representation, it defines weather parameters such as [visibility range](#setVisibility_float_void), [temperature](#setTemperature_float_void), [humidity](#setHumidity_float_void). |
| **CLOUD** = 1 | **Cloud Layer** - layer that controls clouds within the region (via the [WeatherLayerCloud](../../../../api/library/plugins/weather/class.weatherlayercloud_cs.md) class). |
| **PRECIPITATION** = 2 | **Precipitation Layer** - layer that controls precipitation within the region (via the [WeatherLayerPrecipitation](../../../../api/library/plugins/weather/class.weatherlayerprecipitation_cs.md) class). |

### Properties

## float Lightning

The lightning frequency value for the weather layer. This value defines how often the lightning is observed. By the value of 0 there is no lighting at all, while 1 - corresponds to maximum frequency.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**.
## float Barometric

The barometric pressure value for the weather layer.
## float Temperature

The temperature value for the weather layer.
## float Humidity

The humidity value for the weather layer.
## float Visibility

The visibility range within the weather layer. Objects beyond this range are not visible inside the layer.
## float Coverage

The cloud coverage intensity value for the weater layer.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**.
## vec3 Wind

The wind speed and direction for the weather layer.
## vec2 VerticalTransition

The vertical sizes of transition areas at the bottom and the top of the weather layer. The effects of the layer fade out gradually within these areas downwards and upwards.
## double Thickness

The thickness of the weather layer.
## double Elevation

The base altitude for the weather layer above the sea level (distance from the sea level to the lower border of the layer).
## 🔒︎ bool IsGlobal

The value indicating whether the weather layer is global (has no distinct horizontal boundaries) or not.
## 🔒︎ bool IsEnabledSelf

The value indicating if the weather layer itself is enabled. Use [isEnabled()](#isEnabled_int) to check whether the [region](../../../../api/library/plugins/weather/class.region_cs.md) this layer belongs to is enabled as well.
## bool Enabled

The value indicating if the weather layer and the [region](../../../../api/library/plugins/weather/class.region_cs.md) it belongs to are enabled.
## 🔒︎ WeatherLayer.WEATHER_LAYER_TYPE LayerType

The type of the weather layer.
## 🔒︎ long RegionID

The ID of the [weather region](../../../../api/library/plugins/weather/class.region_cs.md) to which the layer belongs.
## 🔒︎ long ID

The ID of the weather layer.
### Members

---

## void SetElevationSmoothBySpeed ( double unit_per_sec )

Sets the mode of smooth gradual change of the [weather layer elevation](#setElevation_double_void) by the specified rate (in units per second). The weather layer elevation changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setElevationSmoothByTime()](#setElevationSmoothByTime_float_void)*.
### Arguments

- *double* **unit_per_sec** - Constant rate (in units per second) with which the value gradually changes from the current to target.

## void SetElevationSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [weather layer elevation](#setElevation_double_void) by the specified time interval. The weather layer elevation changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setElevationSmoothBySpeed()](#setElevationSmoothBySpeed_double_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void SetThicknessSmoothBySpeed ( double unit_per_sec )

Sets the mode of smooth gradual change of the [weather layer thickness](#setThickness_double_void) by the specified rate (in units per second). The weather layer thickness changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setThicknessSmoothByTime()](#setThicknessSmoothByTime_float_void)*.
### Arguments

- *double* **unit_per_sec** - Constant rate (in units per second) with which the value gradually changes from the current to target.

## void SetThicknessSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [weather layer thickness](#setThickness_double_void) by the specified time interval. The weather layer thickness changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setThicknessSmoothBySpeed()](#setThicknessSmoothBySpeed_double_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void SetVerticalTransitionSmoothBySpeed ( vec2 unit_per_sec )

Sets the mode of smooth gradual change of [transition areas](#setVerticalTransition_vec2_void) at the bottom and the top of the weather layer by the specified rate (in units per second). The transition areas at the bottom and the top of the weather layer in all directions changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setVerticalTransitionSmoothByTime()](#setVerticalTransitionSmoothByTime_float_void)*.
### Arguments

- *vec2* **unit_per_sec** - Constant rate (in units per second) with which the value gradually changes from the current to target. Vector components specify rates for transition areas at the bottom and the top of the layer (*bottom_width, top_width*).

## void SetVerticalTransitionSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the sizes of [transition areas](#setVerticalTransition_vec2_void) at the bottom and the top of the weather layer by the specified time interval. The sizes of transition areas at the bottom and the top of the weather layer change gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setVerticalTransitionSmoothBySpeed()](#setVerticalTransitionSmoothBySpeed_vec2_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void SetWindSmoothBySpeed ( vec3 unit_per_sec )

Sets the mode of smooth gradual change of the [wind speed in all directions](#setWind_vec3_void) by the specified rate (in units per second). The wind speed in all directions changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setWindSmoothByTime()](#setWindSmoothByTime_float_void)*.
### Arguments

- *vec3* **unit_per_sec** - Constant rate (in units per second) with which the value gradually changes from the current to target (each vector component specifies the rate for the corresponding coordinate).

## void SetWindSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [wind speed in all directions](#setWind_vec3_void) by the specified time interval. The wind speed in all directions changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setWindSmoothBySpeed()](#setWindSmoothBySpeed_vec3_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void SetCoverageSmoothBySpeed ( float unit_per_sec )

Sets the mode of smooth gradual change of the [cloud coverage intensity](#setCoverage_float_void) by the specified rate (in units per second). The cloud coverage intensity changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setCoverageSmoothByTime()](#setCoverageSmoothByTime_float_void)*.
### Arguments

- *float* **unit_per_sec** - Constant rate (in units per second) with which the value gradually changes from the current to target.

## void SetCoverageSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [cloud coverage intensity](#setCoverage_float_void) by the specified time interval. The cloud coverage intensity changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setCoverageSmoothBySpeed()](#setCoverageSmoothBySpeed_float_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void SetVisibilitySmoothBySpeed ( float unit_per_sec )

Sets the mode of smooth gradual change of the [visibility](#setVisibility_float_void) by the specified rate (in units per second). The visibility changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setVisibilitySmoothByTime()](#setVisibilitySmoothByTime_float_void)*.
### Arguments

- *float* **unit_per_sec** - Constant rate (in units per second) with which the value gradually changes from the current to target.

## void SetVisibilitySmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [visibility](#setVisibility_float_void) by the specified time interval. The visibility changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setVisibilitySmoothBySpeed()](#setVisibilitySmoothBySpeed_float_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void SetHumiditySmoothBySpeed ( float unit_per_sec )

Sets the mode of smooth gradual change of the [humidity](#setHumidity_float_void) by the specified rate (in % per second). The humidity changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setHumiditySmoothByTime()](#setHumiditySmoothByTime_float_void)*.
### Arguments

- *float* **unit_per_sec** - Constant rate (in % per second) with which the value gradually changes from the current to target.

## void SetHumiditySmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [humidity](#setHumidity_float_void) by the specified time interval. The humidity changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setHumiditySmoothBySpeed()](#setHumiditySmoothBySpeed_float_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void SetTemperatureSmoothBySpeed ( float unit_per_sec )

Sets the mode of smooth gradual change of the [temperature](#setTemperature_float_void) by the specified rate (in degrees Celcius per second). The temperature changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setTemperatureSmoothByTime()](#setTemperatureSmoothByTime_float_void)*.
### Arguments

- *float* **unit_per_sec** - Constant rate (in degrees Celcius per second) with which the value gradually changes from the current to target.

## void SetTemperatureSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [temperature](#setTemperature_float_void) by the specified time interval. The temperature changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setTemperatureSmoothBySpeed()](#setTemperatureSmoothBySpeed_float_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void SetBarometricSmoothBySpeed ( float unit_per_sec )

Sets the mode of smooth gradual change of the [barometric pressure](#setBarometric_float_void) by the specified rate (in mmHg per second). The barometric pressure changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setBarometricSmoothByTime()](#setBarometricSmoothByTime_float_void)*.
### Arguments

- *float* **unit_per_sec** - Constant rate (in mmHg per second) with which the value gradually changes from the current to target.

## void SetBarometricSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [barometric pressure](#setBarometric_float_void) by the specified time interval. The barometric pressure changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setBarometricSmoothBySpeed()](#setBarometricSmoothBySpeed_float_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## float GetImpact ( double altitude )

Returns a value indicating the degree of impact of the layer at the specified altitude depending on whether it is completely inside, outside, or somewhere within the [transition area](#setVerticalTransition_vec2_void).
### Arguments

- *double* **altitude** - Altitude value to be checked.

### Return value

Value indicating the degree of impact of the layer at the specified altitude:
- 0 - completely outside the layer (and transition area)
- 1 - inside the layer
- (0 < x < 1) - within the transition area
