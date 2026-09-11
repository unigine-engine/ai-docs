# grass_base


A *grass_base* material is used to create realistic animated grass, plants and flowers. It is applied to [ObjectGrass](../../../../objects/objects/grass/index.md).

 Prior KnowledgeThis article assumes you have prior knowledge of the following topics. Please read them before proceeding:
- *[Materials Settings.](../../../../editor2/materials_settings/index.md)*
- *[mesh_base material states, textures, parameters.](../../../../content/materials/library/mesh_base/index.md)*


[![](index_sm.png)](index.png)


## States


![States](states.png)

*Materials editor,Statestab.*


### Options


#### Auxiliary Pass


**Auxiliary** pass is used for writing an additional texture into an auxiliary color buffer. Detail information on the pass can be found in the [Rendering Sequence](../../../../principles/render/sequence/index.md#auxiliary) article.


> **Notice:** Enabling this option activates an additional **[Auxiliary texture](#texture_auxiliary)** and [**Auxiliary parameters**](#parameter_auxiliary).


#### Shape


**Shape** specifies the way to render the grass geometry:


- **Default** - grass quads are rendered as a plain geometry and are turned randomly.
- **Billboard** - grass quads are rendered as billboards and always face the camera.


| ![](shape_0.png) | ![](shape_1.png) |
|---|---|
| *Default shape* | *Billboard shape* |


#### Animation


**Animation** option enables animation for objects (e.g. for plants swinging in the wind). Available modes:


- **Disabled** - animation is disabled.
- **Default** - standard animation is enabled. ![](animation_default.gif) *Standard animation*
- **Field Animation** - standard animation is enabled. Besides, objects are also influenced by [FieldAnimation](../../../../objects/effects/fields/field_animation/index.md). | ![](animation_1.gif) | ![](animation_2.gif) | |---|---| | *FieldAnimation with visualizer disabled* | *FieldAnimation with visualizer enabled* |


> **Notice:** Enabling this option activates additional **[Animation](#parameters_animation)** parameters.


#### FieldSpacer Interaction


**FieldSpacer interaction** option enables interaction with [FieldSpacer](../../../../objects/effects/fields/field_spacer/index.md) objects.


| ![](spacer_disabled.png) | ![](spacer_enabled.png) |
|---|---|
| *Interaction with FieldSpacer disabled* | *Interaction with FieldSpacer enabled* |


#### Noise


**Noise** activates a spatial color [noise texture](#texture_noise), so the grass field is colored differently according to it. The noise can add irregularity to the color of the grass field or it can color the grass.


| ![](color_noise_disabled.png) | ![](color_noise_enabled.png) |
|---|---|
| *Noise disabled* | *Noise enabled* |


> **Notice:** Enabling this option activates the additional [**Noise texture**](#texture_noise) and [**Noise**](#parameter_noise) parameters.


#### Light Map


**Light map** activates an additional light map texture therefore specifying that the material will be rendered lit by it. Color is multiplied by the light map and the [ambient](../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssao/index.md) color.


> **Notice:** Enabling this option activates the additional [**Lightmap texture**](#textures_lightmap) and **[Lightmap Scale](#parameter_lightmap)** parameters.


#### Ambient Occlusion


**Ambient Occlusion** enables the [ambient occlusion](#parameter_occlusion) that sets shading arising from the ground to the top of the grass blade.


| ![](occlusion_disabled.png) | ![](occlusion_enabled.png) |
|---|---|
| *Ambient Occlusion disabled* | *Ambient Occlusion enabled* |


> **Notice:** Enabling this option activates the additional **[Occlusion scale](#parameter_occlusion)** parameter.


#### Translucent


**Translucent** activates an additional [translucent texture](#textures_translucent).


#### Emission


**Emission** activates an additional [emission texture](#textures_emission). It is used to simulate glow from extremely bright surfaces, therefore imitating real light sources and highlights.


#### Bend


**Bend** activates an additional [bend texture](#textures_bend) and [bend scale parameter](#bend_scale). It is used to bend grass according to the mask.


| ![](grass_bend_disabled.png) | ![](grass_bend_enabled.png) |
|---|---|
| *Bend option disabled* | *Bend option enabled* |


#### Jitter Transparency


**Jitter transparency** enables creating deferred transparency by using jittering. The state can be used when such result is acceptable and post-effects are applied to the material.


#### Mip Bias


**Mip bias** activates an additional [mip bias](#parameter_mip_bias) parameter. It is used to adjust mip mapping.


## Textures


![Textures](textures.png)

*Materials Editor,Texturestab.*


### Base Textures


#### Diffuse Texture


**Diffuse** texture defines the grass shape and color. It is subdivided into **chunks** that are placed in the texture as follows:

- The horizontal row can have up to **4** chunks. This number depends on the number of channels of the [mask texture](../../../../objects/objects/grass/index.md#mask) used.
- The vertical column can have any number of chunks from **1** to **4**. Chunks in the column represent variations of grass of the particular species (thinner, thicker, tangled, etc.). The chunks of the column are randomly spread across the area.


![](chunk.png)


The texture is 4-channeled (RGBA):

- The *RGB* values store grass color information.
- The *alpha (A)* stores transparency information and defines which parts of the grass chunks will be rendered colored and which ones will be cut by means of the alpha test.


> **Notice:** The chunks of the diffuse texture can be rendered according to a [mask texture](../../../../objects/objects/grass/index.md#mask). In this case, each chunk of the horizontal row will correspond to the red, green, blue and alpha channels of the mask (see [details](../../../../objects/objects/grass/index.md#rendering)).


### Options Textures


#### Noise Texture


**Noise** texture is used to color the grass (for example, to match the colors of the terrain) or to add irregularity to the color of the grass field. In both cases, the colors of the grass diffuse texture and the spatial noise texture are blended in the overlay mode.


The texture is 3-channeled (RGB).


| ![](noise_texture.png) | ![](noise_texture_colored.png) |
|---|---|
| *Noise texture used to add color irregularity* | *Noise texture used to color the grass* |


For example, if you apply these textures to the following grass field and set the [**Noise Scale**](#scale) to **0.6**, you will get the following result:


![](grass_regular.png)

*The original grass field*


| ![](grass_noise_irregular.png) | ![](grass_noise_color.png) |
|---|---|


The texture that is used to color the grass is usually generated based on the terrain's albedo colors. The texture and the terrain size may differ, but dimensions of the the spatial noise texture should be equal to some power of two (for example, 1024�נ1024, 2048�נ2048, and so on).


> **Notice:** The texture is present only if **[Noise](#option_color_noise)** is enabled.


#### Lightmap Texture


**Lightmap** texture stores pre-computed light information.

> **Notice:** This texture is present only if **[Light Map](#option_light_map)** is enabled.


#### Translucent Texture


**Translucent** texture stores information on material's translucency.

> **Notice:** This texture is present only if **[Translucent](#option_translucent)** is enabled.


#### Auxiliary Texture


Auxiliary texture is used for [auxiliary](#pass_auxiliary) rendering pass.


#### Emission Texture


**Emission** texture stores information about the light emission. It is blended additively over a texture, so areas which do not glow at all should be pure black on the glow mask, and any brighter colors will appear to be emitting light.


The texture is 4-channeled (RGBA):

- The *RGB* values store information on a glowing color.
- The *alpha (A)* value stores a glow mask:

  - **White** color indicates that the area is glowing.
  - **Black** color indicates that the area is not glowing.


> **Notice:** The texture is present only if **[Emission option](#option_emission)** is enabled.


#### Bend Texture


**Bend** texture stores the grass bending mask.


The texture is 1-channeled (R):

- *R* - bend intensity values.


> **Notice:** The texture is present only if **[Bend option](#option_bend)** is enabled.


## Parameters


![](parameters.png)


> **Notice:** Availability of some parameters depends on the set *[States](#states)* field values.


All the parameters have default values, which can be replaced by your own ones.


### Material Mask


![](decal_mask_parameters.png)


**Material mask** parameter specifies a decal bit-mask. If the material mask of the decal material matches the material mask of the surface material, the decal will be projected.


### Base Shading Parameters


![](shading_parameters.png)


#### Diffuse Color


**Diffuse** texture color is the base color of the grass surface.


| ![](diffuse_color_0.png) | ![](diffuse_color_1.png) | ![](diffuse_color_2.png) |
|---|---|---|
|  |  |  |


#### Specular Color


**Specular** is a color picker to choose the auxiliary specular color. It can be used for specifying different specular colors for one texture or modifying the texture color on the spot.


| ![](specular_color_0.png) | ![](specular_color_1.png) | ![](specular_color_2.png) |
|---|---|---|
|  |  |  |


#### Gloss


**Gloss** is a coefficient modifying the size of the highlight. Low values imitate wider highlights, typically appropriate to create diffuse reflection from mat surfaces. High values imitate pinpoint highlights, typically appropriate to create uniform reflection of light rays from glossy surfaces.


#### Microfiber


**Microfiber** is a coefficient to scale the intensity of the microfiber effect. This parameter creates an effect of the napped surface. The *higher* the value, the *higher* the microfiber effect is.


#### Translucent


A coefficient to scale the translucent effect, which permits light to pass through the grass blades, but diffuses it so objects behind the grass blades are not visible.  The *higher* the value, the *more translucent* the material is.


| ![](translucency_0.png) | ![](translucency_1.png) | ![](translucency_2.png) |
|---|---|---|
|  |  |  |


#### Alpha Intensity


A coefficient to scale the value of the alpha channel of the grass diffuse texture. The higher the value, the bigger areas of the texture are rendered.


| ![](alpha_0.png) | ![](alpha_1.png) |
|---|---|
| ![](alpha_value_0.png) | ![](alpha_value_1.png) |


#### Slope Scale


A coefficient to scale the inclination of grass polygons.

- By the minimum value of **0**, inclination of the grass polygons coincides direction of the normal of the polygon on which the grass grows.
- When increasing the parameter value, the inclination of the grass polygons relative to the camera increases.


| ![](slope.png) |  |
|---|---|
| ![](slope_00.png) | ![](slope_01.png) |
| ![](slope_changing.gif) |  |
| *Changing value from 0 to 0.6 and conversely* |  |


#### Mip Bias


Coefficient for mip maps adjusting.


### Animation Parameters


![](animation_parameters.png)


#### Stem Noise


**Stem noise** is a coefficient to scale a spatial noise that diversifies the direction of movement of the grass.

- **0** makes the grass move uniformly.
- *Increasing* the value makes the grass blades movement more random.


![](stem_noise.gif)


| ![](stem_noise_0.png) | ![](stem_noise_1.png) |
|---|---|


#### Stem Offset


**Stem offset** is a coefficient to scale an amplitude of horizontal movement of the grass.


![](stem_offset.gif)


| ![](stem_offset_0.png) | ![](stem_offset_1.png) |
|---|---|


#### Stem Radius


**Stem radius** is a coefficient to scale an amplitude of vertical movement of the grass.


![](stem_radius.gif)


| ![](stem_radius_0.png) | ![](stem_radius_1.png) |
|---|---|


#### Stem Scale


**Stem scale** is a coefficient to scale the speed of grass movement.


![](stem_scale.gif)


| ![](stem_scale_0.png) | ![](stem_scale_1.png) |
|---|---|


### Noise


![](noise_parameters.png)


#### Transform


Spatial noise texture coordinates transformation represented by a vector of the four float components: the first two scale the texture along the *X* and *Y* axes, and the last two offset it along the *X* and *Y* axes.


#### Scale


Intensity of the [spatial noise texture](#texture_noise).


| ![](noise_scale_0.png) | ![](noise_scale_1.png) |
|---|---|
| ![](noise_scale_00.png) | ![](noise_scale_01.png) |


### Emission


![](emission_parameters.png)


#### Color


**Color** is a color multiplier for the emission texture.


#### Intensity


**Intensity** is a coefficient to scale intensity of the emission texture. The *higher* the value, the *lighter* and *brighter* light areas of the emission texture are.


### Lightmap


![](lightmap_parameters.png)


#### Intensity


**Intensity** is a coefficient to scale the intensity of the light map illumination. The higher the value, the brighter the illumination is.


#### Gamma


**Gamma** parameter specifies the gamma of the light map texture.


### Ambient Occlusion


![](occlusion_parameters.png)


#### Visibility


**Visibility** parameter specifies how the AO has influence on grass.


#### Multiplier


**Multiplier** is a coefficient to scale the occlusion that sets shading starting from the ground to the top of the grass blades. The *higher* the value, the *less shaded* the grass is.


#### Power


**Power** parameter sets the rate of ambient occlusion appearance on the grass.


#### Impact On Diffuse


**Impact On Diffuse** shows how ambient occlusion affects the grass diffuse texture.


### Options


![](auxiliary_parameters.png)


#### Auxiliary Color


**Color** is a constant color for the auxiliary rendering pass.


#### Bend Scale


**Intensity** is a coefficient to scale bending of the grass. The *higher* the value, the *more significant* the bending is.


| ![](grass_bend_scale_06.png) | ![](grass_bend_scale_08.png) |
|---|---|
| *Bend Scale = 0.6* | *Bend Scale = 0.8* |
