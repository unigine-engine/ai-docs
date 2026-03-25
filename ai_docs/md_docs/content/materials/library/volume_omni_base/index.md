# volume_omni_base


A *volume_omni_base* material is used to create a visible light volume around flat light emitters: embedded wall lights, flat ceiling lights or fluorescent lamps. They are applied to the [Volume Omni](../../../../objects/effects/volumetrics/volume_omni.md) objects only.


## States


![](states_tab.png)

*Material Settings, States Tab*


### Soft Interaction


Reduces visual artifacts (such as sharp edges) when the Volume Omni object intersects other objects. The volume object fades out to the intersection plane. Colors of the volume omni object and the object are smoothly interpolated in case they are approximately of the same depth value.


| ![Interaction disabled](interaction_0.jpg) | ![Interaction enabled](interaction_1.jpg) |
|---|---|
| *Disabled Interaction* | *Enabled Interaction* |


## Textures


![](textures_tab.png)

*Material Settings, Textures Tab*


### Attenuation Texture


Attenuation map. A texture that specifies how the object fades out from the center (the left side of the texture) to the edges (the right side of the texture).


| ![Attenuation texture 1](texture_0.jpg) | ![Attenuation texture 2](texture_1.jpg) |
|---|---|
| ![Omni volume object with a texture 1](attenuation_0.jpg) | ![Omni volume object with a texture 2](attenuation_1.jpg) |
| *Fading out near the edges depends on the attenuation texture* |  |


The texture is 3-channelled (RGB).


## Parameters


![](parameters_tab.png)

*Material Settings, Parameters Tab*


### Base Parameters


#### Diffuse


A color picker to choose the color of the volume.


#### Diffuse Scale


Multiplier for the [diffuse color](#parameter_diffuse) of the volume. The higher the value, the brighter the diffuse color is.


### Soft Interaction


This option allows to control the intensity of the volume omni object when it is close or intersects other objects.

- By the minimum value of **0.5**, the whole volume omni is rendered faded out to prevent any sharp edges between it and the intersected object.
- By higher values, only the intersection edge between volume omni and another object is smoothed. The rest of the volume omni is rendered in full brightness.


> **Notice:** The parameter is available only when the *[Soft Interaction](#state_soft_interaction)* state is enabled.


### Transformation Parameters


> **Notice:** For more details on setting texture coordinates, read the [Texture Coordinates Transformation](../../../../content/materials/library/mesh_base/index.md#texture_transform) chapter.


#### Attenuation


Transformation of the *V* coordinate of the attenuation texture. For a default texture, changing this option doesn't affect the volume omni, since a simple gradient is used.


![V coordinate of the attenuation texture](attenuation_transform_v.png)

*V coordinate of the attenuation texture*
