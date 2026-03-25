# Lights


This section contains lights-related settings, such as lens flares effect, batching and interleaved rendering parameters as well as per-object limits for forward rendering pass.


![Lights settings](lights.png)

*Lights Settings*


| Deferred Lights | The value indicating if rendering of lights is enabled. **enabled** by default. `Console access:render_lights_enabled` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_lights_enabled)) |
|---|---|
| Lens Flares | The value indicating if rendering of [per-light lens flares](../../../../api/library/lights/class.light_cpp.md#setLensFlaresEnabled_int_void) is enabled. **enabled** by default. `Console access:render_lights_lens_flares` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_lights_lens_flares)) |


### Direct Lighting Interleaved Rendering Options


| Enabled | The value indicating if interleaved mode for rendering direct lighting is enabled. When enabled, lights are rendered in half resolution with subsequent reconstruction of neighboring pixels using the data from previous frames. This mode requires a high framerate (60+ FPS), otherwise anti-aliasing quality reduces and ghosting effect becomes more pronounced. Recommended for relatively static scenes which contain a lot of light sources and do not have a lot of reflective surfaces (in case of small number of light sources may reduce performance). **disabled** by default. `Console access:render_direct_lighting_interleaved` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_direct_lighting_interleaved)) |
|---|---|
| Samples | The number of samples for interleaved rendering of direct lighting defining the number of pixels to be skipped during interleaved rendering of direct lighting with subsequent reconstruction of neighboring pixels using the data from previous frames (defines the size of reduced lights buffer relative to original size). - **1 x 2** - half of all pixels are rendered skipping each second line (1.0 * width x 0.5 * height) - **2 x 2** - quarter of all pixels are rendered skipping each second line and row (0.5 * width x 0.5 * height) Option **#1** is selected by default (see above). `Console access:render_direct_lighting_interleaved_samples` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_direct_lighting_interleaved_samples)) |
| Color Clamping | The color clamping mode to be used for interleaved rendering of direct lighting. This mode is used to reduce ghosting effect: higher values increase clamping intensity but may cause flickering on rippled reflective surfaces (as this mode is not so good at the object's edges). When disabled, shadows and reflections have a lag as they are several frames behind. One of the following values: - Disabled - Low (by default) - Medium - High - High + Velocity `Console access:render_direct_lighting_interleaved_color_clamping` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_direct_lighting_interleaved_color_clamping)) |
| Catmull Resampling | The value indicating if the Catmull-Rom resampling for interleaved rendering of direct lighting is enabled. This mode allows you to reduce image blurring when the camera moves forward/backward. **disabled** by default. `Console access:render_direct_lighting_interleaved_catmull_resampling` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_direct_lighting_interleaved_catmull_resampling)) |


### Forward Per-Object Limits


| World | The maximum number of World lights per object (available only for materials rendered in the [forward rendering pass](../../../../principles/render/sequence/index.md#transparent)). You should set the nonzero value to increase performance: it is not recommended to use more than 4 World lights per object. Range of values: **[0, 128]**. The default value is : **4**. `Console access:render_lights_forward_per_object_world` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_lights_forward_per_object_world)) |
|---|---|
| Omni | The maximum number of Omni lights per object (available only for materials rendered in the [forward rendering pass](../../../../principles/render/sequence/index.md#transparent)). You should set the nonzero value to increase performance: it is not recommended to use more than 4 Omni lights per object. Range of values: **[0, 128]**. The default value is : **4**. `Console access:render_lights_forward_per_object_omni` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_lights_forward_per_object_omni)) |
| Proj | The maximum number of Projected lights per object (available only for materials rendered in the [forward rendering pass](../../../../principles/render/sequence/index.md#transparent)). You should set the nonzero value to increase performance: it is not recommended to use more than 4 Projected lights per object. Range of values: **[0, 128]**. The default value is : **4**. `Console access:render_lights_forward_per_object_proj` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_lights_forward_per_object_proj)) |
| Environment Probe | The maximum number of Environment Probes per object (available only for materials rendered in the [forward rendering pass](../../../../principles/render/sequence/index.md#transparent)). You should set the nonzero value to increase performance: it is not recommended to use more than 4 Voxel Probes per object. Range of values: **[0, 128]**. The default value is : **4**. `Console access:render_lights_forward_per_object_env` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_lights_forward_per_object_env)) |
| Voxel Probe | The maximum number of Voxel Probes per object (available only for materials rendered in the [forward rendering pass](../../../../principles/render/sequence/index.md#transparent)). You should set the nonzero value to increase performance: it is not recommended to use more than 4 Voxel Probes per object. Range of values: **[0, 128]**. The default value is : **4**. `Console access:render_lights_forward_per_object_voxel` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_lights_forward_per_object_voxel)) |
