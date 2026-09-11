# grass_impostor_base


A *grass_impostor_base* material is used for vegetation impostors. It can be applied to [grass objects](../../../../objects/objects/grass/index.md) that, in turn, can be used as impostors for trees.


[![](index_sm.jpg)](index.jpg)

*Impostor Trees*


## States


![States](states.png)

*Material Settings, States Tab*


### Options


#### Auxiliary


**Auxiliary** rendering pass is used for writing an additional texture into an auxiliary color buffer. Detail information on the pass can be found in the [Rendering Sequence](../../../../principles/render/sequence/index.md#auxiliary) article. The pass can be used for custom post-process effects.

> **Notice:** Enabling this option activates the additional [Auxiliary texture](#texture_auxiliary) and [Auxiliary parameters](#parameters_auxiliary).


#### Noise


**Noise** activates spatial color noise texture, so the grass is colored according to it. The noise texture can add irregularity to the color of the grass field or it can color the grass.

![](noise_0.jpg) ![](noise_1.jpg)


> **Notice:** Enabling this option activates the additional [Noise texture](#texture_noise) and [Noise parameters](#parameters_noise).


#### Ambient Occlusion


**Ambient Occlusion** enables the ambient occlusion that sets shading arising from the ground to the top of the grass blade.

![](occlusion_0.jpg) ![](occlusion_1.jpg)


> **Notice:** Enabling this option activates the additional [Ambient Occlusion parameters](#parameters_noise).


#### AO Map


**AO Map** enables the ambient occlusion effect. This effect is used to modulate global environment illumination using baked shadows from environment probes. Enabling the option activates the [ambient occlusion texture](#texture_ao).


#### Normal Map


**Normal Map** enables the [normal map](#texture_normal) for the grass impostors. This option is used to fake the relief on the impostor surface.


#### Shading Map


**Shading Map** enables the [shading texture](#texture_shading) for the material.


#### Microfiber Map


**Microfiber Map** enables using of the Alpha channel of the [shading texture](#texture_shading) as a microfiber map.


#### Specular Map


**Specular Map** enables using of the B channel of the [shading texture](#texture_shading) as a specular reflection intensity map.


#### Translucent Map


**Translucent Map** enables the translucence effect and activates an additional [translucent texture](#texture_translucent).


#### Depth Map


**Depth Map** activates an additional [depth texture](#texture_depth).


#### Screen Aligned


**Screen Aligned** sets the impostor parallel to the screen plane. The option should be enabled for correct rotation of impostors when the camera looks down. We recommend you to use this option only when impostor rotation is required, as in other cases it may lead to visual artifacts.

> **Notice:** It is not recommended to enable this option when multi-monitor configuration is used: noticeable seams between monitors may occur.


#### Lerp


**Lerp** enables smooth linear interpolation of sprites when the camera rotates around the object. This state should be enabled, if the grabbed impostor textures store low number of frames (i.e. the *Phi* and *Theta* values are small).

![](lerp_0.jpg) ![](lerp_1.jpg)


The following options are available:


- **Disabled** - linear interpolation between the sprites is disabled.
- **Lerp Unoptimized** - legacy linear interpolation mode (interpolation is calculated during the depth pre-pass, making it three times slower than the mode below).
- **Lerp With Separate Opacity Map** - optimized linear interpolation mode using an additional *[Opacity Lerp Map](../../../../editor2/tools/impostors_creator/index.md#opacity_lerp_map)*).


Selecting the last item in the list activates an additional [opacity lerp map](#texture_opacity_lerp_map).


#### Lerp Mode


Linear interpolation mode to be used, one of the following:


- **Full** - sprites are interpolated horizontally and vertically.
- **Horizontal Only** - sprites are interpolated only horizontally, vertically switching is used, this mode can be used for example if we do not fly above the impostors, but rather move around them.


#### Lerp Fix Blur


This option helps making details of impostor images look sharper and less blurred reducing the negative effect of linear interpolation.


> **Notice:** **Lerp Fix Blur** mostly improves the look of impostors generated for vegetation, or can be used for sprites having some irregular patterns. It should be disabled for sprites having geometry patterns, like bricks and so on.


#### Up Direction


**Up Direction** makes impostors always point upwards.


When the impostors are [oriented](../../../../objects/objects/grass/index.md#orientation) along normal of the parent node (usually the terrain), trees grow almost perpendicular to the terrain slopes. To make the trees pointing *up*, the *[Up Direction](#option_up_direction)* option should be enabled. At that, the impostors normals remain the same. It allows you to get correct shadowing of trees impostors on the steep slopes.


#### Animation


**Animation** option enables animation for objects (e.g., for plants swinging in the wind). Available modes:

- **None** � animation is disabled.
- **Animation** � standard animation is used. ![](animation_0.gif) *Standard Animation of Impostors*
- **Field Animation** � standard animation is used together with animation produced by [Field Animation](../../../../objects/effects/fields/field_animation/index.md). ![](animation_1.gif) *Standard Animation of Impostors + Field Animation*


> **Notice:** Enabling this option activates the additional [Animation parameters](#parameters_animation).


#### Jitter Transparency


**Jitter Transparency** enables creating deferred transparency for Alpha Test materials by using jittering. The state can be used when such result is acceptable and post-effects are applied to the material.


#### Mip Bias


**Mip Bias** activates an additional [mip bias parameter](#parameter_mip_bias). It is used to adjust mip mapping.


#### Visibility Mask


**Visibility Mask** activates an additional [visibility mask texture](#texture_visibility_mask) and [visibility mask threshold parameter](#parameter_visibility_mask_threshold). It is used to cut out grass according to the mask texture.


### Post Processing


#### Material SSAO


**SSAO** enables screen space ambient occlusion.


#### Material SSR


**SSR** enables screen space reflections.


#### Material SSSSS


**SSSSS** enables screen-space subsurface scattering.


#### Material DOF


**DOF** enables the depth of field effect.


#### Material Motion Blur


**Motion Blur** enables the motion blur effect.


#### Screen-Space Shadows


**Screen-Space Shadows** enables the screen-space shadows effect.


## Textures


Textures available for the material. All textures fields have set default textures, which can be replaced by your own ones. Availability of some textures depends on the set *[States](#states)* values.


![Textures](textures.png)

*Material Settings, Textures Tab*


### Base Textures


#### Albedo Texture


An albedo texture that specifies the color of the impostor surface. To create an albedo texture for impostor, use Impostors Creator tool: the texture will be set automatically after generation.


The texture is 4-channelled (RGBA):

1. *RGB* values store color information.
2. An *alpha (A)* value stores transparency information.


#### Shading Texture


A shading texture is a container for four different textures:

- The *R* channel stores a *[metalness](../../../../content/materials/library/mesh_base/index.md#texture_metalness_channel)* texture.
- The *G* channel stores a *[roughness](../../../../content/materials/library/mesh_base/index.md#texture_roughness_channel)* texture.
- The *B* channel stores a *[specular](../../../../content/materials/library/mesh_base/index.md#texture_specular_channel)* texture. > **Notice:** The texture from this channel can be used only if the [Specular Map](#option_specular_map) option is enabled.
- The *A* channel stores a *[microfiber](../../../../content/materials/library/mesh_base/index.md#texture_microfiber_channel)* texture. > **Notice:** The texture from this channel can be used only if the [Microfiber Map](#option_microfiber_map) option is enabled.


#### Normal Texture


**Normal** texture of the grass impostor. The texture is used to fake the relief on the impostor surface. To create a normal texture for impostor, use [Impostors Creator](../../../../editor2/tools/impostors_creator/index.md) tool.

> **Notice:** **Unigine Engine** expects a normal map in *DirectX* format. If your normal map is in *OpenGL* format, tick *[Invert G Channel](../../../../editor2/assets_workflow/texture_import.md#invert_g)* in the import menu. As a general rule, if the lighting seems weird, try inverting the G Channel and see if it gets better.


### Additional Textures


#### Ambient Occlusion Texture


Ambient occlusion texture modulates the global environment illumination, for example, when an object is lighter at the top from sky above, and darker at the bottom from the ground below. The texture uses only R channel.


#### Translucent Texture


Translucent texture stores information on material's translucency. For example, by using this texture, it is possible to specify parts of the object that aren't translucent (the *[Translucent](#parameter_translucent)* parameter won't affect them).


#### Auxiliary Texture


**Auxiliary** texture is used for [auxiliary rendering pass](../../../../principles/render/sequence/index.md#auxiliary).

> **Notice:** The texture is available only if **[Auxiliary](#option_auxiliary)** is enabled.


#### Depth Texture


Depth texture stores information on the material's depth.


The texture is 1-channelled.


> **Notice:** The texture is available only if **[Depth Map](#option_depth)** is enabled.


#### Opacity Lerp Map


This texture is used for smooth linear interpolation of sprites when the camera rotates around the object avoiding abrupt switching between the sprites. [Linear interpolation](#option_lerp) based on this texture is performance-friendly, as it is performed during the deferred pass. To create a texture for an impostor, use the [Impostors Creator](../../../../editor2/tools/impostors_creator/index.md) tool: the texture is set automatically after generation.


The texture is 4-channelled.


> **Notice:** The texture is available only if **[Lerp](#option_lerp)** is enabled.


#### Noise Texture


**[Noise](../../../../content/materials/library/grass_base/index.md#texture_noise)** texture is used to color the grass (for example, to match the colors of the terrain) or to add irregularity to the color of the grass field. In both cases, the colors of the grass diffuse texture and the spatial noise texture are blended in the overlay mode.


The texture is 3-channelled (RGB).

> **Notice:** The texture is available only if **[Noise](#option_noise)** is enabled.


#### Visibility Mask Texture


**Visibility Mask** texture is used to cut out grass.


The texture is 1-channelled (R).

- *R* � visibility mask.


> **Notice:** The texture is available only if **[Visibility Mask](#option_visibility_mask)** is enabled.


## Parameters


Availability of some parameters depends on the set *[States](#states)* field values.


![](parameters.png)

*Material Settings, Parameters Tab*


### Material Mask


![](material_mask.png)


**Material Mask** parameter specifies a decal bit-mask. If the material mask of the decal material matches the material mask of the surface material, the decal will be projected.


### Transform Parameters


This group of parameters determines coordinates transformation of impostors


| ![](parameters_transform.png) |
|---|
| *Transform Parameters* |


#### Phi


**Phi** determines the number of frames grabbed into the impostor texture (horizontal camera rotation).


#### Theta


**Theta** determines the number of frames grabbed into the impostor texture (vertical camera rotation).


#### Size


**Size** size of the object for which impostors were grabbed.


#### Pivot Offset


**Pivot Offset** offset of the pivot point from the center of the object's bounding box.


### Base Shading Parameters


![](parameters_base.png)


#### Albedo


**Albedo** is a multiplier of the base color of the surface provided by the [albedo texture](#texture_albedo).


#### Metalness


**Metalness** is a multiplier of metalness.


#### Roughness


**Roughness** is a multiplier of the roughness of a surface.


#### Specular


**Specular** is a multiplier for the intensity of highlight provided by the [specular texture](#texture_shading).


#### Microfiber


**Microfiber** is a coefficient to scale the intensity of the microfiber effect (provided by the [microfiber texture](#texture_shading)). This parameter creates an effect of the napped surface. The higher the value, the higher the microfiber effect is.


#### Translucent


**Translucent** is a coefficient to scale the translucent effect, which permits light to pass through the grass blades, but diffuses it so objects behind the grass blades are not visible. The *higher* the value, the *more translucent* the material is.

![](translucent_0.jpg) ![](translucent_1.jpg)


#### Alpha Intensity


**Alpha Intensity** is a coefficient to scale the value of the alpha channel of the grass diffuse texture. The higher the value, the bigger areas of the texture are rendered.

![](alpha_intensity_0.jpg) ![](alpha_intensity_1.jpg)


#### Shadow Offset


**Shadow Offset** sets an offset of grass impostors shadows.


#### Orientation Normals


When the *[Up Direction](#option_up_direction)* option is used for impostors that are [oriented](../../../../objects/objects/grass/index.md#orientation) along normal of the parent node (usually - a terrain), the [normal map](#texture_normal) set for impostors is blended with the normal map produced by such orientation settings. **Orientation Normals** sets a coefficient of such normal maps blending. The default value is 1. The higher the value, the more intense the effect of orientation settings.


#### Mip Bias


**Mip Bias** is a coefficient for mip maps adjusting.


### Animation Parameters


![](parameters_animation.png)


#### Stem Noise


**[Stem noise](../../../../content/materials/library/grass_base/index.md#parameter_stem_noise)** is a coefficient to scale a spatial noise that diversifies the direction of movement of the grass.

- 0 makes the grass move uniformly.
- Increasing the value makes the grass blades movement more random.


#### Stem Offset


**[Stem offset](../../../../content/materials/library/grass_base/index.md#parameter_stem_offset)** is a coefficient to scale an amplitude of horizontal movement of the grass.


#### Stem Radius


**[Stem radius](../../../../content/materials/library/grass_base/index.md#parameter_stem_radius)** is a coefficient to scale an amplitude of vertical movement of the grass.


#### Stem Scale


**[Stem scale](../../../../content/materials/library/grass_base/index.md#parameter_stem_scale)** is a coefficient to scale the speed of grass movement.


### Ambient Occlusion Parameters


![](parameters_ao.png)


#### Visibility


**Visibility** specifies how the AO has influence on grass.


#### Multiplier


**Multiplier** is a coefficient to scale the occlusion that sets shading starting from the ground to the top of the grass blades. The higher the value, the less shaded the grass is.


#### Power


**Power** is the rate of ambient occlusion appearance on the grass.


#### Impact On Diffuse


**Impact On Diffuse** shows how ambient occlusion affects the grass diffuse texture.


### Noise Parameters


![](parameters_noise.png)


> **Notice:** Available only when **[Noise](#option_noise)** is enabled.


#### Transform


**Transform** specifies spatial noise [texture coordinates transformation](../../../../content/materials/library/grass_base/index.md#transform).


#### Scale


**Scale** is a coefficient to scale intensity of the [spatial noise texture](#texture_noise).

![](noise_scale_0.jpg) ![](noise_scale_1.jpg)


### Auxiliary Parameters


![](parameters_auxiliary.png)


#### Auxiliary Color


**Color** is a color for the auxiliary rendering pass.

> **Notice:** Available only when **[Auxiliary](#option_auxiliary)**state is enabled.


#### Visibility Mask Threshold


**Visibility Mask Threshold** determines the threshold of the [visibility mask texture](#texture_visibility_mask).

> **Notice:** Available only when **[Visibility Mask](#option_visibility_mask)** option is enabled.
