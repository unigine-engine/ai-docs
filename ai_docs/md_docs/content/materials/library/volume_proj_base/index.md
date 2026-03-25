# volume_proj_base


A *volume_proj_base* material is used to create light beams from directional light sources, such as car headlights, searchlights or beacon light. It is applied to the [Volume Projected](../../../../objects/effects/volumetrics/volume_proj.md) objects only.


![Volume Proj Material](projected.jpg)

*Volume Proj Material*


## States


![](states_tab.png)

*Material Settings, States Tab*


### Soft Interaction


Allows to avoid visual artifacts (such as sharp edges) when the volume projected object intersects other objects. The volume object fades out to the intersection plane. Colors of the volume projected object and the object are smoothly interpolated in case they are approximately of the same depth value.

![](interaction.jpg) ![](no_interaction.jpg)


## Textures


![](textures_tab.png)

*Material Settings, Textures Tab*


### Base Textures


#### Diffuse Texture


A diffuse map that is used to create a light beam. The texture is 3-channelled (RGB).


#### Attenuation Texture


An attenuation texture that specifies how the object fades out from the center (the left side of the texture) to the edges (the right side of the texture).


| ![Attenuation texture 1](attenuation_texture_0.jpg) | ![Attenuation texture 2](attenuation_texture_1.jpg) |
|---|---|
| ![Attenuation example 1](attenuation_0.jpg) | ![Attenuation example 2](attenuation_1.jpg) |
| *The same object with two different attenuation textures.* |  |


The texture is 4-channelled (RGBA).


## Parameters


![](parameters_tab.png)

*Material Settings, Parameters Tab*


### Base Parameters


#### Diffuse


A color picker to choose the color of the volume.

![](diffuse_0.jpg) ![](diffuse_1.jpg)


#### Diffuse Scale


Multiplier for the [diffuse color](#parameter_diffuse) of the volume. The higher the value, the brighter the diffuse color is.


### Soft Interaction


This option allows to control the volume projected object intensity when it is close or intersects other objects.

- By the minimum value of **0.5**, the whole volume projected object is rendered faded out to prevent any sharp edges between it and the intersected object.
- By higher values, only the intersection edge between the volume projected object and another object is smoothed. The rest of the volume projected object is rendered in full brightness.


![](interaction_0.jpg) ![](interaction_1.jpg)


> **Notice:** The parameter is available only when the *[Soft Interaction](#state_soft_interaction)* state is enabled.


### Transformation Parameters


> **Notice:** For more details on setting texture coordinates, read the [Texture Coordinates Transformation](../../../../content/materials/library/mesh_base/index.md#texture_transform) chapter.


#### Attenuation


Transformation of the *V* coordinate of the attenuation texture. For a default texture, changing this option doesn't affect the volume proj, since a simple gradient is used.


![V coordinate of the attenuation texture](../volume_omni_base/attenuation_transform_v.png)

*V coordinate of the attenuation texture*
