# volume_fog_base


A *volume_fog_base* material is used to create fog, haze or mist that hides objects behind it. It is applied to [Volume Box](../../../../objects/effects/volumetrics/volume_box.md) and [Volume Sphere](../../../../objects/effects/volumetrics/volume_sphere.md) objects.


![Fog material with Volume box](fog.jpg)

*Fog Material with Volume box*


## States


![](states_tab.png)

*Material Settings, States Tab*


### Height


Specifies if the fog fades out to the top of its volume.

![](height_0.jpg) ![](height_1.jpg)


### Use Sky Color


If enabled, the sky color is used as a multiplier for the fog's [diffuse](#parameter_diffuse) color.


## Parameters


![](parameters_tab.png)

*Material Settings, Parameters Tab*


### Base Parameters


#### Diffuse


A color picker specifying the diffuse color.

![](height_1.jpg) ![](diffuse_1.jpg)


### Density Parameters


#### Power


Specifies if the fog density falls off to the edges of the volume box. If the [Height](#state_height) state is enabled, it also affects the density.

- By the minimum value of **1**, fog is distributed evenly within the volume box.
- If a higher value is set, the fog density reduces at the edges of the object and increases in the center.


![](power_0.jpg) ![](power_1.jpg)


#### Multiplier


A coefficient to scale a density of the fog. This value affects visibility of objects inside the fog:

- By low values, only distant objects are hidden by the fog.
- By high values, even close objects are not visible in the fog.


![](multiplier_0.jpg) ![](multiplier_1.jpg)


#### Height Falloff


Specifies the fog intensity depending on height.

> **Notice:** The parameter is available only when the *[Height](#state_height)* state is enabled.


![](falloff_0.jpg) ![](falloff_1.jpg)
