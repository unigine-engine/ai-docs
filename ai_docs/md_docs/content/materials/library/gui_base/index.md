# gui_base


A *gui_base* material is used for [GUI](../../../../code/gui/index.md) objects.


![](index.jpg)

*ObjectGui with gui_base Material*


## States


![States](states.png)

*Material Settings, States Tab*


### Deferred Buffers


**Deferred Buffers** enables rendering of the material into the [deferred buffers](../../../../principles/render/sequence/index.md#forward_buffers). As the material is transparent, it doesn't write information into deferred buffers by default. Enabling this state allows the material to write into deferred buffers and, therefore, to participate in post effects.


### Options


#### Auxiliary


**Auxiliary** rendering pass is used for writing an additional texture into an auxiliary color buffer. Detail information on the pass can be found in the [Rendering Sequence](../../../../principles/render/sequence/index.md#auxiliary) article. The pass can be used for custom post-process effects.

> **Notice:** Enabling this option activates the additional [Auxiliary parameters](#parameters_auxiliary).


#### Mode


**Mode** specifies the GUI video rendering mode:

- **Default** - a video is rendered as it is.
- **YUV** - a sprite video is rendered in the *YUV* color space.


The following pictures show how the video encoded in YUV format is rendered in different modes:

![](mode_0.jpg) ![](mode_1.jpg)


### Post Processing


#### DOF


**DOF** enables the depth of field effect.


#### Motion Blur


**Motion Blur** enables the motion blur effect.


## Parameters


![](parameters.png)

*Material Settings, Parameters Tab*


### Base Parameters


#### Color


**Color** is a GUI diffuse color.

![](color_0.jpg) ![](color_1.jpg)


### Auxiliary Parameters


#### Auxiliary Color


**Auxiliary Color** is an auxiliary rendering pass constant color.


> **Notice:** The parameter is present only if **[Auxiliary](#option_auxiliary)** is enabled.
