# Light Projected


*Light Projected* is a light source that casts light from a single point forming a focused beam aimed in a specific direction. This type of light is visualized in a form of a pyramid. Due to its form, it is versatile and can be conveniently used to simulate the numerous light emitting sources: for example, car headlights, flash light, or street lamps.


*Light Projected* can produce shadows of accurate perspective projection. They require only a single rendering pass and are performance-cheap if compared to [World Light](../../../objects/lights/world/index.md) and [Omni Light](../../../objects/lights/omni/index.md).


As the *Light Projected* can have different [shapes](../../../objects/lights/parameters/index.md#shape), it can be used to create *area lights*.


![](index.png)

*Example scene that usesLight Projected*


### See Also


- The *[LightProj](../../../api/library/lights/class.lightproj_cpp.md)* class to manage *Light Projected* via API
- The part of the Lighting video tutorial dedicated to [working with *Light Projected*](https://youtu.be/6PNOp963S4U?t=151)


## Adding Projected Light


To add *Light Projected*, do the following:


1. On the Menu bar, click *Create -> Light -> Projected* ![](create_proj.png)
2. Place the light somewhere in the world. ![](add_proj.png)


## Setting Projected Light Parameters


Parameters of *Light Projected* can be adjusted in the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window. It contains both the [common parameters](../../../objects/lights/parameters/index.md) and the parameters specific for *Light Projected* source. The specific ones are described below.


![](parameters.png)


### Light Settings


| Field of view | A field of view of *Light Projected*. This parameter defines the angle of the light clipping in range from 1 (only a very narrow segment is illuminated) to 175 degrees (the whole hemisphere is lit). \| [![](proj_fov_0_sm.png)](proj_fov_0.png) *Field of view = 20* \| [![](proj_fov_1_sm.png)](proj_fov_1.png) *Field of view = 65* \| [![](proj_fov_2_sm.png)](proj_fov_2.png) *Field of view = 90* \| \|---\|---\|---\| | [![](proj_fov_0_sm.png)](proj_fov_0.png) *Field of view = 20* | [![](proj_fov_1_sm.png)](proj_fov_1.png) *Field of view = 65* | [![](proj_fov_2_sm.png)](proj_fov_2.png) *Field of view = 90* |  |  |  |
|---|---|---|---|---|---|---|---|
| [![](proj_fov_0_sm.png)](proj_fov_0.png) *Field of view = 20* | [![](proj_fov_1_sm.png)](proj_fov_1.png) *Field of view = 65* | [![](proj_fov_2_sm.png)](proj_fov_2.png) *Field of view = 90* |  |  |  |  |  |
| Mode | The type of texture used to define light distribution: - **IES** � light distibution is defined by the IES profile, a lighting industry standard of describing how the light is cast based on real-world measured light fixtures. ![](ies_comparison.png) *Light Projectedwithout and with IES profile* - **Simple** � an arbitrary 2D texture is projected onto the scene. All the surfaces receiving the formed light pattern are redrawn in additional rendering pass, this is required because of manipulations with texture matrix. \| ![](texture_0.png) \| ![](texture_1.png) \| \|---\|---\| \| ![](proj_texture_0.png) \| ![](proj_texture_1.png) \| \| *1st texture projected* \| *2nd texture projected* \| | ![](texture_0.png) | ![](texture_1.png) | ![](proj_texture_0.png) | ![](proj_texture_1.png) | *1st texture projected* | *2nd texture projected* |
| ![](texture_0.png) | ![](texture_1.png) |  |  |  |  |  |  |
| ![](proj_texture_0.png) | ![](proj_texture_1.png) |  |  |  |  |  |  |
| *1st texture projected* | *2nd texture projected* |  |  |  |  |  |  |
| Texture | A simple or IES texture projected by *Light Projected*. |  |  |  |  |  |  |
| Relative to FOV | The IES texture rendering mode: - Disabled � the unchanged IES texture is clipped by the light source's [Field of View](#light_settings). - Enabled � the IES texture is scaled to fit within the light source's Field of View. |  |  |  |  |  |  |


### Attenuation Settings


| Penumbra | A light penumbra is used to simulate edge gradual falloff. This parameter determines how fast the intensity decreases from the center of spot to the non-illuminated areas border. - If the attenuation power is set to 0 or close to it, the edge between illuminated and non-illuminated areas will be sharp. - *Increasing* the value up will render softly dispersed light at the non-illuminated areas border. \| ![](proj_penumbra_0.png) *Penumbra = 0* \| ![](proj_penumbra_1.png) *Penumbra power = 1* \| ![](proj_penumbra_2.png) *Penumbra power = 5* \| \|---\|---\|---\| | ![](proj_penumbra_0.png) *Penumbra = 0* | ![](proj_penumbra_1.png) *Penumbra power = 1* | ![](proj_penumbra_2.png) *Penumbra power = 5* |
|---|---|---|---|---|
| ![](proj_penumbra_0.png) *Penumbra = 0* | ![](proj_penumbra_1.png) *Penumbra power = 1* | ![](proj_penumbra_2.png) *Penumbra power = 5* |  |  |
