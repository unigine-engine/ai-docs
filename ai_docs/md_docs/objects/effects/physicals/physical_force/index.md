# Physical Force


A **Physical Force** is a spherical object with a force that is applied to its center and attenuates as follows:


![](force_formula.png)


Here:


| Name | Description |
|---|---|
| *distance* | Distance between the sphere center and the object. |
| *radius* | Radius of the sphere in which the force is applied. |
| *attenuation* | Force attenuation factor. |


All physical bodies and particles that are within the radius of the force are pulled up to or away from the center of the *Physical Force* node. Also the bodies and particles can be [rotated](#rotator) around the center of the *Physical Force* node.


> **Notice:** - The *Physical Force* will affect particles only if their physical mass is nonzero. The [physical mass](../../../../objects/effects/particles/index.md#physical_mass) for the *Particles* object can be set on the *Particles* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window.
> - The *Physical Force* can affect only a *[Cloth](../../../../principles/physics/bodies/cloth/index.md)*, a *[Rope](../../../../api/library/physics/class.bodyrope_cpp.md)*, or a *[Rigid](../../../../principles/physics/bodies/rigid/index.md)* body. If the *Rigid* body is used, a [shape](../../../../principles/physics/shapes/index.md) should be also assigned.


### See also


- The *[PhysicalForce](../../../../api/library/physics/class.physicalforce_cpp.md)* class to manage *Physical Force* nodes via API
- A set of samples located in the `data/samples/physicals` folder:

  - `force_00`
  - `force_01`
- The fragment from the [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=1413s) demonstrating the force effect


## Adding Physical Force


To add a *Physical Force* to the scene via UnigineEditor:


1. [Run](../../../../sdk/projects/index_cpp.md#run) the project with UnigineEditor.
2. On the Menu bar, click *Create -> Physics -> Physical Force*. ![](add_physical_force.png)
3. Click somewhere in the world to place the *Physical Force*. ![](added_physical_force.png)


The new *Physical Force* node will be added to UnigineEditor, and you will be able to edit it via the *Parameters* window. By default, the radius of the node is 1.


## Editing Physical Force


In the *Physical Force* section (*[Parameters](../../../../editor2/node_parameters/index.md)* window -> *Node* tab), you can adjust the following parameters of the *Physical Force*:


![](edit_physical_force.png)


| Edit Size | Toggles the editing mode for the *Physical Force* node. When enabled, the radius of applying the physical force can be changed: each axis is highlighted with the colored circle. To change the radius along the axis, drag the corresponding circle. ![](editing_mode.jpg) |
|---|---|
| Physical Mask | *Physical* mask. The physical mask of the *Physical Force* must [match](../../../../principles/bit_masking/index.md) the *Physical* mask of the physical object. Otherwise, the physical force won't affect the object. |
| Radius | Radius for applying the physical force in units. |
| Attenuation | Attenuation factor indicating how much the physical force decreases when the objects move away from the force center. |
| Attractor | Attraction force applied to objects in the *Physical Force* radius. If a *positive* value is provided, objects will be pulled away from the force point. If a *negative* value is provided, objects will be pulled up to the force point. |
| Rotator | Rotation force that is applied to objects in the *Physical Force* radius. If a *positive* value is provided, objects will be rotated clockwise. If a *negative* value is provided, objects will be rotated counter-clockwise. |
