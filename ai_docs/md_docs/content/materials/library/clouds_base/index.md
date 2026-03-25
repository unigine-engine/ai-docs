# clouds_base


A *clouds_base* material is used to create realistic volumetric clouds. It is applied to CloudLayer object.

 Prior KnowledgeThis article assumes you have prior knowledge of the following topics. Please read them before proceeding:
- *[Materials Settings.](../../../../editor2/materials_settings/index.md)*
- *[mesh_base material states, textures, parameters.](../../../../content/materials/library/mesh_base/index.md)*


![](clouds.png)


## Common


![Common Group](common_group.png)


| Layer Type | Type of the cloud layer: - **Infinite** - a global layer of clouds spread inifinitely. - **Defined** - a layer of clouds of the specified size (limited to a certain area), this type is used for regional weather. |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|
| Layer Size | Size of the cloud layer alonx X and Y axes, in units. > **Notice:** Available only when the [Layer Type](#layer_type) parameter is set to **Defined** |  |  |  |  |  |  |
| Layer Height | Determines the height of the cloud layer, in units. \| ![](layer_h_100.png) \| ![](layer_h_500.png) \| \|---\|---\| \| *Layer Height = 100* \| *Layer Height = 500* \| | ![](layer_h_100.png) | ![](layer_h_500.png) | *Layer Height = 100* | *Layer Height = 500* |  |  |
| ![](layer_h_100.png) | ![](layer_h_500.png) |  |  |  |  |  |  |
| *Layer Height = 100* | *Layer Height = 500* |  |  |  |  |  |  |
| Clouds Shape Type | Defines how the shape of the clouds is determined: - **Coverage Texture** - the shape of the clouds is defined by the built-in [coverage texture](#texture_coverage). - **3D Texture** - the shape of the clouds is defined by a custom [3D texture](#texture_3d) (can be used to create a cloud of a specific predefined shape). > **Notice:** Changing the value of this parameter toggles the set of available parameters in this group and in the [Geometry](#geometry_group) group as well, it also determines whether the [Geometry](#geometry_group) group is to be displayed. |  |  |  |  |  |  |
| > **Notice:** The following four options are available when the [Clouds Shape Type](#clouds_shape_type) is set to **Coverage Texture**. |  |  |  |  |  |  |  |
| Clouds Coverage | An **RGB8** texture with the following channels: \| ![](texture_r.png) \| Red channel stores a coverage map. It determines cloud density in a horizontal plane. > **Notice:** For a number of tuning options to work correctly, this map should not contain absolutely black pixels. \| \|---\|---\| \| ![](texture_g.png) \| Green channel stores a stormcloud map. It determines areas of the coverage map, where storm clouds are located. \| \| ![](texture_b.png) \| Blue channel stores a height map. It determines cloud height for each point of the coverage map. > **Notice:** Absolutely black color does not correspond to an absolutely flat cloud, it determines a minimum possible cloud thickness for a certain configuration. \| | ![](texture_r.png) | Red channel stores a coverage map. It determines cloud density in a horizontal plane. > **Notice:** For a number of tuning options to work correctly, this map should not contain absolutely black pixels. | ![](texture_g.png) | Green channel stores a stormcloud map. It determines areas of the coverage map, where storm clouds are located. | ![](texture_b.png) | Blue channel stores a height map. It determines cloud height for each point of the coverage map. > **Notice:** Absolutely black color does not correspond to an absolutely flat cloud, it determines a minimum possible cloud thickness for a certain configuration. |
| ![](texture_r.png) | Red channel stores a coverage map. It determines cloud density in a horizontal plane. > **Notice:** For a number of tuning options to work correctly, this map should not contain absolutely black pixels. |  |  |  |  |  |  |
| ![](texture_g.png) | Green channel stores a stormcloud map. It determines areas of the coverage map, where storm clouds are located. |  |  |  |  |  |  |
| ![](texture_b.png) | Blue channel stores a height map. It determines cloud height for each point of the coverage map. > **Notice:** Absolutely black color does not correspond to an absolutely flat cloud, it determines a minimum possible cloud thickness for a certain configuration. |  |  |  |  |  |  |
| Clouds Region Mask | A separate single-channel texture to be used to define areas for the layer where the clouds are to be rendered and where they shouldn't (for regional weather). This texture is stretched to fit the region without any tiling. > **Notice:** This parameter is available when the [Clouds Layer Type](#clouds_shape_type) is set to **Defined** |  |  |  |  |  |  |
| Use Coverage Alpha | Use the Alpha-channel of the coverage texture as a mask for rendering coverage of the cloud layer. You can use this mask to define areas for the layer where the clouds are to be rendered and where they shouldn't. It serves to reduce tiling of the clouds coverage. You can also use it to make the borders of the layer smoother (for regional weather) or to reduce tiling for infinite cloud layers. > **Notice:** This option enables the [Alpha Size](#alpha_size) parameter in the *Geometry* group |  |  |  |  |  |  |
| Fix Coverage Tiling | Determines if reduction of tiling for the clouds coverage texture is enabled. Such tiling becomes noticeable in large-scale worlds when observing clouds at significant distances. It is recommended to enable this state only when the unwanted effect appears. Please use it wisely, as additional texture fetching affects performance. By default the state is disabled. ![](fix_tiling_off.jpg) ![](fix_tiling_on.jpg) |  |  |  |  |  |  |
| > **Notice:** The following two options are available when the [Clouds Shape Type](#clouds_shape_type) is set to **3D Texture**. |  |  |  |  |  |  |  |
| Clouds 3D Texture | 3D texture defining a custom shape of clouds for the layer. > **Notice:** An additional single-channel map is to be used for shadows (see the [Clouds Shadow Texture](#texture_shadow) below). |  |  |  |  |  |  |
| Clouds Shadow Texture | A separate single-channel texture to be used to define a custom shape for the shadows from the cloud layer defined by a custom 3D texture. In case of using the [coverage texture](#texture_coverage) shadows are defined by its **Red**-channel. A 3D texture does not contain such information and thus requires an additional map for shadows. |  |  |  |  |  |  |
| FieldWeather Mask | [Bitmask](../../../../principles/bit_masking/index.md) that determines interaction with [FieldWeather](../../../../objects/effects/fields/field_weather/index.md) objects. |  |  |  |  |  |  |


## Geometry


![Geometry Group](geometry_group.png)


| Coverage Size | Determines the size of the coverage texture. \| ![](cover_size_03.png) \| ![](cover_size_1.png) \| \|---\|---\| \| *Coverage Size = 0.3* \| *Coverage Size = 1* \| | ![](cover_size_03.png) | ![](cover_size_1.png) | *Coverage Size = 0.3* | *Coverage Size = 1* |
|---|---|---|---|---|---|
| ![](cover_size_03.png) | ![](cover_size_1.png) |  |  |  |  |
| *Coverage Size = 0.3* | *Coverage Size = 1* |  |  |  |  |
| Alpha Size | Controls tiling of the map stored in the alpha-channel of the *[Coverage](#texture_coverage)* texture. |  |  |  |  |
| Coverage Contrast Type | Determines the way the [**Coverage Contrast**](#coverage_contrast) parameter is controlled: - **Const** - control the parameter via a slider (the value is constant along the layer height) - **Curve** - control the parameter via a [2d curve](../../../../editor2/curve_editor/index.md) (the value changes along the layer height according to the curve) |  |  |  |  |
| Coverage Contrast | This parameter determines the contrast of the [coverage texture](#texture_coverage) and can be used for fine tuning. It also makes it possible to gradually increase cloudiness without changing the coverage texture when simulating weather. The lower the value the more cloudy the sky looks. > **Notice:** For this parameter to work properly, the coverage texture must not contain absolutely black pixels. \| ![](cover_cont_02.png) \| ![](cover_cont_1.png) \| \|---\|---\| \| *Coverage Contrast = 0.3* \| *Coverage Contrast = 1* \| | ![](cover_cont_02.png) | ![](cover_cont_1.png) | *Coverage Contrast = 0.3* | *Coverage Contrast = 1* |
| ![](cover_cont_02.png) | ![](cover_cont_1.png) |  |  |  |  |
| *Coverage Contrast = 0.3* | *Coverage Contrast = 1* |  |  |  |  |
| Coverage Height Remap | Remaps height values stored in the Blue-channel of the [coverage texture](#texture_coverage) (spreads them up vertically along layer height). This parameter can be used to tune the heightmap of the cloud layer without editing the coverage texture in a third-party software. |  |  |  |  |
| > **Notice:** The following three options are available when the [Clouds Shape Type](#clouds_shape_type) is set to **3D Texture**. |  |  |  |  |  |
| 3D Texture Threshold Type | Determines the way the [**3D Texture Threshold**](#texture_3d_threshold) parameter is controlled: - **Const** - control the parameter via a slider (the value is constant along the layer height) - **Curve** - control the parameter via a [2d curve](../../../../editor2/curve_editor/index.md) (the value changes along the layer height according to the curve) |  |  |  |  |
| 3D Texture Threshold | Threshold to be used for the values stored in the [3D texture](#texture_3d). |  |  |  |  |
| 3D Texture Threshold Extent | Threshold extent coefficient to be used for the values stored in the [3D texture](#texture_3d). |  |  |  |  |
| Bottom Fade | Determines the form of clouds bottom. Lower values make the bottom more flat. \| ![](bottom_fade_0.png) \| ![](bottom_fade_05.png) \| \|---\|---\| \| *Bottom Fade = 0* \| *Bottom Fade = 0.5* \| | ![](bottom_fade_0.png) | ![](bottom_fade_05.png) | *Bottom Fade = 0* | *Bottom Fade = 0.5* |
| ![](bottom_fade_0.png) | ![](bottom_fade_05.png) |  |  |  |  |
| *Bottom Fade = 0* | *Bottom Fade = 0.5* |  |  |  |  |
| Clouds Density Type | Determines the way the [**Clouds Density**](#cloud_density) parameter is controlled: - **Const** - control the parameter via a slider (the value is constant along the layer height) - **Curve** - control the parameter via a [2d curve](../../../../editor2/curve_editor/index.md) (the value changes along the layer height according to the curve) |  |  |  |  |
| Clouds Density | Controls density of the clouds which determines visual appearance. This parameter can be used to simulate cirrus clouds. The default value is 1. > **Notice:** This parameter should only be used when the desired visual appearance cannot be achieved using other parameters. The higher is the cloud density, the higher is the performance. Lower density values can significally reduce performance. \| ![](cloud_density_02.png) \| ![](cloud_density_04.png) \| \|---\|---\| \| *Cloud Density = 0.2* \| *Cloud Density = 0.4* \| | ![](cloud_density_02.png) | ![](cloud_density_04.png) | *Cloud Density = 0.2* | *Cloud Density = 0.4* |
| ![](cloud_density_02.png) | ![](cloud_density_04.png) |  |  |  |  |
| *Cloud Density = 0.2* | *Cloud Density = 0.4* |  |  |  |  |
| Storm Cloud Factor | Intensity of storm clouds coverage that is stored in the Green channel of the [Clouds coverage texture](#texture_coverage). \| ![](storm_cloud_0.png) \| ![](storm_cloud_1.png) \| \|---\|---\| \| *Storm Cloud Factor = 0* \| *Storm Cloud Factor = 1* \| | ![](storm_cloud_0.png) | ![](storm_cloud_1.png) | *Storm Cloud Factor = 0* | *Storm Cloud Factor = 1* |
| ![](storm_cloud_0.png) | ![](storm_cloud_1.png) |  |  |  |  |
| *Storm Cloud Factor = 0* | *Storm Cloud Factor = 1* |  |  |  |  |


## Noise


![Noise Group](noise_group.png)


> **Notice:** This group is available only when the [Clouds Shape Type](#clouds_shape_type) is set to **Coverage Texture**.


| Noise Size | Determines noise graininess. The default value is 0.45. > **Notice:** Higher values reduce performance and may bring up the tiling issue. Recommended range of values is from 0.3 to 1 \| ![](noise_size_03.png) \| ![](noise_size_1.png) \| \|---\|---\| \| *Noise Size = 0.3* \| *Noise Size = 1* \| | ![](noise_size_03.png) | ![](noise_size_1.png) | *Noise Size = 0.3* | *Noise Size = 1* |
|---|---|---|---|---|---|
| ![](noise_size_03.png) | ![](noise_size_1.png) |  |  |  |  |
| *Noise Size = 0.3* | *Noise Size = 1* |  |  |  |  |
| Noise Threshold Type | Determines the way the [**Noise Threshold**](#noise_threshold) parameter is controlled: - **Const** - control the parameter via a slider (the value is constant along the layer height) - **Curve** - control the parameter via a [2d curve](../../../../editor2/curve_editor/index.md) (the value changes along the layer height according to the curve) |  |  |  |  |
| Noise Threshold | Determines the density threshold of cloud formation. The higher the value the rougher the clouds are. > **Notice:** This parameter should be used only for fine tuning. Significant changes made to this parameter may result in mismatch of cloud shapes and their shadows. \| ![](noise_threshold_007.png) \| ![](noise_threshold_0375.png) \| \|---\|---\| \| *Noise Threshold = 0.07* \| *Noise Threshold = 0.375* \| | ![](noise_threshold_007.png) | ![](noise_threshold_0375.png) | *Noise Threshold = 0.07* | *Noise Threshold = 0.375* |
| ![](noise_threshold_007.png) | ![](noise_threshold_0375.png) |  |  |  |  |
| *Noise Threshold = 0.07* | *Noise Threshold = 0.375* |  |  |  |  |
| Noise Threshold Extent | This parameter works together with [Noise Threshold](#noise_threshold) parameter and adjusts appearance of clouds making it possible to make clouds softer or rougher for a selected noise threshold. > **Notice:** This parameter should be used only for fine tuning. Significant changes made to this parameter may result in mismatch of cloud shapes and their shadows. \| ![](noise_threshold_ext_001.png) \| ![](noise_threshold_ext_02.png) \| \|---\|---\| \| *Noise Threshold Extent = 0.01* \| *Noise Threshold Extent = 0.2* \| | ![](noise_threshold_ext_001.png) | ![](noise_threshold_ext_02.png) | *Noise Threshold Extent = 0.01* | *Noise Threshold Extent = 0.2* |
| ![](noise_threshold_ext_001.png) | ![](noise_threshold_ext_02.png) |  |  |  |  |
| *Noise Threshold Extent = 0.01* | *Noise Threshold Extent = 0.2* |  |  |  |  |
| Noise Mip Offset | Controls mip levels of the base noise texture in order to reduce blurring at large distances. The recommended range of values is from 0 to 3. Higher values reduce performance. |  |  |  |  |
| Noise Falloff | The shape of the clouds is defined by a 4-channel 3D noise texture (4 noise gradients are combined). This parameter enables you to control each noise gradient along the height of the layer via a separate curve. It can be used, for example, for fine-tuning of large clouds. |  |  |  |  |
| Fix Noise Tiling | Enable reduction of tiling caused by the 3D noise, noticeable in large-scale worlds when the clouds are dense. It is recommended to enable this state only when the unwanted effect appears. Please use it wisely, as additional texture fetching affects performance. By default the state is disabled. |  |  |  |  |


## Extra Noise


![Extra Noise Group](extra_noise_group.png)


Use extra noise for cloud formation. This noise controls cutting out fragments of clouds in less dense areas to add more cloud shape variations. You can use this extra noise when the base form and details are insufficient and you need more variations (e.g. for a cloud layer defined by a [3D texture](#texture_3d)).


| Extra Noise Intensity | Intensity of the extra noise used for cloud formation (it controls cutting out fragments of clouds in less dense areas to add more cloud shape variations): *higher* values result in less dense clouds (more cloud volume is cut out). |  |  |  |  |
|---|---|---|---|---|---|
| Extra Noise Size | Determines noise graininess. The default value is 0.45. > **Notice:** Higher values reduce performance and may bring up the tiling issue. Recommended range of values is from 0.3 to 1 \| ![](noise_size_03.png) \| ![](noise_size_1.png) \| \|---\|---\| \| *Extra Noise Size = 0.3* \| *Extra Noise Size = 1* \| | ![](noise_size_03.png) | ![](noise_size_1.png) | *Extra Noise Size = 0.3* | *Extra Noise Size = 1* |
| ![](noise_size_03.png) | ![](noise_size_1.png) |  |  |  |  |
| *Extra Noise Size = 0.3* | *Extra Noise Size = 1* |  |  |  |  |
| Extra Noise Threshold Type | Determines the way the [**Extra Noise Threshold**](#extra_noise_threshold) parameter is controlled: - **Const** - control the parameter via a slider (the value is constant along the layer height) - **Curve** - control the parameter via a [2d curve](../../../../editor2/curve_editor/index.md) (the value changes along the layer height according to the curve) |  |  |  |  |
| Extra Noise Threshold | Determines the density threshold of cloud formation. The higher the value the rougher the clouds are. > **Notice:** This parameter should be used only for fine tuning. Significant changes made to this parameter may result in mismatch of cloud shapes and their shadows. \| ![](noise_threshold_007.png) \| ![](noise_threshold_0375.png) \| \|---\|---\| \| *Noise Threshold = 0.07* \| *Noise Threshold = 0.375* \| | ![](noise_threshold_007.png) | ![](noise_threshold_0375.png) | *Noise Threshold = 0.07* | *Noise Threshold = 0.375* |
| ![](noise_threshold_007.png) | ![](noise_threshold_0375.png) |  |  |  |  |
| *Noise Threshold = 0.07* | *Noise Threshold = 0.375* |  |  |  |  |
| Extra Noise Threshold Extent | This parameter works together with [Noise Threshold](#noise_threshold) parameter and adjusts appearance of clouds making it possible to make clouds softer or rougher for a selected noise threshold. > **Notice:** This parameter should be used only for fine tuning. Significant changes made to this parameter may result in mismatch of cloud shapes and their shadows. \| ![](noise_threshold_ext_001.png) \| ![](noise_threshold_ext_02.png) \| \|---\|---\| \| *Noise Threshold Extent = 0.01* \| *Noise Threshold Extent = 0.2* \| | ![](noise_threshold_ext_001.png) | ![](noise_threshold_ext_02.png) | *Noise Threshold Extent = 0.01* | *Noise Threshold Extent = 0.2* |
| ![](noise_threshold_ext_001.png) | ![](noise_threshold_ext_02.png) |  |  |  |  |
| *Noise Threshold Extent = 0.01* | *Noise Threshold Extent = 0.2* |  |  |  |  |
| Extra Noise Mip Offset | Controls mip levels of the extra noise texture in order to reduce blurring at large distances. The recommended range of values is from 0 to 3. Higher values reduce performance. |  |  |  |  |
| Extra Noise Falloff | The shape of the clouds is defined by a 4-channel 3D noise texture (4 noise gradients are combined). This parameter enables you to control each noise gradient along the height of the layer via a separate curve. It can be used, for example, for fine-tuning of large clouds. |  |  |  |  |


## Detail


![Detail Group](detail_group.png)


| Detail Intensity Type | Determines the way the [**Detail Intensity**](#detail_intensity) parameter is controlled: - **Const** - control the parameter via a slider (the value is constant along the layer height) - **Curve** - control the parameter via a [2d curve](../../../../editor2/curve_editor/index.md) (the value changes along the layer height according to the curve) |  |  |  |  |
|---|---|---|---|---|---|
| Detail Intensity | Adjusts detail cutout intensity. Details are cut mostly from the bottom of the clouds. > **Notice:** Thunderclouds are dense and do not have detail cutout. Therefore, they have detail intensity value equal to 0. \| ![](detail_intensity_08.png) \| ![](detail_intensity_14.png) \| \|---\|---\| \| *Detail Intensity = 0.8* \| *Detail Intensity = 1.4* \| | ![](detail_intensity_08.png) | ![](detail_intensity_14.png) | *Detail Intensity = 0.8* | *Detail Intensity = 1.4* |
| ![](detail_intensity_08.png) | ![](detail_intensity_14.png) |  |  |  |  |
| *Detail Intensity = 0.8* | *Detail Intensity = 1.4* |  |  |  |  |
| Detail Noise Size | Determines the size of details cutout from the clouds. This parameter is analogous to the [Noise size](#noise_size) parameter. The lower is the value the larger pieces are cutout. \| [![](detail_noise_size_001_sm.png)](detail_noise_size_001.png) \| [![](detail_noise_size_5_sm.png)](detail_noise_size_5.png) \| \|---\|---\| \| *Detail Noise Size = 0.01* \| *Detail Noise Size = 5* \| | [![](detail_noise_size_001_sm.png)](detail_noise_size_001.png) | [![](detail_noise_size_5_sm.png)](detail_noise_size_5.png) | *Detail Noise Size = 0.01* | *Detail Noise Size = 5* |
| [![](detail_noise_size_001_sm.png)](detail_noise_size_001.png) | [![](detail_noise_size_5_sm.png)](detail_noise_size_5.png) |  |  |  |  |
| *Detail Noise Size = 0.01* | *Detail Noise Size = 5* |  |  |  |  |
| Detail Distortion Intensity | Determines the intensity of clouds detail distortion. This parameter is used to control detail turbulence. The higher is the value the stronger is the detail turbulence effect. \| ![](detail_distortion_force_05.png) \| ![](detail_distortion_force_4.png) \| \|---\|---\| \| *Detail Distortion Intensity = 0.5* \| *Detail Distortion Intensity = 4* \| | ![](detail_distortion_force_05.png) | ![](detail_distortion_force_4.png) | *Detail Distortion Intensity = 0.5* | *Detail Distortion Intensity = 4* |
| ![](detail_distortion_force_05.png) | ![](detail_distortion_force_4.png) |  |  |  |  |
| *Detail Distortion Intensity = 0.5* | *Detail Distortion Intensity = 4* |  |  |  |  |
| Detail Distortion Size | Determines the scale of clouds detail distortion according to the corresponding texture. This parameter is used to control detail turbulence. The higher is the value the stronger is the detail turbulence effect. \| [![](detail_distortion_size_0_sm.png)](detail_distortion_size_0.png) \| [![](detail_distortion_size_10_sm.png)](detail_distortion_size_10.png) \| \|---\|---\| \| *Detail Distortion Size = 0* \| *Detail Distortion Size = 10* \| | [![](detail_distortion_size_0_sm.png)](detail_distortion_size_0.png) | [![](detail_distortion_size_10_sm.png)](detail_distortion_size_10.png) | *Detail Distortion Size = 0* | *Detail Distortion Size = 10* |
| [![](detail_distortion_size_0_sm.png)](detail_distortion_size_0.png) | [![](detail_distortion_size_10_sm.png)](detail_distortion_size_10.png) |  |  |  |  |
| *Detail Distortion Size = 0* | *Detail Distortion Size = 10* |  |  |  |  |
| Detail Wispy Billowy Gradient | Controls the inversion of detail noise. With the default value of 0, the clouds form is as in the detail texture, increasing the value gradually inverts the values from wispy to billowy and from billowy to wispy. ![](wispy_billowy_0.png) ![](wispy_billowy_02.png) |  |  |  |  |


## Distortion


![Distorion Group](distortion_group.png)


| Distortion Intensity | Intensity of distortion of the clouds shape based on the curl noise. |
|---|---|
| Distortion Size | Scaling factor for distortion of the clouds shape based on the curl noise. |
| Wind Skew Intensity | Defines intensity of cloud shape distortion in the direction of the [wind](#wind_group) (by default higher portions of clouds are affected more than the lower ones). |
| Wind Skew Height Gradient | Defines which portion of the cloud layer height is affected by the wind skew distortion ([**Wind Skew Intensity**](#wind_skew_intensity) parameter above). The value sets the height level starting from which the cloud shape shall be affected by the skew distortion (e.g. **0.5** - means the middle of the layer). |


## Shading


![Shading Group](shading_group.png)


| Self Shadows | This state determines if a cloud layer casts shadows on itself. By default the state is enabled. \| ![](self_shad_en.png) \| ![](self_shad_dis.png) \| \|---\|---\| \| *Self Shadows enabled.* \| *Self Shadows disabled.* \| | ![](self_shad_en.png) | ![](self_shad_dis.png) | *Self Shadows enabled.* | *Self Shadows disabled.* |
|---|---|---|---|---|---|
| ![](self_shad_en.png) | ![](self_shad_dis.png) |  |  |  |  |
| *Self Shadows enabled.* | *Self Shadows disabled.* |  |  |  |  |
| Sun Color By Depth | Color of lighting from the sun depending on how deep the light goes through the cloud. - **Horizontal axis** - light penetration depth. - **Vertical axis** - RGB channel values. |  |  |  |  |
| Anisotropy By Density | Higher anisotropy values result in more light passing through the clouds without being scattered in various directions. The higher is the value the brighter the cloud will be when we look at the sun and the darker it will be when being looked at in the direction of the sun rays (from the sun). - **Horizontal axis** - cloud density. - **Vertical axis** - anisotropy values. |  |  |  |  |
| Ambient Color By Density | Color multiplier for ambient lighting depending on the cloud density. - **Horizontal axis** - cloud density. - **Vertical axis** - RGB channel values for ambient lighting color, Alpha - ambient lighting color saturation. |  |  |  |  |
| Ambient Occlusion By Coverage | Color multiplier for ambient lighting depending on the brightness of the [Coverage texture](#texture_coverage). - **Horizontal axis** - Coverage texture value. - **Vertical axis** - RGB channel values for Ambient Occlusion, Alpha - lighting color saturation. |  |  |  |  |
| Ambient Occlusion By Coverage Falloff | Intensity gradient for the impact of the [Ambient Occlusion By Coverage](#ambient_occlusion_by_coverage) effect along the height of the cloud. Usually used to avoid darkening of ambient lighting at the top of the clouds. - **Horizontal axis** - height of the cloud from the lowest point at the bottom to the highest point at the top. - **Vertical axis** - RGB channel values for the impact of the [Ambient Occlusion By Coverage](#ambient_occlusion_by_coverage) effect. |  |  |  |  |
| Sun Intensity | Determines intensity of the sun light affecting the clouds (from above). The higher is the value, the more sun lighting affects clouds. This parameter makes it possible to adjust the appearance of clouds by means of correction of sunlight intensity. > **Notice:** Areas lighted by the sun do not have environment lighting. \| ![](sun_int_0.png) \| ![](sun_int_1.png) \| \|---\|---\| \| *Sun intensity = 0* \| *Sun intensity = 1* \| | ![](sun_int_0.png) | ![](sun_int_1.png) | *Sun intensity = 0* | *Sun intensity = 1* |
| ![](sun_int_0.png) | ![](sun_int_1.png) |  |  |  |  |
| *Sun intensity = 0* | *Sun intensity = 1* |  |  |  |  |
| Sun Attenuation | Controls the amount of sun light passing through clouds without changing their density. The higher the value the less light passes through clouds. ![](sun_attenuation_2.png) ![](sun_attenuation_5.png) |  |  |  |  |
| Sun Saturation | Determines the saturation of the sun light affecting the clouds. ![](sun_saturation_05.png) ![](sun_saturation_08.png) |  |  |  |  |
| Ambient Intensity Top | Determines intensity of ambient lighting of clouds (lighting from above). Analogous to the previous parameter. The higher is the value, the more ambient lighting affects clouds. |  |  |  |  |
| Ambient Intensity Bottom | Determines intensity of ambient lighting of clouds (lighting from below). The higher is the value, the more ambient lighting affects clouds. \| ![](ambient_int_0.png) \| ![](ambient_int_1.png) \| \|---\|---\| \| *Ambient Intensity = 0 (Ground color set toff0000)* \| *Ambient Intensity = 1 (Ground color set toff0000)* \| | ![](ambient_int_0.png) | ![](ambient_int_1.png) | *Ambient Intensity = 0 (Ground color set toff0000)* | *Ambient Intensity = 1 (Ground color set toff0000)* |
| ![](ambient_int_0.png) | ![](ambient_int_1.png) |  |  |  |  |
| *Ambient Intensity = 0 (Ground color set toff0000)* | *Ambient Intensity = 1 (Ground color set toff0000)* |  |  |  |  |
| Ambient Saturation | Controls ambient lighting color saturation. \| ![](ambient_saturation_1.png) \| ![](ambient_saturation_2.png) \| \|---\|---\| \| *Ambient Saturation = 0.0* \| *Ambient Saturation = 1.0* \| | ![](ambient_saturation_1.png) | ![](ambient_saturation_2.png) | *Ambient Saturation = 0.0* | *Ambient Saturation = 1.0* |
| ![](ambient_saturation_1.png) | ![](ambient_saturation_2.png) |  |  |  |  |
| *Ambient Saturation = 0.0* | *Ambient Saturation = 1.0* |  |  |  |  |
| Multiscattering Intensity | Controls the approximation of light scattering in clouds. A view-dependent effect is created to control shadows on clouds: when clouds are looked on against the sun, shadows are more intensive compared to the side view. ![](multiscattering_intensity_0.png) ![](multiscattering_intensity_1.png) |  |  |  |  |
| Attenuation Coefficient | Controls the rate of opacity growth (alpha channel) with the distance inside the cloud, imitating cloud volume and fixing a break at a certain height appearing in the process of rendering curved cloud layers when viewed from inside the layer. ![](clouds_attenuation_low.png) ![](clouds_attenuation_high.png) |  |  |  |  |
| Haze Gradient | Controls the degree of gradual fading of the clouds to the haze depending on the [**haze parameters**](../../../../editor2/settings/render_settings/environment/index.md#haze). \| ![](haze_gradient_1.png) \| ![](haze_gradient_2.png) \| \|---\|---\| \| *Haze Gradient = 0.0* \| *Haze Gradient = 4.0* \| | ![](haze_gradient_1.png) | ![](haze_gradient_2.png) | *Haze Gradient = 0.0* | *Haze Gradient = 4.0* |
| ![](haze_gradient_1.png) | ![](haze_gradient_2.png) |  |  |  |  |
| *Haze Gradient = 0.0* | *Haze Gradient = 4.0* |  |  |  |  |


## Shadows


![Shadows Group](shadows_group.png)


| Receive Shadows | This state determines if shadows from an upper cloud layer can be cast on this cloud layer. By default the state is disabled. \| ![](receive_shad_en.png) \| ![](receive_shad_dis.png) \| \|---\|---\| \| *Receive Shadows enabled.* \| *Receive Shadows disabled.* \| | ![](receive_shad_en.png) | ![](receive_shad_dis.png) | *Receive Shadows enabled.* | *Receive Shadows disabled.* |
|---|---|---|---|---|---|
| ![](receive_shad_en.png) | ![](receive_shad_dis.png) |  |  |  |  |
| *Receive Shadows enabled.* | *Receive Shadows disabled.* |  |  |  |  |
| Cast Shadows | This state determines if a cloud layer casts shadows. By default the state is enabled. \| ![](cast_shad_en.png) \| ![](cast_shad_dis.png) \| \|---\|---\| \| *Cast Shadows enabled.* \| *Cast Shadows disabled.* \| | ![](cast_shad_en.png) | ![](cast_shad_dis.png) | *Cast Shadows enabled.* | *Cast Shadows disabled.* |
| ![](cast_shad_en.png) | ![](cast_shad_dis.png) |  |  |  |  |
| *Cast Shadows enabled.* | *Cast Shadows disabled.* |  |  |  |  |
| Shadow Intensity | Determines the intensity of shadows cast by clouds. This parameter is used for synchronization of visual appearance of clouds with their shadows. \| ![](shadow_intensity_08.png) \| ![](shadow_intensity_1.png) \| \|---\|---\| \| *Shadow intensity = 0.8* \| *Shadow intensity = 1* \| | ![](shadow_intensity_08.png) | ![](shadow_intensity_1.png) | *Shadow intensity = 0.8* | *Shadow intensity = 1* |
| ![](shadow_intensity_08.png) | ![](shadow_intensity_1.png) |  |  |  |  |
| *Shadow intensity = 0.8* | *Shadow intensity = 1* |  |  |  |  |
| Shadow Contrast | Determines the contrast of shadows cast by clouds. \| ![](shadow_contrast_0.png) \| ![](shadow_contrast_1.png) \| \|---\|---\| \| *Shadow contrast = 0.3* \| *Shadow contrast = 1.0* \| | ![](shadow_contrast_0.png) | ![](shadow_contrast_1.png) | *Shadow contrast = 0.3* | *Shadow contrast = 1.0* |
| ![](shadow_contrast_0.png) | ![](shadow_contrast_1.png) |  |  |  |  |
| *Shadow contrast = 0.3* | *Shadow contrast = 1.0* |  |  |  |  |
| Shadow Multiplier | Determines darkness of shadows cast by clouds. The *lower* the value, the darker the shadows are. \| ![](shadow_multiplier_0.png) \| ![](shadow_multiplier_1.png) \| \|---\|---\| \| *Shadow multiplier = 0.3* \| *Shadow multiplier = 1.0* \| | ![](shadow_multiplier_0.png) | ![](shadow_multiplier_1.png) | *Shadow multiplier = 0.3* | *Shadow multiplier = 1.0* |
| ![](shadow_multiplier_0.png) | ![](shadow_multiplier_1.png) |  |  |  |  |
| *Shadow multiplier = 0.3* | *Shadow multiplier = 1.0* |  |  |  |  |
| Shadow Subtraction | The higher the value, the larger the area under clouds is covered by the shadow. Decreasing the value causes shadows from clouds to be subtracted from the shadow that covers the area under the clouds. The parameter can be set to the maximum value, for example, when the shadow cast by the clouds doesn't fully cover the area beneath, however, clouds look dense enough. \| ![](shadow_subtraction_0.png) \| ![](shadow_subtraction_1.png) \| \|---\|---\| \| *Shadow subtraction = 0.2* \| *Shadow subtraction = 0.4* \| | ![](shadow_subtraction_0.png) | ![](shadow_subtraction_1.png) | *Shadow subtraction = 0.2* | *Shadow subtraction = 0.4* |
| ![](shadow_subtraction_0.png) | ![](shadow_subtraction_1.png) |  |  |  |  |
| *Shadow subtraction = 0.2* | *Shadow subtraction = 0.4* |  |  |  |  |


## Wind


![Wind Group](wind_group.png)


| Wind speed (X axis) | Wind speed along **X** axis (shifts the coverage texture). |  |  |  |  |
|---|---|---|---|---|---|
| Wind speed (Y axis) | Wind speed along **Y** axis (shifts the coverage texture). \| ![](wind_0.png) \| ![](wind_20.gif) \| \|---\|---\| \| *No wind* \| *Wind X = 20, Wind Y = 20* \| | ![](wind_0.png) | ![](wind_20.gif) | *No wind* | *Wind X = 20, Wind Y = 20* |
| ![](wind_0.png) | ![](wind_20.gif) |  |  |  |  |
| *No wind* | *Wind X = 20, Wind Y = 20* |  |  |  |  |
| Wind speed (Z axis) | Wind speed along **Z** axis (shifts noise). \| ![](windz_0.png) \| ![](windz_100.gif) \| \|---\|---\| \| *No wind* \| *Wind Z = 100* \| | ![](windz_0.png) | ![](windz_100.gif) | *No wind* | *Wind Z = 100* |
| ![](windz_0.png) | ![](windz_100.gif) |  |  |  |  |
| *No wind* | *Wind Z = 100* |  |  |  |  |
| Wind Deformation | Control dynamics of moving clouds, i.e. how much clouds change their form as they move. |  |  |  |  |


## Textures


![Textures](textures.png)

*Material Editor,Texturestab.*
