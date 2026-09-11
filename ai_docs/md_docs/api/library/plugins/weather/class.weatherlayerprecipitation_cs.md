# Unigine::Plugins::Weather::WeatherLayerPrecipitation Class (CS)

**Inherits from:** WeatherLayer


This class is used to represent a precipitation layer within a [weather region](../../../../api/library/plugins/weather/class.region_cs.md). It enables you to define the type of precipitation (rain, snow, etc.), a node (*[ObjectParticles](../../../../objects/effects/particles/index.md)*) to be used to visualize the precipitation effect, and manage the size of particles representing snowflakes or droplets.


## WeatherLayerPrecipitation Class

### Properties

## float ParticlesSize

The size of particles used to visualize the precipitation effect (snowflakes, droplets, etc.).
## int PrecipitationType

The value defining the type of the weather precipitation layer.
## 🔒︎ Node EffectNode

The node used to visualize the precipitation effect.
### Members

---

## void SetParticlesSizeSmoothBySpeed ( float unit_per_sec )

Sets the mode of smooth gradual change of the [particles size](#setParticlesSize_float_void) by the specified rate (in units per second). The particles size changes gradually from the current to target value by the specified value during each second, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). This method fits best when the difference between the target and current value is either too big (e.g. visibility distance change from 10m to 1km) or too small (e.g. from 1m to 1.05m), avoiding too fast or too slow changes. For other cases you can also choose another mode "by time" to change the value from the current to target during the specified time interval via the *[setParticlesSizeSmoothByTime()](#setParticlesSizeSmoothByTime_float_void)*.
### Arguments

- *float* **unit_per_sec** - Constant rate (in units per second) with which the value gradually changes from the current to target.

## void SetParticlesSizeSmoothByTime ( float sec )

Sets the mode of smooth gradual change of the [particles size](#setParticlesSize_float_void) by the specified time interval. The particles size changes gradually from the current to target value during this interval, such smoothing is performed to make changes more realistic. Moreover, each value can be changed with its own rate (the rain starting fast with a slowly changing cloud coverage). When the value of 0 is set, the value changes instantly. If the difference between the target and current value is too big (e.g. visibility distance change from 10m to 1km), the changes in this mode may be too fast and too noticeable, or on the contrary they might be too slow if the difference is too small (e.g. from 1m to 1.05m). In this case you can choose another mode to change the value with a specified rate via the *[setParticlesSizeSmoothBySpeed()](#setParticlesSizeSmoothBySpeed_float_void)*.
### Arguments

- *float* **sec** - Time interval (in seconds) during which the value changes from the current to target.
