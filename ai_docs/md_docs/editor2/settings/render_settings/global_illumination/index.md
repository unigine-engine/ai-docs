# Global Illumination Settings


This section contains global illumination settings.


![Indirect Lighting Interleaved Parameters](gi_preset.png)


## Indirect Lighting Interleaved Parameters


| Indirect Lighting Interleaved | The value indicating if interleaved mode for rendering indirect lighting is enabled. When enabled, lights are rendered in half resolution with subsequent reconstruction of neighboring pixels using the data from previous frames. This mode requires a high framerate (60+ FPS), otherwise anti-aliasing quality reduces and ghosting effect becomes more pronounced. Recommended for relatively static scenes which contain a lot of light sources and do not have a lot of reflective surfaces (in case of small number of light sources may reduce performance). **disabled** by default. `Console access:render_indirect_lighting_interleaved` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_indirect_lighting_interleaved)) |
|---|---|
| Samples | The number of samples for interleaved rendering of indirect lighting defining the number of pixels to be skipped during interleaved rendering of indirect lighting with subsequent reconstruction of neighboring pixels using the data from previous frames (defines the size of reduced lights buffer relative to original size). - **1 x 2** - half of all pixels are rendered skipping each second line (1.0 * width x 0.5 * height) - **2 x 2** - quarter of all pixels are rendered skipping each second line and row (0.5 * width x 0.5 * height) Option **#2** is selected by default (see above). `Console access:render_indirect_lighting_interleaved_samples` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_indirect_lighting_interleaved_samples)) |
| Color Clamping | The color clamping mode to be used for interleaved rendering of indirect lighting. This mode is used to reduce ghosting effect: higher values increase clamping intensity but may cause flickering on rippled reflective surfaces (as this mode is not so good at the object's edges). When disabled, shadows and reflections have a lag as they are several frames behind. One of the following values: - Disabled - Low - High (by default) `Console access:render_indirect_lighting_interleaved_color_clamping` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_indirect_lighting_interleaved_color_clamping)) |
| Color Clamping Intensity | The constant size of the intensity of color clamping for interleaved indirect lighting. Range of values: **[0.0f, 100.0f]**. The default value is : **0.0f**. `Console access:render_indirect_lighting_interleaved_color_clamping_intensity` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_indirect_lighting_interleaved_color_clamping_intensity)) |
| Color Clamping Velocity Threshold | The velocity threshold of color clamping for interleaved indirect lighting. The higher the value, the less the ghosting effect. However, increasing the threshold may change the overall image brightness due to excessive color clamping. Range of values: **[0.0f, 1000.0f]**. The default value is : **100.0f**. `Console access:render_indirect_lighting_interleaved_color_clamping_velocity_threshold` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_indirect_lighting_interleaved_color_clamping_velocity_threshold)) |
| Catmull Resampling | The value indicating whether Catmull-Rom resampling is enabled or not. Catmull-Rom resampling allows you to reduce image blurring when the camera moves forward/backward. It is recommended to disable resampling for low quality presets. **disabled** by default. `Console access:render_indirect_lighting_interleaved_catmull_resampling` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_indirect_lighting_interleaved_catmull_resampling)) |


The UNIGINE Global Illumination system contains three major components that are configured via the settings in the corresponding tabs:


## Articles in This Section

- [Indirect Diffuse](../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/index.md)

  - [SSAO](../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssao/index.md)
  - [SSGI](../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssgi/index.md)
  - [Bent Normal](../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/bent_normal/index.md)

- [Indirect Specular](../../../../editor2/settings/render_settings/ssr/index.md)

- [Denoise](../../../../editor2/settings/render_settings/global_illumination/denoise/index.md)
