# volume_light_base


A *volume_light_base* material is used to create visible spheres of light around [Omni](../../../../objects/lights/omni/index.md) light sources. It is applied to the [Volume Sphere](../../../../objects/effects/volumetrics/volume_sphere.md) objects.


> **Notice:** The *volume_light_base* material can be assigned to a sphere only: the volume sphere cannot be of an ellipsoid shape. That is why the volume sphere with the volume_light_base material assigned is rendered based on the *X* axis [Radius](../../../../objects/effects/volumetrics/volume_sphere.md#volume_sphere_parameters) value. If its radii along *Y* or *Z* axes are smaller, the object is cut along them.


![Volume Light Material](light.jpg)

*Volume Light Material on Volume Spheres*


## Parameters


![](parameters_tab.png)

*Material Settings, Parameters Tab*


### Base Parameters


#### Diffuse


A color picker to choose the color of the light sphere.

![](diffuse_0.jpg) ![](diffuse_1.jpg)


### Density Parameters


#### Power


Specifies if the light density falls off to the edges of the volume sphere.

- By the value of **1**, light is distributed evenly within the volume sphere.
- If a higher value is set, the light density is decreased at the edges of the volume sphere and increased in its center.


![](diffuse_0.jpg) ![](power_1.jpg)


#### Multiplier


A coefficient to scale the density of the light. This value affects visibility of objects inside the light sphere.
