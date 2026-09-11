# Water


This section contains settings related to water rendering.


### Common Settings


![Common Settings](water.png)

*Common Settings*


| Enabled | The value indicating if rendering of water is enabled. **enabled** by default. `Console access:render_water_enabled` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_enabled)) |
|---|---|
| SSR Enabled | The value indicating if the SSR (Screen Space Reflections) effect is enabled for water. **enabled** by default. `Console access:render_water_ssr` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_ssr)) ![](water_ssr_disabled.jpg) ![](water_ssr_enabled.jpg) |
| SSR Quality | The resolution of water SSR (Screen Space Reflections). One of the following values: - *Low* - low quality - *Medium* - medium quality (by default) - *High* - high quality - *Ultra* - ultra quality `Console access:render_water_ssr_quality` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_ssr_quality)) ![](water_ssr_enabled.jpg) ![](water_ssr_resolution_ultra.jpg) |
| SSR Increased Accuracy | The value indicating if increased accuracy for the water SSR (Screen Space Reflections). This option reduces visual artifacts by increasing accuracy of the last step. **disabled** by default. `Console access:render_water_ssr_increased_accuracy` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_ssr_increased_accuracy)) ![](water_ssr_accuracy_off.jpg) ![](water_ssr_enabled.jpg) |
| Refraction Quality | The quality of water refraction. One of the following values: - *Low* - low quality - *Medium* - medium quality - *High* - high quality (by default) - *Ultra* - ultra quality `Console access:render_water_refraction_quality` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_refraction_quality)) |
| Anisotropy Quality | The water texture anisotropy level. The following values are available: - 1x - anisotropy level 1 - 2x - anisotropy level 2 - 4x - anisotropy level 4 - 8x - anisotropy level 8 - 16x - anisotropy level 16 Option **#2** is selected by default (see above). `Console access:render_water_anisotropy` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_anisotropy)) |
| Shoreline Wetness | The value indicating if the wetness effect for objects near the shoreline is enabled. **enabled** by default. `Console access:render_water_shoreline_wetness` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_shoreline_wetness)) ![](water_shoreline_wetness_off.jpg) ![](water_shoreline_wetness_on.jpg) |
| Waterline Accuracy | The quality of underwater and waterline determination. Use high quality only if you need to submerge underwater (to see the waterline) and at medium and high Beaufort values. One of the following values: - *Low* - low quality (by default) - *Medium* - medium quality - *High* - high quality - *Ultra* - ultra quality `Console access:render_water_waterline_accuracy` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_waterline_accuracy)) |
| Render Underwater Shafts | The value indicating if rendering of underwater shafts is enabled. **enabled** by default. `Console access:render_water_shafts` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_shafts)) |
| Render Environment Probes | The value indicating if rendering of environment probes on the water surface is enabled. **enabled** by default. `Console access:render_water_environment_probes` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_environment_probes)) ![](water_render_lights_off.jpg) ![](water_render_env_probes_on.jpg) |
| Render Voxel Probes | The value indicating if voxel probes are enabled for water rendering. **enabled** by default. `Console access:render_water_voxel_probes` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_voxel_probes)) |
| Render Lights | The value indicating if rendering of lights on the water surface is enabled. > **Notice:** The option doesn't affect the [World Light source](../../../../objects/lights/world/index.md). **enabled** by default. `Console access:render_water_lights` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_lights)) ![](water_render_lights_off.jpg) ![](water_render_lights_on.jpg) |
| Opacity Depth | The value indicating if depth data for water is written to the opacity buffer. **enabled** by default. `Console access:render_water_opacity_depth` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_opacity_depth)) |
| Field Height Resolution | The resolution of the texture into which all textures set for all *[FieldHeight](../../../../api/library/fields/class.fieldheight_cpp.md)* objects are rendered. > **Notice:** Increased resolution significantly affects performance. One of the following values: - 128 x 128 - 256 x 256 - 512 x 512 (by default) - 1024 x 1024 - 2048 x 2048 - 4096 x 4096 - 8192 x 8192 `Console access:render_field_height_resolution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_field_height_resolution)) |
| Field Precision 32 bits | The value indicating the precision of textures used for field objects. Either of the following: - 16-bit precision R16 texture - 32-bit precision R32F texture Option **#1** is selected by default (see above). `Console access:render_field_precision` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_field_precision)) |
| Field Shoreline Resolution | The resolution of the texture into which all textures set for all *[FieldShoreline](../../../../api/library/fields/class.fieldshoreline_cpp.md)* objects are rendered. > **Notice:** Increased resolution significantly affects performance. One of the following values: - 128x128 (by default) - 256x256 - 512x512 - 1024x1024 - 2048x2048 - 4096x4096 - 8192x8192 `Console access:render_field_shoreline_resolution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_field_shoreline_resolution)) |


### Geometry Settings


![Geometry Settings](water_geometry.png)

*Geometry Settings*


| Preset | The index of the Global Water geometry preset used at the moment. To customize the Global Water geometry preset options at run time you should activate the **Custom** preset: One of the following values: - Low (by default) - Medium - High - Ultra - Extreme - Custom `Console access:render_water_geometry_preset` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_geometry_preset)) |
|---|---|


#### Customizable Settings


The following settings are available when the *[Custom](#geometry_preset)* preset is selected.


| Geometry Progression | The progression of [Global Water](../../../../objects/objects/water/water_object.md) geometry tessellation. Range of values: **[0.0f, 50.0f]**. The default value is : **1.5f**. `Console access:render_water_geometry_progression` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_geometry_progression)) |
|---|---|
| Geometry Progression Fov Min | The minimum camera field of view value taken into account for tessellation of [Global Water](../../../../objects/objects/water/water_object.md) geometry, in degrees. Tessellation distances are scaled proportionally to the ratio of 60 degrees to the current camera FOV, so that narrow fields of view (zoom optics, long lenses, binocular views) get detailed water geometry at longer distances. The FOV value used in this calculation is clamped to be no less than this minimum, preventing excessive tessellation at extremely narrow FOV values. Range of values: **[0.01f, 60.0f]**. The default value is : **1.5f**. `Console access:render_water_geometry_progression_fov_min` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_geometry_progression_fov_min)) |
| Geometry Progression Fov Scale | The intensity of [Global Water](../../../../objects/objects/water/water_object.md) tessellation compensation for narrow camera fields of view. Tessellation distances are scaled proportionally to the ratio of 60 degrees to the current camera FOV raised to the power of this value: by 0, the camera FOV does not affect tessellation distances at all; by 1, the scaling is strictly linear. Intermediate values soften the compensation. Range of values: **[0.0f, 1.0f]**. The default value is : **0.75f**. `Console access:render_water_geometry_progression_fov_scale` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_geometry_progression_fov_scale)) |
| Geometry Fade Lods | The intensity of fading between levels of [Global Water](../../../../objects/objects/water/water_object.md) geometry tessellation. This value can be increased to remove sharp edges between areas with different geometry density. Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**. `Console access:render_water_geometry_fade_lods` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_geometry_fade_lods)) |
| Geometry Subpixel Reduction | The minimum ratio of a polygon size (in screen space) to the size of an area seen in the viewport. If the ratio calculated for the polygon is less than this value, such polygon will be removed. Range of values: **[0.0f, 50.0f]**. The default value is : **6.0f**. `Console access:render_water_geometry_subpixel_reduction` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_geometry_subpixel_reduction)) |
| Geometry Polygon Size | The size of [Global Water](../../../../objects/objects/water/water_object.md) polygons. The value defines the maximum allowed density of Global Water geometry. If the polygon size is large, small waves will be lost. It is better to set this parameter to about 1/3 or 1/4 of the smallest wavelength. Range of values: **[0.0f, 1000.0f]**. The default value is : **0.01f**. `Console access:render_water_geometry_polygon_size` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_geometry_polygon_size)) |
| Visibility Distance | The maximum visibility distance for the [Global Water](../../../../objects/objects/water/water_object.md). The water is visible, as long as the distance between the camera and the water object does not exceed this value. Range of values: **[0.0f, inf]**. The default value is : **30000.0f**. `Console access:render_water_visible_distance` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_visible_distance)) |


### Culling Settings


![Culling Settings](water_culling.png)

*Culling Settings*


| Culling Aggressive | The value indicating if frustum culling optimization is enabled for the [Global Water](../../../../objects/objects/water/water_object.md). When enabled, the number of culled polygons increases thereby increasing performance. In case of any issues with polygons rendering, try disabling this option (however, note that performance may drop). **enabled** by default. `Console access:render_water_culling_aggressive` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_culling_aggressive)) |
|---|---|
| Culling Frustum Padding | The value, by which the borders of the current frustum are increased. Frustum culling is performed for the frustum of the increased size. By the maximum value of 1, the frustum borders will be increased by the size of the current frustum. Range of values: **[0.0f, 1.0f]**. The default value is : **0.1f**. `Console access:render_water_culling_frustum_padding` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_culling_frustum_padding)) |
| Culling Oblique Frustum | The multiplier for the size of viewing frustum used for culling polygons of *[Global Water](../../../../objects/objects/water/water_object.md)* object beyond the oblique frustum plane. The higher the value, the more patches will be culled. Range of values: **[0.0f, 1.0f]**. The default value is : **0.9f**. `Console access:render_water_culling_oblique_frustum` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_water_culling_oblique_frustum)) |
