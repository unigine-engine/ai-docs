# Sky


**Sky** is an object used to recreate the atmosphere in the scene. It is modelled as an upper hemisphere of the specified color, tiled with clouds textures to produce plausible and inexpensive dynamic clouds. It can also have any cube map as a background picture.


![](index_sm.png)


### See Also


- The *[sky_base](../../../content/materials/library/sky_base/index.md)* material to adjust the sky appearance
- The *[ObjectSky](../../../api/library/objects/class.objectsky_cpp.md)* class to edit the sky via API


## Creating Sky


To create the sky, perform the following steps:


1. On the Menu bar, click *Create -> Sky -> Sky*. ![](create.png)
2. Place the sky object somewhere in the world.
3. Specify the [sky parameters](#parameters).


### Sky Parameters


| Spherical | Create the spherical sky dome. If the option is disabled, only the upper hemisphere will be created. > **Notice:** The sky is represented as the sky dome. To avoid the visual artifacts of the apparent curvature caused by applying the clouds texture, sphere is recommended to be flattened a bit (for detailed information see the *[sky_base](../../../content/materials/library/sky_base/index.md)* material). |
|---|---|
