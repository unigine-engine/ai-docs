# Unigine::Plugins::Weather::MeteoCameraEffects Class (CPP)

**Header:** #include <plugins/Unigine/Weather/UnigineWeather.h>


## MeteoCameraEffects Class

### Members

## Math:: dvec3 getPosition () const

Returns the current camera position in the world space.
### Return value

Current camera position in the world space.
## Math:: vec3 getVelocity () const

Returns the current camera velocity.
### Return value

Current camera velocity as a three-component vector, each component representing the speed along the corresponding axis, in meters per second.
## bool isRenderCloudsTransparentAutoOrder () const

Returns the current value indicating if automatic adjustment of [transparency rendering order for clouds](../../../../editor2/settings/render_settings/clouds/index.md#accurate_transparent_order) is enabled.
### Return value

**true** if automatic adjustment of transparency rendering order for clouds is enabled ; otherwise **false**.
## bool isRenderCloudsInterleaveOptimization () const

Returns the current value indicating if [interleaved rendering optimization for clouds](../../../../editor2/settings/render_settings/clouds/index.md#interleaved_rendering) is enabled.
### Return value

**true** if interleaved rendering optimization for clouds is enabled ; otherwise **false**.
## bool isRenderAnimationEnabled () const

Returns the current value indicating if wind animation is enabled (vegetation and water are affected by the wind).
### Return value

**true** if wind animation is enabled (vegetation and water are affected by the wind); otherwise **false**.
## float getCurrentVisibility () const

Returns the current visibility, in meters.
### Return value

Current visibility, in meters.
## Math:: vec3 getCurrentWind () const

Returns the current wind speed in all directions.
### Return value

Current wind speed in all directions.
---

## void setCloudsOptimizationDistance ( double interleave_1 , double interleave_2 )

Sets the distances from the camera at which the two levels of [interleaved rendering optimization for clouds](../../../../editor2/settings/render_settings/clouds/index.md#interleaved_rendering) should be used.
### Arguments

- *double* **interleave_1** - Distance from the camera (in meters) at which 2x2 interleaved rendering optimization is to be used for clouds.
- *double* **interleave_2** - Distance from the camera (in meters) at which 4x4 interleaved rendering optimization is to be used for clouds.
