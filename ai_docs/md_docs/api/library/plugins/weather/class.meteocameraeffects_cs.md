# Unigine::Plugins::Weather::MeteoCameraEffects Class (CS)


## MeteoCameraEffects Class

### Properties

## 🔒︎ dvec3 Position

The camera position in the world space.
## 🔒︎ vec3 Velocity

The camera velocity.
## 🔒︎ bool IsRenderCloudsTransparentAutoOrder

The value indicating if automatic adjustment of [transparency rendering order for clouds](../../../../editor2/settings/render_settings/clouds/index.md#accurate_transparent_order) is enabled.
## 🔒︎ bool IsRenderCloudsInterleaveOptimization

The value indicating if [interleaved rendering optimization for clouds](../../../../editor2/settings/render_settings/clouds/index.md#interleaved_rendering) is enabled.
## 🔒︎ bool IsRenderAnimationEnabled

The value indicating if wind animation is enabled (vegetation and water are affected by the wind).
## 🔒︎ float CurrentVisibility

The visibility, in meters.
## 🔒︎ vec3 CurrentWind

The wind speed in all directions.
### Members

---

## void SetCloudsOptimizationDistance ( double interleave_1 , double interleave_2 )

Sets the distances from the camera at which the two levels of [interleaved rendering optimization for clouds](../../../../editor2/settings/render_settings/clouds/index.md#interleaved_rendering) should be used.
### Arguments

- *double* **interleave_1** - Distance from the camera (in meters) at which 2x2 interleaved rendering optimization is to be used for clouds.
- *double* **interleave_2** - Distance from the camera (in meters) at which 4x4 interleaved rendering optimization is to be used for clouds.
