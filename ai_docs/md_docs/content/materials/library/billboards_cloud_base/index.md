# billboards_cloud_base


A *billboards_cloud_base* material is used to create independent small clouds via [Billboards](../../../../objects/objects/billboards/index.md).


[![Clouds Billboards](index_sm.jpg)](index.jpg)

*Billboard clouds*


## States


In this tab you can set available settings and options:


![States](states.png)

*Material Editor,billboards_cloud_basematerial,Statestab.*


- **[Axis x](#axis_x)** - lock a billboard along *X* axis.
- **[Axis z](#axis_z)** - lock a billboard along *Z* axis.
- **[Screen](#screen)** - set billboards perpendicularly to each other.


#### axis_x


Locks billboards orientation along *X* axis (by default billboards always face the camera).


| ![](axis_x_0.png) | ![](axis_x_1.png) |
|---|---|
| *Disabledaxis_x* | *Enabledaxis_x* |


#### axis_z


Locks billboards orientation along *Z* axis (by default billboards always face the camera). Billboards can be also locked along both *X* and *Z* axes, so they will be oriented perpendicularly to *Y* axis.


| ![](axis_z_0.png) | ![](axis_z_1.png) |
|---|---|
| *Enabledaxis_z* | *Enabled bothaxis_xandaxis_z* |


#### screen


Set billboards parallel to each other. If they are not axes-locked, they will be oriented strictly towards to the screen plane.


| ![](axis_x_0.png) | ![](screen_0.png) |
|---|---|
| *Disabledscreen* | *Enabledscreen* |


### Options


- **[Soft interaction](#soft_interaction)** - soft interaction with objects.


#### Soft interaction


Enables soft interaction for billboards and objects, so the interactions would not be sharp and cause artifacts.


| ![](soft_interaction_0.png) | ![](soft_interaction_1.png) |
|---|---|
| *DisabledSoft interaction* | *EnabledSoft interaction* |


## Textures


In this tab you can choose textures for billboards:


| ![](textures.png) |
|---|
| *Material editor,Texturestab.* |


### Base


Base textures:


- **[Diffuse](../../../../content/materials/library/mesh_base/index.md#texture_diffuse)** - diffuse texture.


## Parameters


This tab represents parameters available for the material. All of the parameters have set default values, which can be replaced by your own ones. Availability of some parameters can depend on the set *States* tab values.


| ![](parameters.png) |
|---|
| *Material editor,Parameterstab.* |


Transformation parameters:


- **[Base](../../../../content/materials/library/mesh_base/index.md#texture_transform)** - material coordinates transformation.


Other parameters:


- **[Color 0](#cloud_0_color)** - main color of the cloud.
- **[Color 1](#cloud_0_color)** - color of the cloud shadow.
- **Multiplier** - diffuse texture intensity scale.
- **cloud_scattering** - scattering value.
- **[Distance](#cloud_distance)** - near clipping distance value.


Soft interaction parameters:


- **[Soft interaction](#interaction)** - [interaction](#soft_interaction) value.


### Color 0 and Color 1


Color pickers choosing the main color and the color for shadowed parts of the cloud.


An example of the cloud colors configuration:


| ![](color_0.png) | ![](color_1.png) | ![](color_2.png) |
|---|---|---|
|  |  |  |


### cloud_scattering


A slider setting the scattering value for clouds. The higher the value the more visible the clouds are.


| ![](scattering_0.png) | ![](scattering_1.png) | ![](scattering_2.png) |
|---|---|---|
| *Scattering= 0.1* | *Scattering= 0.2* | *Scattering= 0.3* |


### Distance


A slider setting the near clipping distance, starting with which billboards are rendered.


### Soft Interaction


A slider setting interaction value for clouds. The higher the value, the closer to the object clouds are rendered.


| ![](interaction_0.png) | ![](interaction_1.png) | ![](interaction_2.png) |
|---|---|---|
| *Interaction= 10* | *Interaction= 40* | *Interaction= 100* |


> **Notice:** A parameter is present only if a **[Soft interaction](#soft_interaction)** option is enabled.
