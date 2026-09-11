# water_mesh_base


The *water_mesh_base* material simulates [water](../../../../objects/objects/water/index.md) and other liquids and is applied to the [Water Mesh](../../../../objects/objects/water/water_mesh.md) object.

 Prior Knowledge
This article assumes you have prior knowledge of the following topics:


- [Materials Settings](../../../../editor2/materials_settings/index.md)
- [*mesh_base* material states, textures, parameters](../../../../content/materials/library/mesh_base/index.md)


![](index.png)


## Parameters


### Common


![](params_default.png)


| FieldSpacer Interaction | Enables the effect of [FieldSpacer object](../../../../objects/effects/fields/field_spacer/index.md) on the Water Mesh object. |
|---|---|
| Material Mask | The [material bit mask](../../../../principles/bit_masking/index.md#material_mask). The decal can be projected onto the water surface only if the material mask of the decal material matches this mask. |


### Detail


![](params_detail.png)


Waves for the **water_mesh** material are created by using the [Normal Detail](#texture_normal_detail) map. The engine performs sampling from the map and creates ripples using several detail layers.


There are two base detail layers (Detail 0 and 1), additional ripples (Detail 2-4) are enabled by toggling on the [Additional Details](#state_additional_details) parameter.


| Additional Details | \| Provides additional detail layers for more detailed ripple effect. \|  \| \|---\|---\| \| ![](additional_details_0.png) \| ![](additional_details_1.png) \| \| *Additional Details state disabled.* \| *Additional Details state enabled.* \| | Provides additional detail layers for more detailed ripple effect. | ![](additional_details_0.png) | ![](additional_details_1.png) | *Additional Details state disabled.* | *Additional Details state enabled.* |
|---|---|---|---|---|---|---|
| Provides additional detail layers for more detailed ripple effect. |  |  |  |  |  |  |
| ![](additional_details_0.png) | ![](additional_details_1.png) |  |  |  |  |  |
| *Additional Details state disabled.* | *Additional Details state enabled.* |  |  |  |  |  |
| Normal Map | The **Normal Detail** map stores normal information required to achieve an additional (detail) effect of Normal Mapping. Normal map helps to create ripples (cat's-paw effect) on the water surface. The texture is 2-channeled: - *RG* values store two components of a surface normal. - *B* value is calculated based on the *R* and *G* values in run-time. \| ![](texture_n_0.png) \| ![](texture_n_1.png) \| \|---\|---\| \| *With absolutely white normal map* \| *With ripple-simulated normal map* \| > **Notice:** **UNIGINE Engine** expects a normal map in *DirectX* format. If your normal map is in *OpenGL* format, tick *[Invert G Channel](../../../../editor2/assets_workflow/texture_import.md#invert_g)* in the import menu. As a general rule, if the lighting seems weird, try inverting the G Channel and see if it gets better. | ![](texture_n_0.png) | ![](texture_n_1.png) | *With absolutely white normal map* | *With ripple-simulated normal map* |  |
| ![](texture_n_0.png) | ![](texture_n_1.png) |  |  |  |  |  |
| *With absolutely white normal map* | *With ripple-simulated normal map* |  |  |  |  |  |
| Detail UV Transform | This parameter specifies the [transformation](../../../../content/materials/library/mesh_base/index.md#texture_transform) of the detail map sampling. The first two values are the scale texture coordinates along the X and Y axes. The third and forth specify the wind force and direction for the U and V axes. |  |  |  |  |  |
| Detail Intensity | This parameter sets the intensity of the sample of the detail normal map. |  |  |  |  |  |


### Foam


![](params_foam.png)


| Foam Texture | This texture specifies foam on water. The engine samples the foam texture twice to create plausibility of the real world foam behavior. The texture is 3-channeled: - *RGB* values store the color. |
|---|---|
| Patch 0 UV Size | Size of the first foam texture patch. |
| Patch 0 UV Speed | Speed of the first foam patch. |
| Patch 1 UV Size | Size of the second foam texture patch. |
| Patch 1 UV Speed | Speed of the second foam patch. |
| Contrast Foam Intensity | Foam intensity near shores or different objects in water. |
| Texture Affect | Visibility of the foam texture. It can be used to create additional effects, e.g., foam bubbles. |


### Subsurface Scattering Parameters


![](params_sss.png)


| Color | \| The water Subsurface Scattering (**SSS**) color. \|  \| \|---\|---\| \| ![](sss_color_0.png) \| ![](sss_color_1.png) \| \| ![](sss_color_param_0.png) \| ![](sss_color_param_1.png) \| | The water Subsurface Scattering (**SSS**) color. | ![](sss_color_0.png) | ![](sss_color_1.png) | ![](sss_color_param_0.png) | ![](sss_color_param_1.png) |
|---|---|---|---|---|---|---|
| The water Subsurface Scattering (**SSS**) color. |  |  |  |  |  |  |
| ![](sss_color_0.png) | ![](sss_color_1.png) |  |  |  |  |  |
| ![](sss_color_param_0.png) | ![](sss_color_param_1.png) |  |  |  |  |  |
| Ambient Intensity | \| Intensity of subsurface scattering for ambient lighting. The lower the value, the faster the light rays dissipate in water. \|  \| \|---\|---\| \| ![](ambient_intensity_0.png) \| ![](ambient_intensity_1.png) \| \| ![](ambient_intensity_param_0.png) \| ![](ambient_intensity_param_1.png) \| | Intensity of subsurface scattering for ambient lighting. The lower the value, the faster the light rays dissipate in water. | ![](ambient_intensity_0.png) | ![](ambient_intensity_1.png) | ![](ambient_intensity_param_0.png) | ![](ambient_intensity_param_1.png) |
| Intensity of subsurface scattering for ambient lighting. The lower the value, the faster the light rays dissipate in water. |  |  |  |  |  |  |
| ![](ambient_intensity_0.png) | ![](ambient_intensity_1.png) |  |  |  |  |  |
| ![](ambient_intensity_param_0.png) | ![](ambient_intensity_param_1.png) |  |  |  |  |  |
| Intensity Through Waves | \| Intensity of light rays passing through waves. The lower the value, the faster the light rays dissipate in water. \|  \| \|---\|---\| \| ![](intensity_tw_0.png) \| ![](intensity_tw_1.png) \| \| ![](intensity_tw_param_0.png) \| ![](intensity_tw_param_1.png) \| | Intensity of light rays passing through waves. The lower the value, the faster the light rays dissipate in water. | ![](intensity_tw_0.png) | ![](intensity_tw_1.png) | ![](intensity_tw_param_0.png) | ![](intensity_tw_param_1.png) |
| Intensity of light rays passing through waves. The lower the value, the faster the light rays dissipate in water. |  |  |  |  |  |  |
| ![](intensity_tw_0.png) | ![](intensity_tw_1.png) |  |  |  |  |  |
| ![](intensity_tw_param_0.png) | ![](intensity_tw_param_1.png) |  |  |  |  |  |
| Intensity Around Foam | \| Intensity of subsurface scattering near the foam areas. \|  \| \|---\|---\| \| ![](intensity_af_0.png) \| ![](intensity_af_1.png) \| \| ![](intensity_af_param_0.png) \| ![](intensity_af_param_1.png) \| | Intensity of subsurface scattering near the foam areas. | ![](intensity_af_0.png) | ![](intensity_af_1.png) | ![](intensity_af_param_0.png) | ![](intensity_af_param_1.png) |
| Intensity of subsurface scattering near the foam areas. |  |  |  |  |  |  |
| ![](intensity_af_0.png) | ![](intensity_af_1.png) |  |  |  |  |  |
| ![](intensity_af_param_0.png) | ![](intensity_af_param_1.png) |  |  |  |  |  |
| Diffuse Intensity | Intensity of subsurface scattering for diffuse lighting. |  |  |  |  |  |


### Underwater Parameters


![](params_underwater.png)


The Underwater parameters adjust the underwater part of the water_mesh_base material.


The final color of underwater is calculated using the following formula:


```text
FinalColor = FogColor * SunLighting^(1/FogSunLighting) + FogColor * EnvLighting^(1/FogEnvLighting)
```


*FogColor, FogSunLighting*, and *FogEnvLighting* are specified in the material. The other parameters (Sun and Environment lighting) are calculated according to the sun lighting and environment lighting of the scene. In fact, this formula defines how the sun and the environment lights affect the final underwater color.


| Depth LUT | LUT texture that shows the color of the bottom. Depending on the depth, the engine chooses the color of the water and multiplies it by the depth LUT texture. This generated LUT shows how deep the photon goes through water until completely scattered. The texture is 4-channeled: - *RGB* values store color. - *A* value is used to create "transparent" water near the shore. In other words, it defines the fog density. |  |  |  |  |
|---|---|---|---|---|---|
| Fog Color | The underwater fog color. The Sun and Environment lighting affect this parameter to create the final underwater fog color. \| ![](underwater_fog_color_0.png) \| ![](underwater_fog_color_1.png) \| \|---\|---\| \| ![](fog_color_param_0.png) \| ![](fog_color_param_1.png) \| | ![](underwater_fog_color_0.png) | ![](underwater_fog_color_1.png) | ![](fog_color_param_0.png) | ![](fog_color_param_1.png) |
| ![](underwater_fog_color_0.png) | ![](underwater_fog_color_1.png) |  |  |  |  |
| ![](fog_color_param_0.png) | ![](fog_color_param_1.png) |  |  |  |  |
| Fog Transparency | The transparency of the underwater fog. The higher the value, the more transparent the underwater fog is. \| ![](underwater_fog_transparency_0.png) \| ![](underwater_fog_transparency_1.png) \| \|---\|---\| \| *Fog Transparency: 5.0* \| *Fog Transparency: 30.0* \| | ![](underwater_fog_transparency_0.png) | ![](underwater_fog_transparency_1.png) | *Fog Transparency: 5.0* | *Fog Transparency: 30.0* |
| ![](underwater_fog_transparency_0.png) | ![](underwater_fog_transparency_1.png) |  |  |  |  |
| *Fog Transparency: 5.0* | *Fog Transparency: 30.0* |  |  |  |  |
| Fog Lighting Depth | The distance from the water surface, in units, up to which the light affects the underwater color. |  |  |  |  |
| Lighting Offset | Height offset for lighting. |  |  |  |  |
| Fog Environment Lighting | Degree of impact of the environment lighting on the final underwater color. |  |  |  |  |
| Fog Sun Lighting | Degree of impact of the sun lighting on the final underwater color. |  |  |  |  |
| Shafts Intensity | Intensity of the underwater sun shafts. |  |  |  |  |


### Planar Reflection


![](params_planar.png)


This set of parameters is enabled by toggling on the [Planar Reflection](#state_planar_reflection) option.


| Planar Reflection | If enabled, this option allows using planar reflections on the water surface instead of SSR. |
|---|---|
| Map Size | The size of the planar reflection map, in pixels: the higher the value, the better the quality is. Available sizes of the map are: - **128** � creates a reflection image with 128x128 resolution. - **256** � creates a reflection image with 256x256 resolution. - **512** � creates a reflection image with 512x512 resolution. - **1024** � creates a reflection image with 1024x1024 resolution. - **2048** � creates a reflection image with 2048x2048 resolution. - **4096** � creates a reflection image with 4096x4096 resolution. - **Quart height** � creates a reflection image with the resolution *height/4 x height/4*, where height is an application window height. - **Half height** � creates a reflection image with the resolution *height/2 x height/2*, where height is an application window height. - **Height** � creates a reflection image with the resolution *height x height*, where height is an application window height. |
| Show Pivot | Displays the pivot plane that shows the direction of reflective surface. By specifying the direction of planar reflection, you can create a reflection surface even if it was exported at an angle. |
| Viewport Mask | [Viewport mask](../../../../principles/bit_masking/index.md#viewport) of the reflection camera. |
| Distance | **Distance** from the reflection camera to the reflected object. In other words, the distance equals the distance from camera to the reflective surface plus the distance from object to reflective surface. ![](../mesh_base/planar_scheme.png) |
| Pivot Offset | **Pivot offset** specifies the position of the pivot point. > **Notice:** This parameter can be used to correct reflection if the transformation of reflective surface was changed. |
| Pivot Rotation | **Pivot Rotation** specifies the rotation of the reflection pivot point. > **Notice:** This parameter can be used to correct reflection if reflective surface was exported with a tilt angle or was rotated. |


### Reflection


![](params_reflection.png)


| Roughness | The environment reflection roughness of the water surface. This parameter helps to tweak reflections on the water surface relative to the environment. \| ![](env_reflection_0.png) \| ![](env_reflection_1.png) \| \|---\|---\| \| ![](env_reflection_param_0.png) \| ![](env_reflection_param_1.png) \| | ![](env_reflection_0.png) | ![](env_reflection_1.png) | ![](env_reflection_param_0.png) | ![](env_reflection_param_1.png) |
|---|---|---|---|---|---|
| ![](env_reflection_0.png) | ![](env_reflection_1.png) |  |  |  |  |
| ![](env_reflection_param_0.png) | ![](env_reflection_param_1.png) |  |  |  |  |
| Occlusion | The occlusion factor for environment reflections on parts of the water surface with negative normals. Using this parameter enables simulation of reflection of waves on the water surface removing too bright areas on waves close to the horizon. - By the minimum value of 0, no occlusion is performed for reflections of waves, no matter what normals the water surface has. - By the higher values, occlusion is performed for reflections on parts of the water surface with negative normals that have a certain [slope](#reflection_occlusion_slope). The higher the value, the less intensive reflections are on the surface parts with negative normals. \| ![](reflection_occlusion_0.png) ![](reflection_occlusion_1.png) \| \|---\| | ![](reflection_occlusion_0.png) ![](reflection_occlusion_1.png) |  |  |  |
| ![](reflection_occlusion_0.png) ![](reflection_occlusion_1.png) |  |  |  |  |  |
| Occlusion Slope | Slope of negative normals of the water surface, at which occlusion is performed for wave reflections. |  |  |  |  |


### Caustics


Caustics is the effect of light rays refraction by the water surface.


| ![](caustics_0.png) | ![](caustics_1.png) |
|---|---|
| *Caustics state disabled* | *Caustics state enabled* |


![](params_caustics.png)


| Caustics Distortion | Removes pixelation and makes caustics look smoother. When smoothing is not required, you can disable this option to gain performance. \| ![](caustics_distortion_0.png) \| ![](caustics_distortion_1.png) \| \|---\|---\| \| *Caustics Distortion state disabled* \| *Caustics Distortion state enabled* \| | ![](caustics_distortion_0.png) | ![](caustics_distortion_1.png) | *Caustics Distortion state disabled* | *Caustics Distortion state enabled* |
|---|---|---|---|---|---|
| ![](caustics_distortion_0.png) | ![](caustics_distortion_1.png) |  |  |  |  |
| *Caustics Distortion state disabled* | *Caustics Distortion state enabled* |  |  |  |  |
| Caustic Texture | The 3D **Caustic** texture determines the pattern of light rays refracted by the water surface. The texture is 1-channeled: - *R* value defines the caustics pattern. |  |  |  |  |
| UV Transform | UV Transform coordinates for the [caustic texture](#texture_caustics). \| ![](caustics_uv_0.png) \| ![](caustics_uv_1.png) \| \|---\|---\| \| ![](caustics_uv_param_0.png) \| ![](caustics_uv_param_1.png) \| | ![](caustics_uv_0.png) | ![](caustics_uv_1.png) | ![](caustics_uv_param_0.png) | ![](caustics_uv_param_1.png) |
| ![](caustics_uv_0.png) | ![](caustics_uv_1.png) |  |  |  |  |
| ![](caustics_uv_param_0.png) | ![](caustics_uv_param_1.png) |  |  |  |  |
| Distance Fade | Distance from the water surface downwards, at which light shapes fade, in units. \| ![](caustics_distance_fade_0.png) \| ![](caustics_distance_fade_1.png) \| \|---\|---\| \| *Distance Fade: 20.0* \| *Distance Fade: 40.0* \| | ![](caustics_distance_fade_0.png) | ![](caustics_distance_fade_1.png) | *Distance Fade: 20.0* | *Distance Fade: 40.0* |
| ![](caustics_distance_fade_0.png) | ![](caustics_distance_fade_1.png) |  |  |  |  |
| *Distance Fade: 20.0* | *Distance Fade: 40.0* |  |  |  |  |
| Animation Speed | Movement speed of the light patterns. |  |  |  |  |
| Brightness | Brightness of the light shapes. |  |  |  |  |


### Other


![](params_other.png)


| Waves Radius | Radius of waves on the water surface. |  |  |  |  |
|---|---|---|---|---|---|
| Refraction Scale | Scale of the water refraction. \| ![](refraction_scale_0.png) \| ![](refraction_scale_1.png) \| \|---\|---\| \| ![](refraction_scale_param_0.png) \| ![](refraction_scale_param_1.png) \| | ![](refraction_scale_0.png) | ![](refraction_scale_1.png) | ![](refraction_scale_param_0.png) | ![](refraction_scale_param_1.png) |
| ![](refraction_scale_0.png) | ![](refraction_scale_1.png) |  |  |  |  |
| ![](refraction_scale_param_0.png) | ![](refraction_scale_param_1.png) |  |  |  |  |
| Diffuse Distortion | Distortion of [decals](../../../../objects/decals/index.md) projected onto water. |  |  |  |  |
| Soft Intersection | Soft intersection of water with the shoreline and surfaces of objects. |  |  |  |  |


### Post Processing


Post processing effects available for the material:


- **DOF** � enables the depth of field effect.
- **Motion blur** � enables the motion blur effect.
