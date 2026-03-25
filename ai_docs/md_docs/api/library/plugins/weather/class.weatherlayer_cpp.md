# Unigine::Plugins::Weather::WeatherLayer Class (CPP)

**Header:** #include <plugins/Unigine/Weather/UnigineWeather.h>


This is a base class for weather layers. Layers comprise a vertical profile of the [weather region](../../../../api/library/plugins/weather/class.region_cpp.md). Different cloud or precipitation layers may exist at various heights. There are three types of layers available:


- **Base Layer** - layer with no visual representation, it defines weather parameters such as [visibility range](#setVisibility_float_void), [temperature](#setTemperature_float_void), [humidity](#setHumidity_float_void).
- **Cloud Layer** - layer that controls clouds within the region (via the [WeatherLayerCloud](../../../../api/library/plugins/weather/class.weatherlayercloud_cpp.md) class).
- **Precipitation Layer** - layer that controls precipitation within the region (via the [WeatherLayerPrecipitation](../../../../api/library/plugins/weather/class.weatherlayerprecipitation_cpp.md) class).


## WeatherLayer Class

### Enums

## WEATHER_LAYER_TYPE

| Name | Description |
|---|---|
| **WEATHER_LAYER_TYPE_BASE** = 0 | **Base Layer** - layer with no visual representation, it defines weather parameters such as [visibility range](#setVisibility_float_void), [temperature](#setTemperature_float_void), [humidity](#setHumidity_float_void). |
| **WEATHER_LAYER_TYPE_CLOUD** = 1 | **Cloud Layer** - layer that controls clouds within the region (via the [WeatherLayerCloud](../../../../api/library/plugins/weather/class.weatherlayercloud_cpp.md) class). |
| **WEATHER_LAYER_TYPE_PRECIPITATION** = 2 | **Precipitation Layer** - layer that controls precipitation within the region (via the [WeatherLayerPrecipitation](../../../../api/library/plugins/weather/class.weatherlayerprecipitation_cpp.md) class). |

### Members

---

## long long getID ( ) const

Returns the ID of the weather layer.
### Return value

ID of the weather layer.
## long long getRegionID ( ) const

Returns the ID of the [weather region](../../../../api/library/plugins/weather/class.region_cpp.md) to which the layer belongs.
### Return value

ID of the [weather region](../../../../api/library/plugins/weather/class.region_cpp.md) to which the layer belongs.
## WeatherLayer::WEATHER_LAYER_TYPE getLayerType ( ) const

Returns the type of the weather layer.
### Return value

Weather layer type, one of the following values:
- *Plugins::IG::WEATHER_LAYER_TYPE_BASE* - base layer.
- *Plugins::IG::WEATHER_LAYER_TYPE_CLOUD* - [cloud layer](../../../../api/library/plugins/weather/class.weatherlayercloud_cpp.md).
- *Plugins::IG::WEATHER_LAYER_TYPE_PRECIPITATION* - [precipitation layer](../../../../api/library/plugins/weather/class.weatherlayerprecipitation_cpp.md).


## void setEnabled ( bool v )

Sets a value indicating if the weather layer is enabled. The layer change callback is called.
### Arguments

- *bool* **v** - true to enable the weather layer, false - to disable it.

## bool isEnabled ( ) const

Returns a value indicating if the weather layer and the [region](../../../../api/library/plugins/weather/class.region_cpp.md) it belongs to are enabled.
### Return value

true if the layer and the [region](../../../../api/library/plugins/weather/class.region_cpp.md) it belongs to are both enabled; otherwise, false.
## bool isEnabledSelf ( ) const

Returns a value indicating if the weather layer itself is enabled. Use [isEnabled()](#isEnabled_int) to check whether the [region](../../../../api/library/plugins/weather/class.region_cpp.md) this layer belongs to is enabled as well.
### Return value

true if the layer itself is enabled; otherwise, false.
## bool isGlobal ( ) const

Returns a value indicating whether the weather layer is global (has no distinct horizontal boundaries) or not.
### Return value

true if the weather layer is global (has no distinct horizontal boundaries); false - atmospheric effects of the layer are restricted to a certain area.
## void setElevation ( double value )

Sets the base altitude for the weather layer above the sea level (distance from the sea level to the lower border of the layer).
### Arguments

- *double* **value** - New base altitude for the weather layer, in meters.

## double getElevation ( ) const

Returns the current base altitude for the weather layer above the sea level (distance from the sea level to the lower border of the layer).
### Return value

Current base altitude for the weather layer, in meters.
## void setElevationSmoothBySpeed ( double unit_per_sec )

Sets the mode of smooth gradual change of the [weather layer elevation](#setElevation_double_void) by the specified rate (in units per second). The weather layer elevation changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setElevationSmoothByTime()](#setElevationSmoothByTime_float_void)*.
### Arguments

- *double* **unit_per_sec** - Constant rate (in units per second) with which the value gradually changes from the current to target.

## void setElevationSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [weather layer elevation](#setElevation_double_void) by the specified time interval. The weather layer elevation changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setElevationSmoothBySpeed()](#setElevationSmoothBySpeed_double_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void setThickness ( double value )

Sets the thickness of the weather layer.
### Arguments

- *double* **value** - New thickness of the weather layer, in meters.

## double getThickness ( ) const

Returns the current thickness of the weather layer.
### Return value

Current thickness of the weather layer, in meters.
## void setThicknessSmoothBySpeed ( double unit_per_sec )

Sets the mode of smooth gradual change of the [weather layer thickness](#setThickness_double_void) by the specified rate (in units per second). The weather layer thickness changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setThicknessSmoothByTime()](#setThicknessSmoothByTime_float_void)*.
### Arguments

- *double* **unit_per_sec** - Constant rate (in units per second) with which the value gradually changes from the current to target.

## void setThicknessSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [weather layer thickness](#setThickness_double_void) by the specified time interval. The weather layer thickness changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setThicknessSmoothBySpeed()](#setThicknessSmoothBySpeed_double_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void setVerticalTransition ( const Math::vec2& value )

Sets new vertical sizes of transition areas at the bottom and the top of the weather layer. The effects of the layer fade out gradually within these areas downwards and upwards.
### Arguments

- *const  Math::vec2&* **value** - Vector containing new vertical sizes (widths in meters) of transition areas at the bottom and the top of the layer (*bottom_width, top_width*).

## const Math::vec2& getVerticalTransition ( ) const

Returns the vertical sizes of transition areas at the bottom and the top of the weather layer. The effects of the layer fade out gradually within these areas downwards and upwards.
### Return value

Vector containing the current vertical sizes (widths in meters) of transition areas at the bottom and the top of the layer (*bottom_width, top_width*).
## void setVerticalTransitionSmoothBySpeed ( const Math::vec2& unit_per_sec )

Sets the mode of smooth gradual change of [transition areas](#setVerticalTransition_vec2_void) at the bottom and the top of the weather layer by the specified rate (in units per second). The transition areas at the bottom and the top of the weather layer in all directions changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setVerticalTransitionSmoothByTime()](#setVerticalTransitionSmoothByTime_float_void)*.
### Arguments

- *const  Math::vec2&* **unit_per_sec** - Constant rate (in units per second) with which the value gradually changes from the current to target. Vector components specify rates for transition areas at the bottom and the top of the layer (*bottom_width, top_width*).

## void setVerticalTransitionSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the sizes of [transition areas](#setVerticalTransition_vec2_void) at the bottom and the top of the weather layer by the specified time interval. The sizes of transition areas at the bottom and the top of the weather layer change gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setVerticalTransitionSmoothBySpeed()](#setVerticalTransitionSmoothBySpeed_vec2_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void setWind ( const Math::vec3& value )

Sets the wind speed and direction for the weather layer.
### Arguments

- *const  Math::vec3&* **value** - Vector defining wind speed in all directions, in meters per second.

## const Math::vec3& getWind ( ) const

Returns the current wind speed and direction for the weather layer.
### Return value

Vector defining new wind speed in all directions, in meters per second.
## void setWindSmoothBySpeed ( const Math::vec3& unit_per_sec )

Sets the mode of smooth gradual change of the [wind speed in all directions](#setWind_vec3_void) by the specified rate (in units per second). The wind speed in all directions changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setWindSmoothByTime()](#setWindSmoothByTime_float_void)*.
### Arguments

- *const  Math::vec3&* **unit_per_sec** - Constant rate (in units per second) with which the value gradually changes from the current to target (each vector component specifies the rate for the corresponding coordinate).

## void setWindSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [wind speed in all directions](#setWind_vec3_void) by the specified time interval. The wind speed in all directions changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setWindSmoothBySpeed()](#setWindSmoothBySpeed_vec3_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void setCoverage ( float value )

Sets the cloud coverage intensity value for the weater layer.
### Arguments

- *float* **value** - Current cloud coverage intensity value for the weater layer, in the [0; 1] range (from zero to maximum cloudiness).

## float getCoverage ( ) const

Returns the current cloud coverage intensity value for the weater layer.
### Return value

Current cloud coverage intensity value for the weater layer, in the [0; 1] range (from zero to maximum cloudiness).
## void setCoverageSmoothBySpeed ( float unit_per_sec )

Sets the mode of smooth gradual change of the [cloud coverage intensity](#setCoverage_float_void) by the specified rate (in units per second). The cloud coverage intensity changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setCoverageSmoothByTime()](#setCoverageSmoothByTime_float_void)*.
### Arguments

- *float* **unit_per_sec** - Constant rate (in units per second) with which the value gradually changes from the current to target.

## void setCoverageSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [cloud coverage intensity](#setCoverage_float_void) by the specified time interval. The cloud coverage intensity changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setCoverageSmoothBySpeed()](#setCoverageSmoothBySpeed_float_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void setVisibility ( float value )

Sets the visibility range within the weather layer. Objects beyond this range are not visible inside the layer.
### Arguments

- *float* **value** - New visibility range within the weather layer, in meters.

## float getVisibility ( ) const

Returns the current visibility range within the weather layer. Objects beyond this range are not visible inside the layer.
### Return value

Visibility range within the weather layer, in meters.
## void setVisibilitySmoothBySpeed ( float unit_per_sec )

Sets the mode of smooth gradual change of the [visibility](#setVisibility_float_void) by the specified rate (in units per second). The visibility changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setVisibilitySmoothByTime()](#setVisibilitySmoothByTime_float_void)*.
### Arguments

- *float* **unit_per_sec** - Constant rate (in units per second) with which the value gradually changes from the current to target.

## void setVisibilitySmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [visibility](#setVisibility_float_void) by the specified time interval. The visibility changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setVisibilitySmoothBySpeed()](#setVisibilitySmoothBySpeed_float_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void setHumidity ( float value )

Sets the humidity value for the weather layer.
### Arguments

- *float* **value** - New humidity value for the weather layer, in %.

## float getHumidity ( ) const

Returns the current humidity value for the weather layer.
### Return value

Current humidity value for the weather layer, in %.
## void setHumiditySmoothBySpeed ( float unit_per_sec )

Sets the mode of smooth gradual change of the [humidity](#setHumidity_float_void) by the specified rate (in % per second). The humidity changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setHumiditySmoothByTime()](#setHumiditySmoothByTime_float_void)*.
### Arguments

- *float* **unit_per_sec** - Constant rate (in % per second) with which the value gradually changes from the current to target.

## void setHumiditySmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [humidity](#setHumidity_float_void) by the specified time interval. The humidity changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setHumiditySmoothBySpeed()](#setHumiditySmoothBySpeed_float_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void setTemperature ( float value )

Sets the temperature value for the weather layer.
### Arguments

- *float* **value** - New temperature value to be set, in degrees Celcius.

## float getTemperature ( ) const

Returns the current temperature value for the weather layer.
### Return value

Current temperature value, in degrees Celcius.
## void setTemperatureSmoothBySpeed ( float unit_per_sec )

Sets the mode of smooth gradual change of the [temperature](#setTemperature_float_void) by the specified rate (in degrees Celcius per second). The temperature changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setTemperatureSmoothByTime()](#setTemperatureSmoothByTime_float_void)*.
### Arguments

- *float* **unit_per_sec** - Constant rate (in degrees Celcius per second) with which the value gradually changes from the current to target.

## void setTemperatureSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [temperature](#setTemperature_float_void) by the specified time interval. The temperature changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setTemperatureSmoothBySpeed()](#setTemperatureSmoothBySpeed_float_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void setBarometric ( float value )

Sets the barometric pressure value for the weather layer.
### Arguments

- *float* **value** - New barometric pressure value to be set, in mmHg.

## float getBarometric ( ) const

Returns the current barometric pressure value for the weather layer.
### Return value

Current barometric pressure value, in mmHg.
## void setBarometricSmoothBySpeed ( float unit_per_sec )

Sets the mode of smooth gradual change of the [barometric pressure](#setBarometric_float_void) by the specified rate (in mmHg per second). The barometric pressure changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setBarometricSmoothByTime()](#setBarometricSmoothByTime_float_void)*.
### Arguments

- *float* **unit_per_sec** - Constant rate (in mmHg per second) with which the value gradually changes from the current to target.

## void setBarometricSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [barometric pressure](#setBarometric_float_void) by the specified time interval. The barometric pressure changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setBarometricSmoothBySpeed()](#setBarometricSmoothBySpeed_float_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void setLightning ( float freq )

Sets a new lightning frequency value for the weather layer. This value defines how often the lightning is observed.
### Arguments

- *float* **freq** - Lightning frequency within the [0; 1] range. By the value of 0 there'll be no lighting at all, while 1 - corresponds to maximum frequency.

## float getLightning ( ) const

Returns the current lightning frequency value for the weather layer. This value defines how often the lightning is observed.
### Return value

Lightning frequency within the [0; 1] range. By the value of 0 there is no lighting at all, while 1 - corresponds to maximum frequency.
## float getImpact ( double altitude ) const

Returns a value indicating the degree of impact of the layer at the specified altitude depending on whether it is completely inside, outside, or somewhere within the [transition area](#setVerticalTransition_vec2_void).
### Arguments

- *double* **altitude** - Altitude value to be checked.

### Return value

Value indicating the degree of impact of the layer at the specified altitude:
- 0 - completely outside the layer (and transition area)
- 1 - inside the layer
- (0 < x < 1) - within the transition area


## float getDensityGeodetic ( const Math::dvec3& geodetic_pos ) const

Returns the current density of clouds/precipitation intensity at the point specified in geodetic coordinates. This method can be used to implement a meteoradar.
### Arguments

- *const  Math::dvec3&* **geodetic_pos** - Geodetic coordinates of the point at which the density of clouds or precipitation intensity is to be obtained.

### Return value

Density of clouds for a [cloud layer](../../../../api/library/plugins/weather/class.weatherlayercloud_cpp.md) or precipitation intensity for a [precipitation layer](../../../../api/library/plugins/weather/class.weatherlayerprecipitation_cpp.md).
## float getDensityWorld ( const Math::Vec3& world_pos ) const

Returns the current density of clouds/precipitation intensity at the point specified in world coordinates. This method can be used to implement a meteoradar.
### Arguments

- *const  Math::Vec3&* **world_pos** - World coordinates of the point at which the density of clouds or precipitation intensity is to be obtained.

### Return value

Density of clouds for a [cloud layer](../../../../api/library/plugins/weather/class.weatherlayercloud_cpp.md) or precipitation intensity for a [precipitation layer](../../../../api/library/plugins/weather/class.weatherlayerprecipitation_cpp.md).
