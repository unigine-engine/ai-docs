# volume_cloud_base


The *volume_cloud_base* material is used to create clouds or shaped fog. It is applied to [Volume Box](../../../../objects/effects/volumetrics/volume_box.md) objects.


![Volume Cloud Material](cloud.gif)

*volume_cloud_base material*


## States


![](states_tab.png)

*Material Settings, States tab*


### Samples


Defines how many times a [density](#texture_density) texture is sampled to render a cloud. The higher the value, the smoother and less discrete the cloud is. To increase performance, use low **Samples** values combined with a higher [Jitter](#parameter_jitter) value.

![](samples_0.png) ![](samples_1.png)


### Attenuation


If enabled, the [attenuation texture](#texture_attenuation) is used to define the cloud color.


### Use Sky Color


If enabled, the sky color is used as a multiplier for the cloud's [diffuse](#parameter_diffuse) color.


### Options


#### Soft Interaction


Enables soft interaction for volume boxes and other objects, so that the interactions would not be sharp and cause artifacts. A volume object fades out to the intersection plane: the color of the volume box and the object is smoothly interpolated in case they are approximately of the same depth value.


## Textures


![](textures_tab.png)

*Material Settings, Textures tab*


Use of the texture depends on the [Attenuation](#states) state: if disabled, the density texture is used, if enabled�the attenuation texture is used for the cloud.


### Base Textures


#### Density Texture


Specifies the shape of the cloud and its density. It is a 3D texture that represents a set of vertical cross-sections of the cloud.


The texture is 4-channelled (RGBA):


- *RGB* values store the color of the texture.
- *A* value stores transparency values.


#### Attenuation Texture


The *R* value of the Density texture is used to identify the *U* coordinate of the attenuation texture, which sets a color:


- The minimum value of **0** means U coordinate value is **0**.
- The maximum value of **255** means U coordinate value is **1**. ![U coordinate of the attenuation texture](attenuation_u.png) *U coordinate of the attenuation texture.*


All other values of the texture are ignored.


## Parameters


In the *Parameters* tab, you can set or modify base and additional parameters.


![](parameters_tab.png)

*Material Settings, Parameters Tab*


### Transformation Parameters


> **Notice:** For more details on setting texture coordinates, read the [Texture Coordinates Transformation](../../../../content/materials/library/mesh_base/index.md#texture_transform) chapter.


#### Attenuation


*V* coordinate of the [attenuation texture](#texture_attenuation) coordinates transformation.


![Attenuation Coordinates](attenuation_v.png)

*V coordinate of the attenuation texture.*


#### Scale


Coordinate transformation of the [density](#texture_density) texture. UnigineScript expressions can be used in this field.

![](scale_0.png) ![](scale_1.png)


#### Offset


An offset of the [density texture](#texture_density) along *X*, *Y*, and *Z* axes respectively. UnigineScript expressions can be used in this field.


### Base Parameters


#### Diffuse


A color picker to choose the diffuse color.

![](diffuse_0.png) ![](diffuse_1.png)


### Density Parameters


#### Multiplier


A coefficient to scale the density of the cloud.

- By the minimum value of **0**, the cloud is not rendered at all.
- The higher the value, the thicker the cloud is (if a default texture is used).


![](multiplier_0.png) ![](multiplier_1.png)


### Jitter


This parameter determines smoothness of the cloud with a small number of samples. The higher the value, the smoother the cloud is.

![](jitter_0.png) ![](jitter_1.png)


### Volume Power


Specifies if the cloud density reduces from the edges of the volume box to its center. The higher the value, the more the cloud reduces.


![](volume_power.gif)
