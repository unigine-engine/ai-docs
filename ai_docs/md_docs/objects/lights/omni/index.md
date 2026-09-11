# Light Omni


*Light Omni* is a point source emitting light in all directions (360�degrees) and realistically reproducing shadow cast. This type of light serves to simulate light sources with bright center and equal roll-off of intensity. An example of such a light is an ordinary household lightbulb, uncovered and hanging from the ceiling. *Light Omni* proves useful for general lighting purposes in indoor scenes because of its nondirectional qualities.


Please note that as *Light Omni* uses cubemap modulation, the shadowing by this source requires **6 passes** and can be expensive.


*Light Omni* has a variety of [shapes](../../../objects/lights/parameters/index.md#shape) and, therefore, can be used to create *area lights*, for example, realistic interior or street lights.


![](index.png)

*Example scene that usesLight Omni*


### See Also


- The *[LightOmni](../../../api/library/lights/class.lightomni_cpp.md)* class to manage *Light Omni* via API
- The part of the Lighting video tutorial dedicated to [working with *Light Omni*](https://youtu.be/6PNOp963S4U?t=38)


## Adding Light Omni


To add *Light Omni*, do the following:


1. On the Menu bar, click *Create -> Light -> Omni* ![](create_omni.png)
2. Place the light somewhere in the world. ![](add_omni.png)


## Setting Light Omni Parameters


Parameters of *Light Omni* can be adjusted on the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window. Both [common parameters](../../../objects/lights/parameters/index.md) and the parameters specific for the *Light Omni* source are available. The specific ones are described below.


![](light_settings.png)


### Light Settings


| Mode | The type of texture used to define light's distribution: - **IES** � light distibution is defined by the IES profile, a lighting industry standard of describing how the light is cast based on real-world measured light fixtures. ![](ies_comparison.png) *Light Omnisources without and with IES profile* - **Simple** � a cubemap texture is projected by *Light Omni*. Such modulations allow you to re-light the affected scene area in a new way at the same performance cost, create variegated light scattering patterns and, for example, imitate several light sources. ![](cubemap_texture.png) *Cubemap texture* ![](omni_texture_0.png) *Modulation by texture* |
|---|---|
| Texture | A cubemap or *IES* texture projected by *Light Omni*. |


### Shadow Settings


| Enabled | Toggles rendering of shadows produced by this light source on and off. |
|---|---|
| Shadow Side Enabled | *Light Omni* makes shadows to be cast to the six cubemap sides. By default, shadows are cast in all directions: positive and negative X axis, positive and negative Y axis, and positive and negative Z axis. Any direction can be disabled, if necessary. |
