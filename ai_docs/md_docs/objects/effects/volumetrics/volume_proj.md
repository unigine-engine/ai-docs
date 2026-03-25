# Volume Projected


The *Volume Projected* object is used to create light beams from directional light sources, such as car headlights, searchlights or beacon light. It can also be animated to simulate a flow of particles that moves from the light source or even swirls. Only a *[volume proj](../../../content/materials/library/volume_proj_base/index.md)* material can be assigned to it.


![Volume Projected objects](proj_light.jpg)

*Volume Projected objects*


*Volume Projected* is rendered as a simple particle system. It is a number of *Billboards*, where each following *Billboard* is bigger than the previous one.


![Billboards of a Volume Projected object](proj_wireframe.jpg)

*Billboards of a Volume Projected object*


### See also


- The *[ObjectVolumeProj](../../../api/library/objects/class.objectvolumeproj_cpp.md)* class to edit *Volume Projected* objects via API


## Creating a Volume Projected Object


To create a *Volume Projected* object, perform the following steps:


1. On the Menu bar, click *Create -> Volume -> Projected*. ![](volume_proj_create.png)
2. Place the *Volume Projected* object somewhere in the world.
3. Specify the *Volume Projected* object [parameters](#volume_proj_parameters).


## Volume Projected Parameters


![Options](proj_options.gif)

*Parameters*


In the *Volume Projected* section (*[Parameters](../../../editor2/node_parameters/index.md)* window -> *Node* tab), you can adjust the following parameters of the *Volume Projected* object:


![](volume_projected_params.png)


| Size | Size of the smallest *Billboard* in units. By the minimum value of **0**, *Volume Projected* is not rendered at all. |
|---|---|
| Radius | Length of the light beam along the Z axis, in units. |
| FOV | Width of the light beam. It is specified as the angle of the beam cone (in degrees). - By the minimum value of **10**, the beam is the narrowest. - By the maximum value of **90**, the beam is the widest. |
| Step | Distance between neighboring *Billboards*. - The lower the step is, the smoother the beam, since more *Billboards* are rendered. - The higher the step, the more discrete the beam, but the higher the performance is. |
| Velocity | Velocity with which *Billboards* move to the end of the beam (along the Z axis). |
| Rotation | Angle of *Billboards* rotation (in degrees). This angle is set for the *Billboard* at the end of the beam. - If positive, all *Billboards* rotate clockwise. - If negative, all *Billboards* rotate counterclockwise. ![Positive rotation angle](proj_rotation.gif) *Positive rotation angle* |
