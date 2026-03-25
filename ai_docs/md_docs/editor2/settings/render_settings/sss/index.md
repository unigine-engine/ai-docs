# Subsurface Scattering


This section contains settings related to the Screen-Space Subsurface Scattering effect. This effect should be used to imitate human skin, wax, etc.


> **Notice:** Do not forget to enable the SSSSS effect for a material.


![Subsurface scattering settings](sss_preset.png)


## Common Parameters


| Screen-Space Subsurface Scattering | The  value indicating if the SSSSS (Screen-Space Subsurface Scattering) effect is enabled. This effect is used to imitate human skin, wax, etc. **disabled** by default. `Console access:render_sssss` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss)) |  |  |
|---|---|---|---|
| Preset | The SSSSS (Screen-Space Subsurface Scattering) preset used at the moment. To customize the SSSSS effect options at run time you should activate the **Custom** preset: One of the following values: - Low (by default) - Medium - High - Ultra - Extreme - Custom `Console access:render_sssss_preset` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_preset)) > **Notice:** Presets override user-defined custom settings. When any preset other than Custom is active, modification of the parameters via [API](../../../../api/library/rendering/class.render_cpp.md) has no effect. The parameter value set via the last API call shall be used only when the Custom preset is active. When checking the current parameter value via API you'll get the corresponding setting stored in the active preset (default or custom one). |  |  |
| Radius | The  [subsurface scattering radius](../../../../editor2/settings/render_settings/sss/index.md#sss_radius) - distance in the screen space, within which colors will be sampled.It controls how much wrinkles, pores and cavities will be blurred and highlighted. The higher the value, the farther subsurface scattering reaches. Too high values result in the ghosting effect. By the minimum value of 0, no subsurface scattering is rendered. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_sssss_radius` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_radius)) \| ![Radius = 1](sss_0.png) *Radius = 1* \| ![Radius = 0.2](sss_1.png) *Radius = 0.2* \| \|---\|---\| | ![Radius = 1](sss_0.png) *Radius = 1* | ![Radius = 0.2](sss_1.png) *Radius = 0.2* |
| ![Radius = 1](sss_0.png) *Radius = 1* | ![Radius = 0.2](sss_1.png) *Radius = 0.2* |  |  |
| SSSSS Color | The  [subsurface scattering color](../../../../editor2/settings/render_settings/sss/index.md#sss_color) used to simulate the subsurface component of skin lighting, i.e. the light that bounces inside of the subsurface tissue layers (epidermis and dermis) before exiting.For skin, subsurface color is reddish, due to blood circulating in skin tissues. To use this option, SSSSS effect *[SSSSS](#render_sssss)* should be enabled. **vec4(1.0f, 0.0f, 0.0f, 1.0f)** - default value `Console access:render_sssss_color` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_color)) |  |  |
| Threshold Min | The threshold of SSSSS (Screen-Space Subsurface Scattering) for the material's [Translucent](../../../../content/materials/library/mesh_base/index.md#parameter_translucency) parameter equal to 0 (minimum translucency). To use this option, the SSSSS effect*[SSSSS](#render_sssss)* should be enabled. Range of values: **[0.0f, inf]**. The default value is : **4.0f**. `Console access:render_sssss_min_threshold` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_min_threshold)) |  |  |
| Threshold Max | The threshold of SSSSS (Screen-Space Subsurface Scattering) for the material's [Translucent](../../../../content/materials/library/mesh_base/index.md#parameter_translucency) parameter equal to 1 (maximum translucency). To use this option, the SSSSS effect*[SSSSS](#render_sssss)* should be enabled. Range of values: **[0.0f, inf]**. The default value is : **10.0f**. `Console access:render_sssss_max_threshold` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_max_threshold)) |  |  |


## Translucency Options


| Translucent Color | The color used for translucent objects globally. When light shines on one side of the object, the other side is partially illuminated with this color. **vec4(1.0f, 1.0f, 1.0f, 1.0f)** - default value (white) `Console access:render_translucent_color` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_translucent_color)) ![](translucency_0.png) ![](translucency_1.png) |
|---|---|


## Customizable Settings


The following settings are available when the [Custom](#preset) preset is selected.


![SSS custom settings](sss.png)

*Subsurface Scattering Settings*


| Diffuse | The value indicating if the SSSSS (Screen-Space Subsurface Scattering) calculation for diffuse lighting (directional lights) is enabled. If this option is not required, disable it to save performance. To use this option, the SSSSS effect*[SSSSS](#render_sssss)* should be enabled. **enabled** by default. `Console access:render_sssss_diffuse` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_diffuse)) |  |  |
|---|---|---|---|
| Ambient | The value indicating if the SSSSS (Screen-Space Subsurface Scattering) calculation for ambient lighting (environment) is enabled. If this option is not required, disable it to save performance. To use this option, the SSSSS effect*[SSSSS](#render_sssss)* should be enabled. **disabled** by default. `Console access:render_sssss_ambient` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_ambient)) |  |  |
| Quality | The [quality](../../../../editor2/settings/render_settings/sss/index.md#sss_quality) of the SSSSS (Screen-Space Subsurface Scattering) effect. One of the following values: - *Low* - low quality - *Medium* - medium quality (by default) - *High* - high quality - *Ultra* - ultra quality `Console access:render_sssss_quality` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_quality)) \| ![Quality = Low](sss_low.png) *Quality = Low* \| ![Quality = Ultra](sss_ultra.png) *Quality = Ultra* \| \|---\|---\| | ![Quality = Low](sss_low.png) *Quality = Low* | ![Quality = Ultra](sss_ultra.png) *Quality = Ultra* |
| ![Quality = Low](sss_low.png) *Quality = Low* | ![Quality = Ultra](sss_ultra.png) *Quality = Ultra* |  |  |
| Resolution | The [resolution](../../../../editor2/settings/render_settings/sss/index.md#sss_resolution) of the SSSSS (Screen-Space Subsurface Scattering) effect. One of the following values: - *Quarter* - quarter resolution - *Half* - half resolution (by default) - *Full* - full resolution `Console access:render_sssss_resolution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_resolution)) |  |  |
| Noise Ray | The intensity of the ray noise used for SSSSS (Screen-Space Subsurface Scattering) calculation to reduce banding artifacts of tracing. Higher values make banding less visible. To use this option, the SSSSS effect*[SSSSS](#render_sssss)* should be enabled. Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**. `Console access:render_sssss_noise_ray` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_noise_ray)) |  |  |
| Noise Step | The intensity of the step noise used for SSSSS (Screen-Space Subsurface Scattering) calculation to reduce banding artifacts of tracing. Higher values make banding less visible. To use this option, the SSSSS effect*[SSSSS](#render_sssss)* should be enabled. Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**. `Console access:render_sssss_noise_step` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_noise_step)) |  |  |


### Interleaved Rendering Options


| Enabled | The value indicating if the [interleaved rendering mode](../../../../editor2/settings/render_settings/sss/index.md#sss_interleaved) for SSSSS (Screen-Space Subsurface Scattering) is enabled. This option enables rendering of the effect in only half or quarter of all pixels with subsequent reconstruction of neighboring pixels using the data from previous frames, significantly improving performance. The effect is cumulative and works best with *[Temporal Filter](../../../../editor2/settings/render_settings/sss/index.md#taa)*, which reduces ghosting and noise artifacts. **disabled** by default. `Console access:render_sssss_interleaved` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_interleaved)) |
|---|---|
| Samples | The number of pixels to be skipped when rendering the SSSSS (Screen-Space Subsurface Scattering) effect with subsequent reconstruction of neighboring pixels using the data from previous frames. The following options are available: - **1 x 2** (1.0 * width x 0.5 * height) - a half of all pixels is rendered, skipping each second line - **2 x 2** (0.5 * width x 0.5 * height) - a quarter of all pixels is rendered, skipping each second line and row Option **#1** is selected by default (see above). `Console access:render_sssss_interleaved_samples` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_interleaved_samples)) |
| Color Clamping | The [color clamping mode](../../../../editor2/settings/render_settings/sss/index.md#sss_interleaved_color_clamping) used to reduce ghosting effect. *Higher* values increase clamping intensity, but may cause flickering (to reduce flickering you can choose **High + Velocity**). When disabled, translucency has a lag as it is several frames behind. One of the following values: - Disabled - Low (by default) - Medium - High - High + Velocity `Console access:render_sssss_interleaved_color_clamping` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_interleaved_color_clamping)) |


### Temporal Filtering Options


| Fix Flicker | The value indicating if the taa [fix flicker](../../../../principles/render/antialiasing/taa.md#taa_fix_flicker) option is enabled. This option fixes flickering edges caused by TAA: it removes bright pixels by using the pixel brightness information from the previous frame. It is recommended to enable the option for bright thin ropes, wires and lines. The option is available only when TAA*[TAA](#render_taa)* is enabled. > **Notice:** Enabling this option may increase performance costs. **enabled** by default. `Console access:render_taa_fix_flicker` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_taa_fix_flicker)) |
|---|---|
| Frames By Color | The value of TAA parameter for Screen-Space Subsurface Scattering that is similar to [TAA Frames By Color](#render_taa_frames_by_color)*[TAAFramesByColor](#render_taa_frames_by_color)*. **enabled** by default. `Console access:render_sssss_taa_frames_by_color` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_taa_frames_by_color)) |
| Fix Blur | The value of TAA parameter for Screen-Space Subsurface Scattering that is similar to [TAA Catmull Resampling](#render_taa_catmull_resampling)*[TAACatmullResampling](#render_taa_catmull_resampling)*. **enabled** by default. `Console access:render_sssss_taa_catmull_resampling` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_taa_catmull_resampling)) |
| Antialiasing In Motion | The value of TAA parameter for Screen-Space Subsurface Scattering that is similar to [TAA Antialiasing In Motion](#render_taa_antialiasing_in_motion)*[TAAAntialiasingInMotion](#render_taa_antialiasing_in_motion)*. **disabled** by default. `Console access:render_sssss_taa_antialiasing_in_motion` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_taa_antialiasing_in_motion)) |
| Preserve Details | The value of TAA parameter for Screen-Space Subsurface Scattering that is similar to [TAA Preserve Details](#render_taa_preserve_details)*[TAAPreserveDetails](#render_taa_preserve_details)*. Range of values: **[0.0f, inf]**. The default value is : **0.5f**. `Console access:render_sssss_taa_preserve_details` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_taa_preserve_details)) |
| Frame Count | The value of TAA parameter for Screen-Space Subsurface Scattering that is similar to [TAA Frame Count](#render_taa_frame_count)*[TAAFrameCount](#render_taa_frame_count)*. Range of values: **[0.0f, inf]**. The default value is : **30.0f**. `Console access:render_sssss_taa_frame_count` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_taa_frame_count)) |


#### Frames By Velocity


| Enabled | The value of TAA parameter for Screen-Space Subsurface Scattering that is similar to [TAA Frames By Velocity](#render_taa_frames_by_velocity)*[TAAFramesByVelocity](#render_taa_frames_by_velocity)*. **enabled** by default. `Console access:render_sssss_taa_frames_by_velocity` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_taa_frames_by_velocity)) |
|---|---|
| Threshold | The value of TAA parameter for Screen-Space Subsurface Scattering that is similar to [TAA Frames Velocity Threshold](#render_taa_frames_velocity_threshold)*[TAAFramesVelocityThreshold](#render_taa_frames_velocity_threshold)*. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_sssss_taa_frames_velocity_threshold` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sssss_taa_frames_velocity_threshold)) |
