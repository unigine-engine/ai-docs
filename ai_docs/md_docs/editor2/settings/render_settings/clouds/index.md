# Clouds


This section contains settings for clouds.


![](clouds.png)

*Clouds Settings*


## Common


| Enable Clouds | The value indicating if rendering of clouds is enabled. **enabled** by default. `Console access:render_clouds_enabled` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_enabled)) |
|---|---|
| Mode | The clouds rendering mode. Rendering clouds into the panorama cubemap texture once per frame automatically makes the clouds seen in simple default environment-based reflections making them look more natural for a reduced cost. However, rendering views from inside the clouds is possible in *Volumetric* mode only. One of the following values: - *Volumetric* - render volumetric clouds (by default) - *Render To Panorama* - render clouds to panorama (environment cubemap) `Console access:render_clouds_mode` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_mode)) |
| Panorama Resolution | The resolution of the panorama cubemap texture. Available for *Render To Panorama* [clouds mode](#render_clouds_mode). One of the following values: - 128x128 - 256x256 - 384x384 - 512x512 - 768x768 (by default) - 1024x1024 - 1536x1536 - 2048x2048 - 4096x4096 `Console access:render_clouds_panorama_resolution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_panorama_resolution)) |
| Reuse Panorama Between Viewports | The value indicating if the panorama cubemap texture is reused between several viewports. Available for *Render To Panorama* [clouds mode](#render_clouds_mode). **disabled** by default. `Console access:render_clouds_panorama_reuse` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_panorama_reuse)) |
| Ground Shadows | The value indicating if rendering of shadows from the clouds on the ground is enabled. **enabled** by default. `Console access:render_clouds_ground_shadows` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_ground_shadows)) |
| Accurate Layers Sorting | The value indicating if correct sorting of intersecting cloud layers is enabled. > **Notice:** Enabling this feature may reduce raymarching quality as samples shall be distributed among all layers. **disabled** by default. `Console access:render_clouds_accurate_layers_sorting` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_accurate_layers_sorting)) |
| Cutout By Far Clipping | The value indicating if [far-plane clipping](../../../../editor2/camera_settings/index.md#camera_settings) is used for clouds visibility. Controlling clouds visibility by increasing the far-plane distance significantly affects performance in many aspects (dynamic Environment Probes, etc.). You can disable this option when necessary as an optimization. **enabled** by default. `Console access:render_clouds_far_clipping` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_far_clipping)) |
| Transparent Order | The rendering order for clouds relative to transparent objects (except water). - **Render Before Transparent** - render clouds before all [transparent objects](../../../../principles/render/sequence/index.md#transparent) (except water). - **Render After Transparent** - render clouds after all [transparent objects](../../../../principles/render/sequence/index.md#transparent) (except water). - **Sort Transparent** - enable rough sorting for [transparent objects](../../../../principles/render/sequence/index.md#transparent) relative to clouds (*below the lowest cloud layer base -> inside the clouds -> above the highest cloud layer top*). Option **#1** is selected by default (see above). `Console access:render_clouds_transparent_order` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_transparent_order)) |
| Detail Distortion | The value indicating which texture type is used for clouds distortion at the moment. This parameter has a significant impact on performance: - **2D Texture** - more performance-friendly, but may cause an excessive vertical extrusion of clouds. - **3D Texture** - ensures homogeneous detail distortion and better image quality, but at a higher performance cost. Option **#1** is selected by default (see above). `Console access:render_clouds_distortion_texture` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_distortion_texture)) |
| Soft Intersection | The [soft intersection distance](../../../../editor2/settings/render_settings/clouds/index.md#soft_intersection) for clouds, in meters. Range of values: **[0.0f, 100000.0f]**. The default value is : **100.0f**. `Console access:render_clouds_soft_intersection` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_soft_intersection)) |


## Quality


![Clouds quality rendering settings](quality_preset.png)


| Preset | The index of the clouds quality preset used at the moment. One of the following values: - Low (by default) - Medium - High + Interleaved - High - Ultra + Interleaved - Ultra - Extreme + Interleaved - Extreme - Custom `Console access:render_clouds_quality_preset` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_quality_preset)) |
|---|---|


> **Notice:** Presets override user-defined custom settings. When any preset other than Custom is active, modification of the parameters via [API](../../../../api/library/rendering/class.render_cpp.md) has no effect. The parameter value set via the last API call shall be used only when the Custom preset is active. When checking the current parameter value via API, you'll get the corresponding setting stored in the active preset (default or custom one).


### Customizable Settings


The following settings are available when the *[Custom](#preset)* preset is selected.


![Clouds quality custom settings](quality.png)

*Clouds Quality Settings*


| Sampling Quality | The [sampling quality](../../../../editor2/settings/render_settings/clouds/index.md#sampling_quality) for clouds. This parameter sets the number of noise samples that affects the cloud shape processing quality. The higher the value, the less are visual artifacts. The following modes are available: - **Low** - 1 sample, low quality (higher cloud density) - **Medium** - 3 samples, medium quality - **High** - 5 samples, high quality - **Ultra** - 6 samples, ultra quality (lower density, the clouds are softer) > **Notice:** Visual difference between low and ultra quality is not significant. Therefore, it is recommended to use low settings, when possible, to gain performance. Option **#2** is selected by default (see above). `Console access:render_clouds_sampling_quality` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_sampling_quality)) |
|---|---|
| Lighting Quality | The [lighting quality](../../../../editor2/settings/render_settings/clouds/index.md#lighting_quality) for clouds. This parameter determines the number of samples used to calculate lighting for clouds. The following values are available: - **Low** - 1 sample, low quality - **Medium** - 3 samples, medium quality - **High** - 5 samples, high quality - **Ultra** - 6 samples, ultra quality > **Notice:** This parameter has a significant impact on performance. Therefore, it is recommended to use low settings, when possible. Option **#2** is selected by default (see above). `Console access:render_clouds_lighting_quality` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_lighting_quality)) |
| Samples Count | The [number of samples](../../../../editor2/settings/render_settings/clouds/index.md#samples_count) used for clouds rendering. The higher the value, the less noise in clouds rendering. The following values are available: - **Low** - 1 sample, low quality - **Medium** - 3 samples, medium quality - **High** - 5 samples, high quality - **Ultra** - 6 samples, ultra quality Option **#3** is selected by default (see above). `Console access:render_clouds_samples_count` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_samples_count)) |
| Step Accuracy | The accuracy of ray marching steps. This parameter enables you to improve the visual look of clouds when viewed from inside a cloud layer. It reduces the noise of lighting and clouds shape for long ray marching distances, adds some noise-based blur to a sharp border at the bottom sphere of the cloud layer (rounded) and removes popping effect when leaving a rounded cloud layer. *Higher* values provide more accurate form and less noise, while *lower* ones gain more performance. Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**. `Console access:render_clouds_step_accuracy` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_step_accuracy)) |
| Downsampling Rendering | The downsampling rendering mode for clouds. This parameter determines clouds resolution based on current screen resolution. > **Notice:** This parameter has a significant impact on performance. One of the following values: - *Quarter* - quarter resolution - *Half* - half resolution (by default) - *Full* - full resolution `Console access:render_clouds_downsampling_rendering` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_downsampling_rendering)) |
| Interleaved Rendering | The [interleaved rendering mode](../../../../editor2/settings/render_settings/clouds/index.md#interleaved_rendering) for clouds. In cases when clouds are viewed from the ground, or from above (at significant distance) and viewer's velocities are less than 200 units per second, this parameter can be used to provide a significant gain in performance. One of the following values: - Disabled (by default) - 2�2 - 4�4 - 8�8 `Console access:render_clouds_interleaved_rendering` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_interleaved_rendering)) |
| Depth Based Reconstruction | The value indicating if clouds ray-marched depth is used for upsampling the downsampled clouds without obscuring the geometry and reprojection depending on the cloud depth. Recommended for flying through clouds. > **Notice:** Works only with the clouds downsampling rendering mode*[CloudsDownsamplingRendering](#render_clouds_downsampling_rendering)* set to half and/or the clouds interleaved rendering mode*[CloudsInterleavedRendering](#render_clouds_interleaved_rendering)* set to 2x2. **disabled** by default. `Console access:render_clouds_depth_based_reconstruction` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_depth_based_reconstruction)) |
| Interleaved Rendering Temporal | The value indicating if temporal accumulation of noises for interleaved sampling for clouds is enabled. > **Notice:** Works only when the clouds interleaved rendering mode*[CloudsInterleavedRendering](#render_clouds_interleaved_rendering)* is set to 2x2. **enabled** by default. `Console access:render_clouds_interleaved_rendering_temporal` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_interleaved_rendering_temporal)) |
| Depth Based Reconstruction Threshold | The depth threshold value for clouds depth-based reconstruction mode*[CloudsDepthBasedReconstruction](#render_clouds_depth_based_reconstruction)*. This value defines the depth difference starting from which pixels are considered to be related to different surfaces. Range of values: **[0.0f, inf]**. The default value is : **100.0f**. `Console access:render_clouds_depth_based_reconstruction_threshold` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_depth_based_reconstruction_threshold)) |
| Noise Step | The value of the *noise step* parameter for clouds. This parameter determines the amount of jitter in the areas within clouds, that is used to reduce banding effect due to insufficient number of steps. Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**. `Console access:render_clouds_noise_step` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_noise_step)) |
| Noise Iterations | The value of the *noise iterations* parameter for clouds. This parameter determines the amount of jitter in the areas within clouds, that is used to reduce banding effect due to insufficient number of steps. Range of values: **[0.0f, 1.0f]**. The default value is : **0.1f**. `Console access:render_clouds_noise_iterations` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_noise_iterations)) |
| Noise Lighting | The value of the *noise lighting* parameter for the clouds. This parameter determines the amount of jitter for tracing steps of lighting calculation, that is used to reduce banding effect due to insufficient number of steps. Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**. `Console access:render_clouds_noise_lighting` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_noise_lighting)) |
| Noise Step Skip | The value of the *noise step skip* parameter for clouds. This parameter determines the amount of jitter in the areas between clouds, that is used to reduce banding effect due to insufficient number of steps. Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**. `Console access:render_clouds_noise_step_skip` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_noise_step_skip)) |


## Lighting


| Lighting Trace Length | The [lighting trace length](../../../../editor2/settings/render_settings/clouds/index.md#lighting_trace_length) for clouds. This parameter determines the maximum length of a sun ray inside a cloud. Range of values: **[1.0f, 2048.0f]**. The default value is : **230.0f**. `Console access:render_clouds_lighting_tracelength` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_lighting_tracelength)) |
|---|---|
| Lighting Cone Radius | The [lighting cone sampling radius](../../../../editor2/settings/render_settings/clouds/index.md#lighting_cone_radius) for clouds lighting. > **Notice:** Low values may result in unnatural behavior as the position of the sun changes. Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**. `Console access:render_clouds_lighting_cone_radius` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_lighting_cone_radius)) |
| Lighting Samples Distribution | The value that controls distribution of samples for clouds lighting. Can be used to keep small details for long shadows when the lighting trace length value*[CloudsLightingTraceLength](#render_clouds_lighting_tracelength)* is high. Range of values: **[0.001f, 5.0f]**. The default value is : **1.0f**. `Console access:render_clouds_lighting_samples_distribution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_lighting_samples_distribution)) |


## Rounded


| Enable Rounded | The value indicating if cloud layers are to be curved to make them look more natural imitating planet's curvature. **enabled** by default. `Console access:render_clouds_rounded` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_rounded)) ![](clouds_rounded_off.png) ![](clouds_rounded_on.png) |
|---|---|
| Planet Radius | The radius of the planet to be used for clouds curving. Visual curving can be used to make clouds look more natural imitating planet's curvature. Range of values: **[100.0f, inf]**. The default value is : **200000.0f**. `Console access:render_clouds_rounded_planet_radius` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_rounded_planet_radius)) |


## Dynamic Coverage


| Dynamic Coverage Resolution | The the value defining the size of the square dynamic coverage resolution texture for clouds, in pixels. This parameter determines the quality of dynamic coverage texture for [FieldWeather](../../../../objects/effects/fields/field_weather/index.md) objects. Higher values make it possible to preserve texture details at high distances. > **Notice:** Increased resolution significantly affects performance. Range of values: **[16, 8192]**. The default value is : **256**. `Console access:render_clouds_dynamic_coverage_resolution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_dynamic_coverage_resolution)) The following values are available: - **128 x 128** - **256 x 256** - **512 x 512** - **1024 x 1024** - **2048 x 2048** |
|---|---|
| Dynamic Coverage Area | The dynamic coverage area for clouds, in units. This parameter determines visibility distance for coverage of [FieldWeather](../../../../objects/effects/fields/field_weather/index.md) objects. > **Notice:** Increasing dynamic coverage area leads to reduction of quality of FieldWeather coverage texture and loss of details. This effect can be mitigated by increasing dynamic coverage resolution using the corresponding command*[CloudsDynamicCoverageResolution](#render_clouds_dynamic_coverage_resolution)*. Range of values: **[10.0f, 400000.0f]**. The default value is : **10000.0f**. `Console access:render_clouds_dynamic_coverage_area` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_clouds_dynamic_coverage_area)) |
