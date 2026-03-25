# Volume Omni


*Volume Omni* is used to create a visible volume of light emitted from a flat surface, for example, embedded wall lights, flat ceiling lights or fluorescent lamps. Only a *[volume_omni](../../../content/materials/library/volume_omni_base/index.md)* material can be assigned to it.


![Volume Omni objects](omni_light.jpg)

*Volume Omni objects*


*Volume Omni* is rendered in the following way: in the center there is a flat rectangle. It simulates a surface that emits light. Around its edges, there are billboards that always face the camera. They create a light volume around the surface even when you look on the omni from the side, and make the volume fade out smoothly. When you look at the object at 90 degrees, it is not visible at all.


![Fading out of Volume Omni](omni_rotate.gif)

*Fading out of Volume Omni at different angles*


### See also


- The *[ObjectVolumeOmni](../../../api/library/objects/class.objectvolumeomni_cpp.md)* class to edit *Volume Omni* objects via API


## Creating a Volume Omni Object


To create a *Volume Omni* object, perform the following steps:


1. On the Menu bar, click *Create -> Volume -> Omni*. ![](volume_omni_create.png)
2. Place the *Volume Omni* object somewhere in the world.
3. Specify the *Volume Omni* object [parameters](#volume_omni_parameters).


## Volume Omni Parameters


In the *Volume Omni* section (*[Parameters](../../../editor2/node_parameters/index.md)* window -> *Node* tab), you can adjust the following parameters of *Volume Omni*:


![](volume_omni_params.png)


| Edit Size | Toggles the editing mode for the *Volume Omni* node. When enabled, the *Volume Omni* sides that can be resized are highlighted with the colored rectangles. To change the size of a side, drag the corresponding rectangle. ![](editing_volume_omni.jpg) |
|---|---|
| Width | Width of the central rectangle in units (along the X axis). |
| Height | Height of the central rectangle in units (along the Y axis). |
| Radius | Size of *Billboards* around the edges in units. |
| Attenuation | Specifies how fast object fades out when viewed from the side. - By the minimum value of **0**, *Volume Omni* doesn't fade out. It abruptly disappears when you look at *Volume Omni* at 90 degrees. - The higher the value is, the more faded out *Volume Omni* is at a small viewing angle. High values also decrease overall intensity. |
