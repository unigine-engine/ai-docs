# billboards_impostor_base


The **billboards_impostor_base** material is used for [impostors](../../../../editor2/tools/impostors_creator/index.md). This material can be used for project optimization to replace a *[Cluster](../../../../objects/objects/mesh_cluster/index.md)* object with *[ObjectBillboards](../../../../objects/objects/billboards/index.md)*.


## States


The States tab contains the following settings and options:


![States](states.png)

*Material Settings, States tab*


### Deferred Buffers


**Deferred Buffers** enables rendering of the material into the [deferred buffers](../../../../principles/render/sequence/index.md#opaque_deferred). If a material is transparent, information about it is not written into the deferred buffers by default. Enabling this state for a transparent material allows this material to [write into deferred buffers](../../../../principles/render/sequence/index.md#forward_buffers) and, therefore, to participate in post effects.


### Lerp


**Lerp** enables smooth linear interpolation of sprites when the camera rotates around the object. Linear interpolation should be enabled if grabbed impostor textures store low number of frames (i.e., *Phi* and *Theta* values are small). The following options are available:


- **Disabled** - linear interpolation between the sprites is disabled.
- **Lerp Unoptimized** - legacy linear interpolation mode (interpolation is calculated during the depth pre-pass, making it three times slower than the mode below).
- **Lerp With Separate Opacity Map** - optimized linear interpolation mode using an additional *[Opacity Lerp Map](../../../../editor2/tools/impostors_creator/index.md#opacity_lerp_map)*).


Selecting the last item in the list activates an additional [opacity lerp map](#texture_opacity_lerp_map).


### Lerp Mode


Linear interpolation mode to be used, one of the following:


- **Full** - sprites are interpolated horizontally and vertically.
- **Horizontal Only** - sprites are interpolated only horizontally, vertically switching is used, this mode can be used for example if we do not fly above the impostors, but rather move around them.


### Lerp Fix Blur


This option helps making details of impostor images look sharper and less blurred reducing the negative effect of linear interpolation.


> **Notice:** **Lerp Fix Blur** mostly improves the look of impostors generated for vegetation, or can be used for sprites having some irregular patterns. It should be disabled for sprites having geometry patterns, like bricks and so on.


### Options


#### AO Map


**AO Map** enables the ambient occlusion effect. This effect is used to modulate global environment illumination using baked shadows from environment probes. Enabling the option activates the [ambient occlusion texture](#texture_ao).


#### Shading Map


**Shading Map** enables the [shading texture](#texture_base_shading) for the material.


#### Specular Map


**Specular Map** enables using of the B channel of the [shading texture](#texture_base_shading) as a specular reflection intensity map.


#### Microfiber Map


**Microfiber Map** enables using of the Alpha channel of the [shading texture](#texture_base_shading) as a microfiber map.


#### Translucent Map


**Translucent Map** activates an additional [translucent texture](#texture_translucent).


#### Depth Map


**Depth Map** activates an additional [depth texture](#texture_depth).


### Post Processing


#### SSAO


**SSAO** enables the [Screen-Space Ambient Occlusion](../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssao/index.md) effect.


#### SSR


**SSR** enables the [Screen-Space Reflections](../../../../editor2/settings/render_settings/ssr/index.md) effect.


#### SSSSS


**SSSSS** enables the [Screen-Space Subsurface Scattering](../../../../editor2/settings/render_settings/sss/index.md) effect.


#### DOF


**DOF** enables the [Depth of Field](../../../../editor2/settings/render_settings/camera_effects/index.md#dof) effect.


#### Motion Blur


**Motion Blur** enables the [Motion Blur](../../../../editor2/settings/render_settings/camera_effects/index.md#motion_blur) effect.


#### Screen-Space Shadows


**Screen-Space Shadows** enables the Screen-Space Shadows effect.


## Textures


The Textures tab allows setting textures for billboards:


| ![](textures.png) |
|---|
| *Material Settings, Textures tab* |


### Base Textures


The following base texture types are available:


#### Albedo Texture


The albedo texture specifies the color of the impostor surface. To create an albedo texture for an impostor, use the [Impostors Creator](../../../../editor2/tools/impostors_creator/index.md) tool: the texture is set automatically after generation.


The texture is 4-channelled (*RGBA*):

1. *RGB* values store color information.
2. *Alpha (A)* value stores transparency information.


#### Shading Texture


The shading texture is a container for four different textures:

- *R* channel stores the *[metalness](../../../../content/materials/library/mesh_base/index.md#texture_metalness_channel)* texture.
- *G* channel stores the *[roughness](../../../../content/materials/library/mesh_base/index.md#texture_roughness_channel)* texture.
- *B* channel stores the *[specular](../../../../content/materials/library/mesh_base/index.md#texture_specular_channel)* texture.
- *A* channel stores the *[microfiber](../../../../content/materials/library/mesh_base/index.md#texture_microfiber_channel)* texture. > **Notice:** The texture from this channel can be used only if the [Microfiber Map](#option_microfiber) option is enabled.


#### Normal Texture


**[Normal](../../../../content/materials/library/mesh_base/index.md#texture_normal)** texture. To create a normal texture for an impostor, use the [Impostors Creator](../../../../editor2/tools/impostors_creator/index.md) tool: the texture is set automatically after generation.


### Optional Textures


#### Ambient Occlusion Texture


Ambient occlusion texture modulates the global environment illumination, for example, when an object is lighter at the top from the sky above, and darker at the bottom from the ground below. The texture uses only *R* channel.


#### Translucent Texture


Translucent texture stores information on the material's translucency. For example, by using this texture, it is possible to specify parts of the object that aren't translucent (the *[Translucent](#parameter_translucent)* parameter won't affect them).


The texture is 1-channelled.


#### Depth Texture


Depth texture stores information on the material's depth.


The texture is 1-channelled.


#### Opacity Lerp Map


This texture is used for smooth linear interpolation of sprites when the camera rotates around the object avoiding abrupt switching between the sprites. [Linear interpolation](#option_lerp) based on this texture is performance-friendly, as it is performed during the deferred pass. To create a texture for an impostor, use the [Impostors Creator](../../../../editor2/tools/impostors_creator/index.md) tool: the texture is set automatically after generation.


The texture is 4-channelled.


> **Notice:** This texture is available only if **[Lerp](#option_lerp)** is enabled.


## Parameters


This tab represents parameters available for the material. All parameters have default values, which can be replaced with your own. Availability of some parameters can depend on the values set in the *States* tab.


| ![](parameters.png) |
|---|
| *Material Settings, Parameters tab* |


### Base Parameters


#### Material Mask


**Material mask** is a decal bit mask. If the material mask of a decal material matches the material mask of the surface material, the decal is projected onto the surface.


#### Base Parameters


> **Notice:** By default, all parameters are set to 1.0. You should adjust them to achieve the required result.


##### Albedo


**Albedo** is a multiplier of the base color of the surface provided by the [albedo texture](#texture_base_albedo).


##### Metalness


**Metalness** is a multiplier of metalness.


##### Roughness


**Roughness** is a multiplier of the roughness of a surface.


##### Specular


**Specular** is a multiplier for the intensity of highlight provided by the [specular texture](#texture_base_shading).


##### Microfiber


**Microfiber** is a coefficient to scale the intensity of microfiber (provided by the [microfiber texture](#texture_base_shading)). The higher the value, the higher the microfiber texture effect is.


##### Translucent


**Translucent** is a scale of the translucency effect, which allows the light to pass through the object, but diffuses it, so objects on the opposite side are not clearly visible.


##### Shadow Offset


**Shadow Offset** sets an offset of impostors shadows.


##### Normal Intensity


**Normal Intensity** is a coefficient to scale the intensity of normals (provided by the [normal map](#texture_base_normal)). The higher the value, the higher the normal texture effect is.


#### Transform Parameters


This group of parameters determines coordinates transformation of impostors.


| ![](parameters_transform.png) |
|---|
| *Transform Parameters* |


##### Phi


**Phi** determines the number of frames grabbed into the impostor texture when the camera rotates horizontally around the object.

| ![](../../../../editor2/tools/impostors_creator/phi_0.png) *Phi = 4* |
|---|
| ![](../../../../editor2/tools/impostors_creator/phi_1.png) *Phi = 8* |


##### Theta


**Theta** determines the number of frames grabbed into the impostor texture when the camera rotates vertically around the object.

| ![](../../../../editor2/tools/impostors_creator/theta_0.png) | ![](../../../../editor2/tools/impostors_creator/theta_1.png) |
|---|---|
| *Theta = 2* | *Theta = 4* |


##### Size


**Size** of the object for which impostors were grabbed.


##### Aspect


**Aspect ratio** (width/height) of the grabbed images. The aspect affects the size of the impostor texture cell that stores the grabbed frame. For example:

- If you need to grab the impostor for an object which height far exceeds the width (e.g. pine tree, lamp post, etc.), you should use the 4/1 aspect. In this case, the height of the texture cell will be 4 times bigger than the width. For horizontal objects (e.g. fallen pine tree), the 1/4 aspect should be used.
- If the original object's width to height aspect is near 1 (e.g. spherical or cuboid-shaped objects), the 1/1 value should be used.


##### Pivot Offset


**Pivot Offset** is the offset of the pivot point from the center of the object's bounding box.
