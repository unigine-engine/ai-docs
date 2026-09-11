# Unigine::Plugins::Weather::Water Class (CPP)

**Header:** #include <plugins/Unigine/Weather/UnigineWeather.h>


## Water Class

### Enums

## BEAUFORT_CHANGE_TYPE

Mode of transition between the current and target Beaufort wind force levels.
| Name | Description |
|---|---|
| **BEAUFORT_CHANGE_TYPE_DISCRETE** = 0 | Beaufort wind force levels are switched discretely from current to target. |
| **BEAUFORT_CHANGE_TYPE_CONTINUOUS** = 1 | Smooth wind force transition between the current and target Beaufort levels is enabled. |

### Members

## void setWhitecap ( float whitecap )

Sets a new foam intensity for white caps on the water surface.
### Arguments

- *float* **whitecap** - The foam intensity for white caps on the water surface in the [0, 1] range.

## float getWhitecap () const

Returns the current foam intensity for white caps on the water surface.
### Return value

Current foam intensity for white caps on the water surface in the [0, 1] range.
## void setClarity ( float clarity )

Sets a new clarity of water.
### Arguments

- *float* **clarity** - The water clarity from 0 (unclear) to 1 (clear).

## float getClarity () const

Returns the current clarity of water.
### Return value

Current water clarity from 0 (unclear) to 1 (clear).
## void setBeaufort ( float beaufort )

Sets a new Beaufort wind force level from 0(Calm) to 12(Hurricane).
### Arguments

- *float* **beaufort** - The Beaufort wind force level from 0(Calm) to 12(Hurricane).

## float getBeaufort () const

Returns the current Beaufort wind force level from 0(Calm) to 12(Hurricane).
### Return value

Current Beaufort wind force level from 0(Calm) to 12(Hurricane).
## void setSeaLevel ( double level )

Sets a new height of the sea level in world coordinates.
### Arguments

- *double* **level** - The Sea level height, in meters.

## double getSeaLevel () const

Returns the current height of the sea level in world coordinates.
### Return value

Current Sea level height, in meters.
## void setBeaufortChangeType ( Water::BEAUFORT_CHANGE_TYPE type )

Sets a new type of transition between the current and target Beaufort wind force levels.
### Arguments

- *[Water::BEAUFORT_CHANGE_TYPE](../../../../api/library/plugins/weather/class.water_cpp.md#BEAUFORT_CHANGE_TYPE)* **type** - The type of transition between the current and target Beaufort wind force levels.

## Water::BEAUFORT_CHANGE_TYPE getBeaufortChangeType () const

Returns the current type of transition between the current and target Beaufort wind force levels.
### Return value

Current type of transition between the current and target Beaufort wind force levels.
## void setWaterNode ( const Ptr < ObjectWaterGlobal >& node )

Sets a new *[Water Global](../../../../api/library/objects/class.objectwaterglobal_cpp.md)* object to be used.
> **Notice:** The Water Global object is automatically found at the start of the project. Use this method only for dynamically created Water Global object.


### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ObjectWaterGlobal](../../../../api/library/objects/class.objectwaterglobal_cpp.md)>&* **node** - The *Water Global* object.

## Ptr < ObjectWaterGlobal > getWaterNode () const

Returns the current *[Water Global](../../../../api/library/objects/class.objectwaterglobal_cpp.md)* object to be used.
> **Notice:** The Water Global object is automatically found at the start of the project. Use this method only for dynamically created Water Global object.


### Return value

Current *Water Global* object.
---

## void setSeaLevelSmoothBySpeed ( double unit_per_sec )

Sets the mode of smooth gradual change of the [height of the sea level](#setSeaLevel_double_void) by the specified rate (in meters per second). The height of the sea level changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setSeaLevelSmoothByTime()](#setSeaLevelSmoothByTime_float_void)*.
### Arguments

- *double* **unit_per_sec** - Constant rate (in meters per second) with which the value gradually changes from the current to target.

## void setSeaLevelSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [height of the sea level](#setSeaLevel_double_void) by the specified time interval. The barometric pressure changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setSeaLevelSmoothBySpeed()](#setSeaLevelSmoothBySpeed_double_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void setClaritySmoothBySpeed ( float unit_per_sec )

Sets the mode of smooth gradual change of the [water clarity](#setClarity_float_void) by the specified rate (in units per second). The water clarity changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setClaritySmoothByTime()](#setClaritySmoothByTime_float_void)*.
### Arguments

- *float* **unit_per_sec** - Constant rate (in units per second) with which the value gradually changes from the current to target.

## void setClaritySmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [water clarity](#setClarity_float_void) by the specified time interval. The water clarity changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setClaritySmoothBySpeed()](#setClaritySmoothBySpeed_float_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void setBeaufortSmoothBySpeed ( float unit_per_sec )

Sets the mode of smooth gradual change of the [Beaufort wind force level](#setBeaufort_float_void) by the specified rate (in levels per second). The Beaufort wind force level changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setBeaufortSmoothByTime()](#setBeaufortSmoothByTime_float_void)*.
### Arguments

- *float* **unit_per_sec** - Constant rate (in levels per second) with which the value gradually changes from the current to target.

## void setBeaufortSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [Beaufort wind force level](#setBeaufort_float_void) by the specified time interval. The water Beaufort wind force level changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setBeaufortSmoothBySpeed()](#setBeaufortSmoothBySpeed_float_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void setWindDirection ( float direction )

Sets a new wind direction angle relative to North.
### Arguments

- *float* **direction** - Wind direction angle relative to North, in degrees.

## float getWindDirection ( ) const

Returns the current wind direction angle relative to North.
### Return value

Current wind direction angle relative to North, in degrees.
## void setWhitecapSmoothBySpeed ( float unit_per_sec )

Sets the mode of smooth gradual change of the [foam intensity for white caps on the water surface](#setWhitecap_float_void) by the specified rate (in units per second). The foam intensity for white caps on the water surface changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setWhitecapSmoothByTime()](#setWhitecapSmoothByTime_float_void)*.
### Arguments

- *float* **unit_per_sec** - Constant rate (in units per second) with which the value gradually changes from the current to target.

## void setWhitecapSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [foam intensity for white caps on the water surface](#setWhitecap_float_void) by the specified time interval. The white caps on the water surface change gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setWhitecapSmoothBySpeed()](#setWhitecapSmoothBySpeed_float_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.

## void updateAllShorelines ( )

Forced shoreline update (affects all *[FieldShoreline](../../../../api/library/fields/class.fieldshoreline_cpp.md)* nodes).
