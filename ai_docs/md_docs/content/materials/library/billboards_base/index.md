# billboards_base


The *billboards_base* material is used to create coverings for multiple [Billboards](../../../../objects/objects/billboards/index.md).

 Prior KnowledgeThis article assumes that you have prior knowledge of the following topics. Please read them before proceeding:
- *[Materials Settings](../../../../editor2/materials_settings/index.md)*
- The *[mesh_base](../../../../content/materials/library/mesh_base/index.md)* material


## States


![States](states.png)

*Statestab*


### Default


| Deferred Buffer | If enabled, the material is rendered to the [deferred buffers](../../../../principles/render/sequence/index.md#forward_buffers). |
|---|---|
| Auxiliary Rendering | Toggles the auxiliary rendering pass for the material on and off. This pass can be used for custom post effects. Enabling the pass activates the [auxiliary texture](#texture_auxiliary) and the [auxiliary color](#auxiliary_param) parameter. |
| Lock Axis X | If enabled, locks billboards orientation along the *X* axis (by default billboards always face the camera). ![](x_disabled.png) ![](x_enabled.png) |
| Lock Axis Z | If enabled, locks billboards orientation along the *Z* axis (by default billboards always face the camera). ![](z_disabled.png) ![](z_enabled.png) Billboards can be also locked along both *X* and *Z* axes, so they will be oriented perpendicularly to *Y* axis. |
| Screen Aligned | If enabled, sets billboards parallel to each other. If they are not axis-locked, they are oriented strictly towards to the screen plane. ![](screen_aligned_disabled.png) ![](screen_aligned_enabled.png) |
| Angular Size | If enabled, sets billboards to always be of the same size regardless of the camera position. ![](angular_size_enabled.png) ![](angular_size_enabled_far.png) |


### Options


| Emission | Toggles on and off rendering of the [emission](../../../../content/materials/library/mesh_base/index.md#option_emission) effect and an additional [emission texture](#texture_additional_emission). |
|---|---|
| Emission Texture | The option allows selecting the texture to be used for the [emission](../../../../content/materials/library/mesh_base/index.md#option_emission) effect: [Albedo](#texture_base_diffuse) or [Emission](#texture_additional_emission). |
| Angle Visibility | Enables the [parameters](#visibility_param) that set limits for visibility of the billboards at a certain horizontal and/or vertical angle. Can be used to simulate directional light based on billboards. |
| Angle Visibility Fade | Toggles on and off the [Angle Fade](#visibility_param_angle_fade) parameter for the [Angle Visibility](#angle_visibility) option. If enabled, allows creating an effect of gradual fading at a certain range. |
| Geometry Inflation | Toggles on and off limiting the minimum billboard screen size (in pixels) to a fixed value set in the [Inflation Scale](#geometry_param_inflation_scale) parameter in order to provide visibility from far distances. |
| Soft Interaction | Toggles on and off soft depth interaction of billboards with objects. This option can be used to avoid visual artefacts in the areas where billboards and objects overlap. Enabling this option activates the [Soft Interaction](#soft_interaction_param) parameter. > **Notice:** This state is available for all transparent materials except materials with the *Alpha test* transparency preset enabled. |
| Haze | If enabled, billboards are overlapped by the [haze](../../../../editor2/settings/render_settings/environment/index.md#haze). > **Notice:** This state is available for all transparent materials except materials with the *Alpha test* transparency preset enabled. |


### Light Passes


![](states_light.png)

*Statestab,Light Passessection*


> **Notice:** The states are available for all transparent materials except materials with the *Alpha test* transparency preset enabled.


| Environment | Enables rendering of the material illuminated by the ambient light. |
|---|---|
| Light Omni | Enables rendering of the material illuminated by an omni light. |
| Light Proj | Enables rendering of the material illuminated by a projected light. |
| Light World | Enables rendering of the material illuminated by a world light. |


### Shadows


![](shadows_settings.png)

*Material window,Statestab.*


These options control rendering of shadows cast on transparent objects.

> **Notice:** This group of settings is available for **transparent materials** only.
>
>
> Enabling/disabling shadows options via *Rendering -> Shadows* menu does not affect transparent materials, as they are controlled **per-material** via the group of options listed below.


#### Lerp Cascades


**Lerp Cascades** enables linear interpolation for shadows cascades. When enabled, transitions between cascades become smoother. However, the option drops performance, as in the transition parts 2 shadow maps are rendered.

> **Notice:** For this feature to work properly linear interpolation of shadow cascades should be [enabled globally](../../../../editor2/settings/render_settings/shadows/index.md#lerp_shadow_cascades) (via *Rendering -> Shadows -> Lerp Shadow Cascades*).


#### Filter Mode


Filtering mode to be used for shadows from all light sources cast on the material. This mode determines the quality of soft shadows reducing the stair-step effect. *Higher* quality produces *smoother* shadows. Available values:

- **Disabled** - filtering for shadows is disabled, the stair-step effect is clearly seen at the edges of shadows.
- **Low** � low quality
- **Medium** � medium quality
- **High** � high quality
- **Ultra** � ultra quality


> **Notice:** This parameter is similar to the [global shadow filtering mode](../../../../editor2/settings/render_settings/shadows/index.md#filter_mode) (*Settings -> Render -> Shadows*), but is used for transparent objects on a per-material basis.


#### Penumbra Mode


Quality mode to be used for rendering penumbra from all light sources cast on the material. This mode enables simulation of real-world shadows by keeping sharp contact shadows closer to the base and softening the farther the shadow stretches away. *Higher* quality produces *softer* shadows. Available values:

- **Disabled** - penumbra rendering is disabled, shadow edges are crisp and sharp (no shadow softness at all).
- **Low** � low quality
- **Medium** � medium quality
- **High** � high quality
- **Ultra** � ultra quality


> **Notice:** This parameter is similar to the [global shadow penumbra mode](../../../../editor2/settings/render_settings/shadows/index.md#penumbra_mode) (*Settings -> Render -> Shadows*), but is used for transparent objects on a per-material basis.


#### Filter Noise


Toggles the use of noise for shadow filtering on and off. This noise is used for smoothing shadows cast on the material and reducing the stair-step effect at the edges of shadows.

> **Notice:** This parameter is similar to the [global shadow filter noise](../../../../editor2/settings/render_settings/shadows/index.md#filter_noise) (*Settings -> Render -> Shadows*), but is used for transparent objects on a per-material basis.


#### Penumbra Noise


Toggles the use of noise for penumbra rendering on and off. This noise is used for smoothing soft shadows cast on the material.

> **Notice:** This parameter is similar to the [global shadow penumbra noise](../../../../editor2/settings/render_settings/shadows/index.md#penumbra_noise) (*Settings -> Render -> Shadows*), but is used for transparent objects on a per-material basis.


### Post Processing


Post Processing options activate post processing effects for the material.


![](states_post.png)

*Statestab,Post Processingsection*


| SSAO | Toggles screen space ambient occlusion on and off. Available for opaque and alpha test materials (materials with the *Alpha test* transparency preset enabled). |
|---|---|
| SSR | Toggles screen space reflections on and off. Available for opaque and alpha test materials (materials with the *Alpha test* transparency preset enabled). |
| SSSSS | Toggles screen-space subsurface scattering on and off. Available for opaque and alpha test materials (materials with the *Alpha test* transparency preset enabled). |
| DOF | Toggles the depth of field effect on and off. Available for both opaque and transparent materials. |
| Motion Blur | Toggles the motion blur effect on and off. Available for both opaque and transparent materials. |
| Screen-Space Shadows | Toggles the screen-space shadows effect on and off. Available for both opaque and transparent materials. |


## Textures


![](textures.png)

*Texturestab*


### Base


| Diffuse | The diffuse texture defines the color of the surface. The texture is 4-channeled (RGBA): - *RGB* values store color information. - The *Alpha (A)* value stores transparency information: - **White** color indicates the visible area. - **Black** color indicates the transparent area. |
|---|---|
| Normal | The normal texture stores information about the surface's contours in order to create the illusion of depth and is used to add details without adding additional polygons. The texture is 2-channeled: RG values contain two components of a normal, and the third component's value is calculated from the given components at run time. |
| Specular | The specular texture defines the surface's shininess and highlights color. The texture is 4-channeled (RGBA): - *RGB* values store reflection color and intensity (black color means no reflection). - The *alpha (A)* value specifies the specular power: **0** means specular highlights are very bright and intense, **256** � specular highlights are faded. |


> **Notice:** The base textures with the ***_d***, ***_n*** and ***_s*** postfixes in the name respectively, located in a folder named `uncompressed`, are automatically compressed by the engine.


### Options


| Emission | Emission texture stores information about the light emission. This texture is available only if the [Emission](#emission) option is enabled. The texture is 4-channeled (RGBA): - *RGB* values store the glowing color. - The *Alpha (A)* value stores the *glow mask*: black is for non-glowing areas, white � for glowing ones. |
|---|---|
| Auxiliary | Auxiliary texture is used for rendering into the [Auxiliary](#pass_auxiliary) buffer. |


## Parameters


![](parameters.png)

*Parameterstab*


### Default


| Material Mask | Specifies a [material bit mask](../../../../principles/bit_masking/index.md#material_mask) that is used for projecting the decal. If the material mask of the surface material matches the decal material mask, the decal is projected onto it. |
|---|---|


### Base


| Diffuse | A color picker to choose the color of the [diffuse map](#texture_base_diffuse). |
|---|---|
| Specular | A color picker to choose the color of the [specular map](#texture_base_specular). |
| Gloss | A coefficient to modify size of the highlight of the [specular map](#texture_base_specular): - **Low** values imitate wider highlights, typically appropriate to create a diffuse reflection from the matte surface. - **High** values imitate pinpoint highlights, typically appropriate to create a uniform reflection of light rays from the glossy surface. |
| Normal Intensity | A coefficient to scale the intensity of the normals (provided by a [normal map](#texture_base_normal)). The higher the value, the more the normal texture effect is. |
| Translucency | Scale of the translucency effect, which permits light to pass through the object, but diffuses it so objects on the opposite side are not clearly visible. > **Notice:** This parameter is operating with non-transparent materials only. |
| Microfiber | Coefficient to scale the intensity of the microfiber effect. The higher the value, the more pronounced the microfiber effect is. |
| UV Transform | Transformation of the base texture coordinates. The field contains a vector of four float components: - The first pair of coordinates scales the texture along the *X* and *Y* axes. - The second pair of coordinates offsets the texture respectively to its initial position along the *X* and *Y* axes. > **Notice:** For more details about the UV Transform parameter, see the [Texture coordinates transformation](../../../../content/materials/library/mesh_base/index.md#texture_transform) chapter of the mesh_base article. |


### Emission


Emission parameters are available at enabling the [Emission](#emission) option in the *States* tab.


| Color | A color picker to choose an ambient emission color for the [emission texture](#texture_additional_emission). |
|---|---|
| Scale | Visibility scale for the [emission texture](#additional_textures). Raising the value increases visibility of the emission texture: light areas become lighter and brighter. |
| Visibility Distance | Distance from the camera up to which the emission from the billboard will be visible, in units. |
| Visibility Power | Power multiplier to scale distant dependent visibility of the [emission texture](#additional_textures). It determines the way the intensity of the emission effect changes depending on the distance from the camera. |


### Geometry


| Billboard Scale | A factor to manage the billboard size. |
|---|---|
| Inflation Scale | Minimum permissible size for the billboard, in pixels. The parameter is available only if the [Geometry Inflation](#geometry_inflation) option is enabled in the *States* tab. |


### Visibility


Geometry parameters are available only if the corresponding item of the [Angle Visibility](#angle_visibility) option is enabled in the *States* tab.


| Horizontal Angle | Angle limit in the XY plane relative to the -Y direction, in degrees. The billboards are visible within the [-value; value] range of angles. |
|---|---|
| Vertical Angle | Angle limit relative to the Z axis, in degrees. The billboards are visible within the [-value; value] range of angles. |
| Fade Angle | A portion of the [Horizontal](#visibility_param_horizontal_angle) and/or [Vertical Angle](#visibility_param_vertical_angle) within which fading occurs, in degrees. If equals to 0, the billboards disappear at the limit of a visibility angle without fading; if, for example, equals to 10, each billboard would fade gradually within the last 10 degrees of a visibility angle. The parameter is available only if the [Angle Visibility Fade](#angle_visibility_fade) option is enabled in the *States* tab. |


### Other Parameters


| Auxiliary Color | A color picker to choose an auxiliary color for the [Auxiliary rendering pass](../../../../principles/render/sequence/index.md#auxiliary). Available only if the [Auxiliary](#pass_auxiliary) option is enabled in the *States* tab. |
|---|---|
| Soft Interaction | Depth factor that controls fading of the billboards depending on their position relative to the object. Available only if the [Soft Interaction](#soft_interaction) option is enabled in the *States* tab. |
