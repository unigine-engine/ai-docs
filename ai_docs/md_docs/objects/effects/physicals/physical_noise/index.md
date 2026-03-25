# Physical Noise


A **Physical Noise** is a cuboid shaped area that adds a distribution flow based on a volumetric noise texture. The *Physical Noise* enables to simulate a force field that affects particles and physical bodies with a spatial 3D noise.


> **Notice:** The physical noise can affect only a *[Cloth](../../../../principles/physics/bodies/cloth/index.md)*, a *[Rope](../../../../api/library/physics/class.bodyrope_cpp.md)*, or a *[Rigid](../../../../principles/physics/bodies/rigid/index.md)* body. Also you should remember that a *Rigid* body requires a [shape](../../../../principles/physics/shapes/index.md) to be assigned.


For example, if you add the physical noise for particles, you can get the following:


| [![](noise_disabled_sm.png)](noise_disabled.png) *Noise is disabled* | [![](noise_enabled_sm.png)](noise_enabled.png) *Noise is enabled. A colored square is a noise image texture* |
|---|---|


> **Notice:** The *Physical Noise* will affect particles only if their physical mass is nonzero. The [physical mass](../../../../objects/effects/particles/index.md#physical_mass) for the particles can be set on the *Particles* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window.


### See also


- The *[PhysicalNoise](../../../../api/library/physics/class.physicalnoise_cpp.md)* class to edit *Physical Noise* nodes via API
- The `data/samples/physicals/noise_00` sample
- The fragment from the [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=1433s) demonstrating the noise effect


## Main Concepts


> **Notice:** The calculations described below are added for better understanding of the [parameters](#edit_physical) of the *Physical Noise* .


The direction of the force, which affects particles and physical bodies inside the *Physical Noise* box, is stored in the **Noise** texture: a 3D texture, each texel of which stores force direction. The noise texture that is used for the *Physical Noise* can be [adjusted](#noise_texture_params) via UnigineEditor.


When the physical body falls within the *Physical Noise* box, the force at the current point starts to affect it. This force is calculated as follows:


![](formula_noise.png)


Here:


| Name | Description |
|---|---|
| *force* | The resulting force that affects the physical body at the current point |
| *force_direction* | Direction of the force vector that is stored in the color of a texel of the noise texture |
| *force_multiplier* | [Force multiplier](#force_multiplier) |
| *threshold* | [Threshold distance](#threshold) along the axes |


The *force_direction* is obtained from the noise texture as follows:


![](formula_force.png)


As the *force_direction* is a vector, the calculation is actually performed as follows:


![](formula_force_full.png)


The *pixel_color* is obtained by sampling a pixel with the given coordinates from the noise texture. The pixel coordinates are calculated as follows:


![](formula_pixel.png)


Here:


| Name | Description |
|---|---|
| *pixel_color* | Color of the noise texture pixel that stores direction of the force vector |
| *pixel_coordinates* | Coordinates of the noise texture pixel that stores direction of the force vector |
| *body_position* | Local coordinates of the physical body (relative to coordinates of the *Physical Noise* node) |
| *step* | [Sampling Step](#texture_sampling_parameters) |
| *offset* | [Sampling Offset](#texture_sampling_parameters) |
| *threshold* | [Threshold Distance](#threshold) along the axes |


## Adding Physical Noise


To add a *Physical Noise* to the scene via UnigineEditor:


1. [Run](../../../../sdk/projects/index_cpp.md#run) the project with UnigineEditor.
2. On the Menu bar, click *Create -> Physics -> Physical Noise*. ![](add_physical_noise.png)
3. Click somewhere in the world to place the *Physical Noise*. ![](added_physical_noise.png)


A new *Physical Noise* node will be added to UnigineEditor, and you will be able to edit it via the *Parameters* window.


## Editing Physical Noise


In the *Physical Noise* section (*[Parameters](../../../../editor2/node_parameters/index.md)* window -> *Node* tab), you can adjust parameters of the *Physical Noise*.


> **Notice:** To have a more clear understanding how the following parameters affect the resulting force inside the *Physical Noise* node, see [*Main Concepts*](#main_concepts).


![](edit_physical_noise.png)


### Node Parameters


The following parameters are used to set conditions of the size of the *Physical Noise* node.


| Edit Size | Toggles the editing mode for the *Physical Noise* node. When enabled, the *Physical Noise* box sides that can be resized are highlighted with the colored rectangles. To change the size of a side, drag the corresponding rectangle. ![](editing_mode.png) |
|---|---|
| Physical Mask | *Physical* mask. The physical mask of the *Physical Noise* must [match](../../../../principles/bit_masking/index.md) the *Physical* mask of the physical object. Otherwise, the physical noise won't affect the object. |
| Size | Size of the *Physical Noise* box along the axes in units. |
| Threshold | Threshold distance along the axes. The threshold determines the distance of gradual change from zero to full force value. These values are relative to the size of the *Physical Noise* box. It means that the threshold values should be less than the size of the *Physical Noise* box. ![](../threshold.png) |


### Texture Sampling Parameters


The following parameters are used for pixel sampling from the generated noise texture.


> **Notice:** You can animate a force field in run-time by changing these parameters.


| Offset | Sampling offset along the axes. |
|---|---|
| Step | Size of the sampling step along the axes. |


### Force Multiplier


| Force | Force multiplier. The higher the value is, the higher the value of the resulting force that affects an object inside the *Physical Noise* node will be. |
|---|---|


### Texture Generation Parameters


The following parameters are used to generate a noise texture that will be used at run time.


> **Notice:** It is not recommended to change values of the following parameters at run time as the noise texture will be regenerated and the performance will decrease.


| Scale | Scale of the noise texture. The minimum value is 0, the maximum value is 1. |  |  |  |  |
|---|---|---|---|---|---|
| Frequency | Number of octaves for the Perlin noise. The higher the value is, the more details the noise texture has. The minimum value is 0, the maximum value is 16. \| ![](noise_frequency_1.png) \| ![](noise_frequency_16.png) \| \|---\|---\| \| *Frequency = 1* \| *Frequency = 16* \| | ![](noise_frequency_1.png) | ![](noise_frequency_16.png) | *Frequency = 1* | *Frequency = 16* |
| ![](noise_frequency_1.png) | ![](noise_frequency_16.png) |  |  |  |  |
| *Frequency = 1* | *Frequency = 16* |  |  |  |  |
| Image Size | Size of the noise texture image in pixels. |  |  |  |  |
