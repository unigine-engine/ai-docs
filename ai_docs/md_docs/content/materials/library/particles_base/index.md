# particles_base


> **Notice:** This article describes only a part of parameters of *Particle Systems* (material-side), the rest of the parameters (that belong to the node) are described in the *[Particle Systems](../../../../objects/effects/particles/index.md)* article.


A `particles_base` material is used for [particles](../../../../objects/effects/particles/index.md). This material supports [particles animation](#anim_texture).


[![](particles_base_sm.png)](particles_base.png)


## Parameters


### Base


![](base_params.png)


| Albedo | Albedo texture that defines the particle appearance. ![](diffuse.jpg) The texture is 4-channeled (RGBA): - *RGB* values store a color of the texture. - The *Alpha (A)* channel contains the transparency value. The texture can also store an [animation](#anim_texture) atlas that is used to play animated particles, for example burning fire: ![](fire_middle_d.png) *Texture containing animation atlas* One more way of using the texture atlas is to pick a random image from it for each particle. In this case, the [Texture Atlas](../../../../objects/effects/particles/index.md#texture_atlas) option should be enabled. |  |  |  |  |
|---|---|---|---|---|---|
| Albedo Color Type | The mode of setting the [Albedo Color](#albedo_color): - **Color** � the color is selected using the color picker and is unchanged during the particle life time. - **Curve** � the color is set using the [curve](../../../../editor2/curve_editor/index.md) that defines its changes during the particle life time. |  |  |  |  |
| Albedo Color | Color multiplier for the [Albedo](#texture_albedo) texture. \| ![](diffuse_color_yellow.png) \| ![](diffuse_color_green.png) \| \|---\|---\| \| *Albedo Color = Yellow* \| *Albedo Color = Green* \| | ![](diffuse_color_yellow.png) | ![](diffuse_color_green.png) | *Albedo Color = Yellow* | *Albedo Color = Green* |
| ![](diffuse_color_yellow.png) | ![](diffuse_color_green.png) |  |  |  |  |
| *Albedo Color = Yellow* | *Albedo Color = Green* |  |  |  |  |
| Animation | Toggle it on if the [Albedo](#texture_albedo) texture contains a texture with atlas animation. Enabling this parameter makes two additional parameters available: - **Animation Size** � the atlas texture size. - **Animation Scale** � the time scale for the animation. > **Notice:** Fine-tuning of animation may require enabling the [Motion Vectors](#motion_vectors) option. |  |  |  |  |
| Material Mask | A [bit mask](../../../../principles/bit_masking/index.md#material_mask) used by decals. If the material mask of the decal material matches the particle material, the decal is projected. |  |  |  |  |
| Normal | Texture to store information about a surface's normals deviation. Becomes available, if the [Normal Map](#normal_map) or [Refraction](#refraction_pass) parameter is enabled. ![](normal.jpg) The texture is 2-channeled (RG): - *RG* values contain two components of a normal - The third component's value is calculated from the given components in run-time > **Notice:** **Unigine Engine** expects a normal map in *DirectX* format. If your normal map is in *OpenGL* format, tick *[Invert G Channel](../../../../editor2/assets_workflow/texture_import.md#invert_g)* in the import menu. As a general rule, if the lighting seems weird, try inverting the G Channel and see if it gets better. |  |  |  |  |
| Disable Underwater Rendering | Disables rendering of particles underwater. |  |  |  |  |


### Normal Map


![](normal_off.png) ![](normal_on.png)


Normal map is used to make flat particles look like spatial objects. Enabling this parameter makes available two additional settings:


![](param_normal_map.png)


- [**Normal**](#normal_texture) texture in the [Base parameters](#parameters_base) section
- **Intensity** of the normal texture


### Refraction


![](param_refraction.png)


**Refraction** specifies if the material should be rendered during the refraction pass. Surfaces are rendered during this pass only if they are transparent.


| ![](refraction_on.png) | ![](refraction_off.png) |
|---|---|
| *Refraction pass is enabled for particles in the center* | *Refraction pass is disabled for particles in the center* |


Enabling this state makes the [**Normal**](#normal_texture) texture in the [Base parameters](#parameters_base) section available.


Refraction has the **Scale** parameter � a coefficient to scale the refraction area.

- By the value of **0** there is no refraction of light for the material.
- The higher the positive value, the more distorted the image behind the refracting material is.
- Negative values invert the direction of distortion: the lower the negative value, the bigger the distortion is.


| ![](refraction_on.png) | ![](refraction_scale_high.png) |
|---|---|
| *Scale = 0.6* | *Scale = 2* |


### Transparent Blur


![](param_transparent_blur.png)


Enables rendering of the transparent blur effect that can be used to create a heat haze effect typical for hot air.


> **Notice:** *Rendering -> Transparent -> Blur* option must be enabled.


![](transparent_blur_off_sm.jpg) ![](transparent_blur_on_sm.jpg)


Transparent blur is fine-tuned via two parameters:


| Intensity | Degree of blurring. |
|---|---|
| Texture | Four-channel texture to create a specific blur pattern. |


### Soft Interaction


![](soft_interaction_off.png) ![](soft_interaction_on.png)


This option allows adjusting interaction of volumetric particles with other objects to avoid sharp cutting of particles by objects the particles interact with. The particles color is reduced depending on their position relative to the object:

- If the depth value specifies that the particles are in front or behind the object, they are rendered as usual.
- If the depth value between the particle and the object is small, the color is smoothly interpolated.


![](param_soft_interaction.png)


The **Intensity** parameter is a depth factor that controls the particles color lessening depending on their position relative to the object:

- *Decreasing* the value results in rendering in full color of the particles that are positioned far from the objects.
- By **0** value, the depth value is considered to be infinite and thus no particles are rendered. All of them are interpolated with the environment.
- *Increasing* the value results in rendering of more closely positioned particles in full color. The interpolated area lessens.


### Motion Vectors


![](param_motion_vectors.png)


This option allows making smoother animation for sprite-to-sprite transitions of the [texture atlas](#texture_albedo) for [animated](#anim_texture) particles. If disabled, the particle images are linearly interpolated in animation.


![](motion_vector_off_on.gif)


| Texture | RG texture that contains motion vectors. The result will be especially spectacular if you use particle texture atlases with high-resolution sprites and low number of frames. Such textures can be generated in EmberGen or Houdini. > **Notice:** - Do not enable [Mipmaps sRGB Correction](../../../../editor2/assets_workflow/texture_import.md#mipmap_correction) when importing the texture. > - In some cases it may be required to [Invert G Channel](../../../../editor2/assets_workflow/texture_import.md#invert_g) for correct rendering. |
|---|---|
| Scale | The multiplier for the motion vector offset. |
| Type | Algorithm that defines how the motion vectors are used. - **To Current** � the previous frame is moved to the current frame using the motion vectors. - **Opposite Sides** � the previous and the next frame are moved to the current one using the motion vectors. |
| Jitter | Jittering of the image in the direction of the motion vector. |
| Motion Blur | Blurring of the image in the direction of the motion vector. |
| Current Frame Offset | Offset of the current frame in the motion vector texture. |
| Next Frame Offset | Offset of the next frame in the motion vector texture. |


### Lighting


![](param_lighting.png)


| Ambient | **Ambient** specifies if the material should be rendered during the ambient light pass. Note that only transparent surfaces will be rendered. |
|---|---|
| Light Omni | **Light Omni** specifies if the material should be rendered illuminated by the *Omni* light sources during the [shadow maps rendering](../../../../principles/render/sequence/index.md#shadow_maps_omni). Note that only transparent surfaces will be rendered. |
| Light Proj | **Light Proj** specifies if the material should be rendered illuminated by the *Projected* light sources during the [shadow maps rendering](../../../../principles/render/sequence/index.md#shadow_maps_proj). Note that only transparent surfaces will be rendered. |
| Light World | **Light World** specifies if the material should be rendered illuminated by the *World* light sources during the [shadow maps rendering](../../../../principles/render/sequence/index.md#shadow_maps_world). Note that only transparent surfaces will be rendered. |
| Use Voxel Probe | Specifies whether the particle system is affected by lighting baked into [Voxel Probes](../../../../objects/lights/voxelprobe/index.md). |
| Environment Scale | **Environment Scale** is a multiplier for ambient lighting. ![](environment_0.png) ![](environment_1.png) |
| Diffuse Scale | A coefficient to scale the brightness of the [Albedo](#texture_albedo) texture. The higher the value, the brighter the albedo texture is. ![](diffuse_scale_0.png) ![](diffuse_scale_1.png) |


### Emission


![](emission_0.png) ![](emission_1.png)


![](param_emission.png)


| Emission Texture | Texture used for the light emitting. |
|---|---|
| Emission Scale | **Emission Scale** is a multiplier for the material's emission. |
| Emission Color Type | The mode of setting the [Emission Color](#emission_color): - **Color** � the color is selected using the color picker. - **Curve** � the color is selected using the [curve](../../../../editor2/curve_editor/index.md). |
| Emission Color | Color multiplier for the [Emission](#emission_texture) texture. |


### Translucent


![](param_translucent.png)


| Translucent Texture | The 1-channeled texture that defines which portions of the [Albedo](#texture_albedo) texture are translucent and which are not. |
|---|---|
| Translucent Scale | Translucency coefficient that controls the extent of light diffusion inside the particles object. With a higher value, more light can penetrate through particles. |
| Translucent Depth | The coefficient that fine-tunes the depth of the shadow inside the particles volume. ![](translucent_depth_1.png) ![](translucent_depth_4.png) |


### Shadows


![](param_shadows.png)


| Receive Shadows | Specifies if polygons, to which the material is applied, receive shadows from omni, projected or cubemap (environment probe) light sources. |
|---|---|
| Receive World Shadows | Specifies if polygons, to which the material is applied, receive shadows from world light sources. |
| Transparent Shadow | Makes shadows look like they are cast by translucent objects. > **Notice:** This feature is available for transparent materials only. |
| Lerp Cascades | Toggles linear interpolation of shadows cascades on and off. When enabled, transitions between cascades become smoother. However, the option drops performance, because two shadow maps are rendered in the transition parts. > **Notice:** For this feature to work properly, linear interpolation of shadow cascades should be [enabled globally](../../../../editor2/settings/render_settings/shadows/index.md#lerp_shadow_cascades) (via *Rendering -> Shadows -> Lerp Shadow Cascades*). |
| Filter Mode | Filtering mode to be used for shadows from all light sources cast on the material. This mode determines the quality of soft shadows reducing the stair-step effect. Higher quality produces smoother shadows. Available values: - **Disabled** � filtering for shadows is disabled, the stair-step effect is clearly seen at the edges of shadows. - **Low** � low quality - **Medium** � medium quality - **High** � high quality - **Ultra** � ultra quality > **Notice:** This parameter is similar to the [global shadow filtering mode](../../../../editor2/settings/render_settings/shadows/index.md#filter_mode) (*Settings -> Render -> Shadows*), but is used for transparent objects on a per-material basis. |
| Penumbra Mode | Quality mode to be used for rendering penumbra from all light sources cast on the material. This mode enables simulation of real-world shadows by keeping sharp contact shadows closer to the base and softening the farther the shadow stretches away. Higher quality produces softer shadows. Available values: - **Disabled** � penumbra rendering is disabled, shadow edges are crisp and sharp (no shadow softness at all). - **Low** � low quality - **Medium** � medium quality - **High** � high quality - **Ultra** � ultra quality > **Notice:** This parameter is similar to the [global shadow penumbra mode](../../../../editor2/settings/render_settings/shadows/index.md#penumbra_mode) (*Settings -> Render -> Shadows*), but is used for transparent objects on a per-material basis. |
| Filter Noise | Toggles the use of noise for shadow filtering on and off. This noise is used for smoothing shadows cast on the material and reducing the stair-step effect at the edges of shadows. > **Notice:** This parameter is similar to the [global shadow filter noise](../../../../editor2/settings/render_settings/shadows/index.md#filter_noise) (*Settings -> Render -> Shadows*), but is used for transparent objects on a per-material basis. |
| Penumbra Noise | Toggles the use of noise for penumbra rendering on and off. This noise is used for smoothing soft shadows cast on the material. > **Notice:** This parameter is similar to the [global shadow penumbra noise](../../../../editor2/settings/render_settings/shadows/index.md#penumbra_noise) (*Settings -> Render -> Shadows*), but is used for transparent objects on a per-material basis. |
| Softness Multiplier | Multiplier for smoothing the edges of shadows cast by particles. |
| Shadow Threshold | Threshold for the alpha component for shadows. > **Notice:** Not available for opaque particles. |
| Shadow Offset | Fine-tuning of the distance between the shadow and the object that casts this shadow. |


### Deferred Buffers


![](param_deferred_buffers.png)


Enabling **Deferred Buffers** makes the material to be rendered during the [deferred pass](../../../../principles/render/sequence/index.md#opaque_deferred).

> **Notice:** This parameter is available for transparent particles only.


| Deferred Threshold | Threshold for the alpha component for the deferred pass. If the alpha component is greater than this value, the particle will be written into the deferred buffer. |
|---|---|


### Auxiliary


![](param_auxiliary.png)


**Auxiliary** specifies if the material should be rendered into the [auxiliary color buffer](../../../../principles/render/sequence/index.md#auxiliary) to create a custom post-process effect.


| Auxiliary Color | Color picker to choose an auxiliary color for the [Auxiliary rendering pass](../../../../principles/render/sequence/index.md#auxiliary). |
|---|---|
| Auxiliary Threshold | Threshold for the alpha component for the auxiliary pass. If the alpha component is greater than this value, the particle will be written into the auxiliary buffer. |
