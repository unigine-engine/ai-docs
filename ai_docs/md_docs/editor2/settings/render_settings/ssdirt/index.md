# Screen Space Dirt


This section contains settings that control the *Screen-Space Dirt* effect.


Various slits and cavities are prone to accumulating dirt and dust, while edges tend to wear, scratch and change their initial color, usually this is simulated using so-called curvature maps prepared for each model.


Using this effect allows you to perform curvature mapping (simulate worn scratched edges and accumulation of dirt and dust in cavities) in the screen space for all objects globally. It saves time for large complex scenes with a lot of various models and elements making them look more natural without having to prepare textures for each of them individually.


## General Options


![](ssdirt.png)

*Screen-Space DirtSettings*


> **Notice:** Settings are applied to materials with the *Procedural Effects* and *Dirt* states enabled.


The *Screen-Space Dirt* effect uses additional geometry buffer (*Rendering -> Buffers -> Additional Features*). If the buffer is disabled, the effect won't be rendered.


| Enabled | The value indicating if the [Screen-Space Dirt](../../../../editor2/settings/render_settings/ssdirt/index.md) (SSDirt) effect is enabled. **disabled** by default. `Console access:render_ssdirt` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt)) ![](ssdirt_enabled_0.jpg) ![](ssdirt_enabled_1.jpg) |
|---|---|
| Quality | The [quality](../../../../editor2/settings/render_settings/ssdirt/index.md#quality) for the SSDirt effect. SSDirt*[SSDirt](#render_ssdirt)* must be enabled. Quality implies the number of samples used for the Screen-Space Dirt effect: - Low - 4 samples - Medium - 8 samples - High - 16 samples - Ultra - 32 samples > **Notice:** This parameter significantly affects performance, so choose it reasonably. Option **#3** is selected by default (see above). `Console access:render_ssdirt_quality` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_quality)) |
| Resolution | The [resolution](../../../../editor2/settings/render_settings/ssdirt/index.md#resolution) of the SSDirt effect. SSDirt*[SSDirt](#render_ssdirt)* must be enabled. > **Notice:** This parameter significantly affects performance, so choose it reasonably. One of the following values: - *Quarter* - quarter resolution - *Half* - half resolution (by default) - *Full* - full resolution `Console access:render_ssdirt_resolution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_resolution)) |
| Intensity | The [intensity](../../../../editor2/settings/render_settings/ssdirt/index.md#intensity) of the SSDirt effect. - By the minimum value of 0.0f, the effect is not visible. - *Higher* values make the effect more pronounced. SSDirt*[SSDirt](#render_ssdirt)* must be enabled. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_ssdirt_intensity` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_intensity)) ![](ssdirt_intensity_07.jpg) ![](ssdirt_intensity_22.jpg) |
| Radius | The [size](../../../../editor2/settings/render_settings/ssdirt/index.md#radius) of the SSDirt effect. SSDirt*[SSDirt](#render_ssdirt)* must be enabled. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_ssdirt_radius` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_radius)) |
| Threshold | The [threshold](../../../../editor2/settings/render_settings/ssdirt/index.md#threshold) of the SSDirt effect. It determines depth limit for the SSDirt effect in areas where information cannot be obtained. *Higher* values make the effect less pronounced. SSDirt*[SSDirt](#render_ssdirt)* must be enabled. Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**. `Console access:render_ssdirt_threshold` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_threshold)) |
| Angle Bias | The angle bias value to limit the [SSDirt](../../../../editor2/settings/render_settings/ssdirt/index.md) effect where information cannot be obtained. This parameter can be used to remove visual artefacts at the edges of polygons. SSDirt*[SSDirt](#render_ssdirt)* must be enabled. > **Notice:** This parameter affects both, concave and convex areas. Range of values: **[0.0f, 1.0f]**. The default value is : **0.35f**. `Console access:render_ssdirt_angle_bias` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_angle_bias)) |
| Perspective | The [perspective](../../../../editor2/settings/render_settings/ssdirt/index.md#perspective) value, that determines the degree of impact of distance from the camera on the radius of the Screen-Space Dirt effect. - 0.0f - radius of the effect is bound to screen space (it remains constant relative to screen size, regardless of the distance to the camera). - 1.0f - radius of the effect is bound to world space (it remains the same relative to objects, i.e. gets smaller as the camera moves away from them). SSDirt*[SSDirt](#render_ssdirt)* must be enabled. Range of values: **[0.0f, 1.0f]**. The default value is : **0.02f**. `Console access:render_ssdirt_perspective` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_perspective)) |
| Increase Accuracy | The value indicating if increased accuracy for the [SSDirt](../../../../editor2/settings/render_settings/ssdirt/index.md) effect. This option should be used to remove visual artefacts along the screen edges, in case if they appear. Otherwise, it should be disabled. SSDirt*[SSDirt](#render_ssdirt)* must be enabled. **disabled** by default. `Console access:render_ssdirt_increase_accuracy` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_increase_accuracy)) |


## Cavity Options


These options are used to control the look of pits and other cavity areas where dirt or dust would collect.


| Albedo | Albedo texture for cavities. This texture defines dirt and dust color pattern for all cavities globally. |
|---|---|
| Shading | Shading texture for cavities. *Red* channel of this texture defines metalness pattern for all cavities globally (other channels are ignored). |
| Texture Size | The scaling factor for the textures used for cavities. SSDirt*[SSDirt](#render_ssdirt)* must be enabled. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_ssdirt_cavity_texture_size` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_cavity_texture_size)) |
| Color | The [color multiplier](../../../../editor2/settings/render_settings/ssdirt/index.md#cavity_color) for the Albedo texture used for cavities (global dirt and dust color pattern). SSDirt*[SSDirt](#render_ssdirt)* must be enabled. **vec4(0.26f, 0.24f, 0.21f, 1.0f)** - default value `Console access:render_ssdirt_cavity_color` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_cavity_color)) ![](ssdirt_cavity_color_0.jpg) ![](ssdirt_cavity_color_1.jpg) |
| Exponent | The [exponent](../../../../editor2/settings/render_settings/ssdirt/index.md#cavity_exponent) value that determines the rate of gradual change of intensity along the radius for cavities. *Lower* values make gradual change of intensity smoother. SSDirt*[SSDirt](#render_ssdirt)* must be enabled. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_ssdirt_cavity_exponent` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_cavity_exponent)) ![](ssdirt_cavity_color_1.jpg) ![](ssdirt_cavity_exponent_19.jpg) |
| Metalness | The [metalness](../../../../editor2/settings/render_settings/ssdirt/index.md#cavity_metalness) value for cavities. When set to 0 (by default), the SSDirt effect does not modify metalness buffer in cavities. SSDirt*[SSDirt](#render_ssdirt)* must be enabled. Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**. `Console access:render_ssdirt_cavity_metalness` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_cavity_metalness)) |
| Metalness Visibility | The [metalness visibility](../../../../editor2/settings/render_settings/ssdirt/index.md#cavity_metalness_visibility) value for cavities. A multiplier that determines the degree of impact of the effect on metalness buffer (the *higher* the value the more metalness buffer is affected. SSDirt*[SSDirt](#render_ssdirt)* must be enabled. Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**. `Console access:render_ssdirt_cavity_metalness_visibility` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_cavity_metalness_visibility)) |


## Convexity Options


These options are used to control highlighting and accentuating the edges of model (simulating edge wear, scratches or chipped metal).


| Albedo | Albedo texture for convexities. This texture defines wear and scratch color pattern for all convexities globally. |
|---|---|
| Shading | Shading texture for convexities. *Red* channel of this texture defines metalness pattern for all convexities globally (other channels are ignored). |
| Texture Size | The scaling factor for the textures used for convexities. SSDirt*[SSDirt](#render_ssdirt)* must be enabled. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_ssdirt_convexity_texture_size` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_convexity_texture_size)) |
| Color | The [color multiplier](../../../../editor2/settings/render_settings/ssdirt/index.md#convexity_color) for the Albedo texture used for convexities (global wear and scratch color pattern). SSDirt*[SSDirt](#render_ssdirt)* must be enabled. **vec4(0.48f, 0.44f, 0.39f, 1.0f)** - default value `Console access:render_ssdirt_convexity_color` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_convexity_color)) |
| Exponent | The [exponent](../../../../editor2/settings/render_settings/ssdirt/index.md#convexity_exponent) value that determines the rate of gradual change of intensity along the radius for convexities. *Lower* values make gradual change of intensity smoother. SSDirt*[SSDirt](#render_ssdirt)* must be enabled. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_ssdirt_convexity_exponent` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_convexity_exponent)) |
| Metalness | The [metalness](../../../../editor2/settings/render_settings/ssdirt/index.md#convexity_metalness) value for convexities. When set to 0 (by default), the SSDirt effect does not modify metalness buffer in convex areas. SSDirt*[SSDirt](#render_ssdirt)* must be enabled. Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**. `Console access:render_ssdirt_convexity_metalness` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_convexity_metalness)) |
| Metalness Visibility | The [metalness visibility](../../../../editor2/settings/render_settings/ssdirt/index.md#convexity_metalness_visibility) value for convexities. A multiplier that determines the degree of impact of the effect on metalness buffer (the *higher* the value the more metalness buffer is affected. SSDirt*[SSDirt](#render_ssdirt)* must be enabled. Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**. `Console access:render_ssdirt_convexity_metalness_visibility` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssdirt_convexity_metalness_visibility)) |


## Adjusting the SSDirt Effect Per Material


Despite all major settings of the SSDirt effect are global and are adjusted via the Settings window, some parameters for fine tuning can be set up per material. The SSDirt effect is applied to all materials inherited from the **[mesh_base](../../../../content/materials/library/mesh_base/index.md#option_ssdirt)** and *[**terrain_global_base**](../../../../content/materials/library/terrain_global_base/index.md#option_ssdirt)* having the **SSDirt** option enabled.


To set up SSDirt for a specific material, perform the following:


1. Enable the *[Procedural Effects](../../../../content/materials/library/mesh_base/index.md#option_procedural)* option of the target material.
2. Enable the *[SSDirt](../../../../content/materials/library/mesh_base/index.md#option_ssdirt)* option of the target material.
3. [Enable](#enabled) the *Screen-Space Dirt* effect in one of the following ways:

  - Via the *Render Settings* window: go to the *Windows -> Settings -> Runtime -> Render -> SSDirt* section and click **Enabled**.
  - In the Main Menu select *Rendering -> Features* and choose **SSDirt**.
4. In the *Render Settings* window, specify the [global SSDirt settings](#enabled) described above.
5. In the [material settings](../../../../editor2/materials_settings/index.md) (the *Parameters* window), specify cavity and convexity masks in the [procedural texture](../../../../content/materials/library/mesh_base/index.md#texture_procedural), [UV coordinates transformation](../../../../content/materials/library/mesh_base/index.md#parameters_ssdirt_uv_transform), *[Cavity Scale](../../../../content/materials/library/mesh_base/index.md#parameters_ssdirt_cavity_scale)*, and *[Convexity Scale](../../../../content/materials/library/mesh_base/index.md#parameters_ssdirt_convexity_scale)*.
