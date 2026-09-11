# Physical Water


The **Physical Water** is a cuboid shaped area inside which water interaction effects are simulated. The *Physical Water* is usually used with [*water objects*](../../../../objects/objects/water/index.md): you can add the *Physical Water* node together with a *Water* node to indicate an area where physical interactions will take place. Note, however, that you cannot simulate waves by using the *Physical Water*.


> **Notice:** The water will affect only objects, to which the *[Cloth](../../../../principles/physics/bodies/cloth/index.md)* body or the *[Rigid](../../../../principles/physics/bodies/rigid/index.md)* body are assigned. If the *Rigid* body is used, a [shape](../../../../principles/physics/shapes/index.md) should be also assigned. However, *Cloth* bodies cannot float in the *Physical Water*: they can only go with the water flow.


Also it is possible to generate particles in the contacts between the *Rigid* bodies and the *Physical Water* (in order to create, for example, foam on the water or water splashes). This requires that the *ObjectParticles* node must be added as a child node to the *Physical Water* node.


> **Notice:** You cannot generate particles in the contact between the water and the *Cloth* body, since these bodies cannot float in the water.


Bodies with different physical properties behave differently in the same *Physical Water*. Therefore, in addition to editing [*Physical Water* parameters](#edit_physical), you should adjust parameters of the physical body in order to get the expected result.


Physical bodies of objects participating in the contact with a *Physical Water* can be obtained via code. Also you can get the depth of the object submergence, the force applied to the contact, coordinates of the contact point and the relative velocity between the object and the *Physical Water*.


By using the *Physical Water*, you can create, for example, flows in the ocean.


### See also


- The *[PhysicalWater](../../../../api/library/physics/class.physicalwater_cpp.md)* class to manage *Physical Water* nodes via API
- A set of samples located in the `data/samples/physicals` folder:

  - `water_00`
  - `water_01`
- The fragment from the [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=1460s) demonstrating the *Physical Water* effect.


## Adding Physical Water


To add a *Physical Water* to the scene via UnigineEditor:


1. [Run](../../../../sdk/projects/index_cpp.md#run) the project with UnigineEditor.
2. On the Menu bar, click *Create -> Water -> Physical Water*. ![](add_physical_water.png)
3. Click somewhere in the world to place the *Physical Water*. ![](added_physical_water.png)


A new *Physical Water* node will be added to UnigineEditor, and you will be able to edit it via the *Parameters* window. By default, the size of the node is 1�1�1 unit.


## Editing Physical Water


In the *Physical Water* section (*[Parameters](../../../../editor2/node_parameters/index.md)* window -> *Node* tab), you can adjust the following parameters of the *Physical Water*:


![](edit_physical_water.png)


| Edit Size | Toggles the editing mode for the *Physical Water* node. When enabled, the *Physical Water* box sides that can be resized are highlighted with the colored rectangles. To change the size of a side, drag the corresponding rectangle. ![](../physical_noise/editing_mode.png) |  |  |  |  |
|---|---|---|---|---|---|
| Physical Mask | *Physical* mask. The physical mask of the *Physical Water* must [match](../../../../principles/bit_masking/index.md) the *Physical* mask of the physical object. Otherwise, the *Physical Water* won't affect the object. |  |  |  |  |
| Size | Size of the *Physical Water* box along the axes in units. |  |  |  |  |
| Velocity | Velocity of the flow in the *Physical Water* along the axes. |  |  |  |  |
| Density | Density of the *Physical Water*. It determines buoyancy of objects that float in the *Physical Water*. The higher the value, the higher is the buoyancy of the object. The lower the water density, the deeper the object submerges into water. > **Notice:** The [density](../../../../principles/physics/bodies/index.md#density) and the [mass](../../../../principles/physics/bodies/index.md#mass) of the physical body also affect buoyancy of the object. \| ![](water_density_10.png) \| ![](water_density_25.png) \| \|---\|---\| \| *Physical Water density = 10* \| *Physical Water density = 25* \| | ![](water_density_10.png) | ![](water_density_25.png) | *Physical Water density = 10* | *Physical Water density = 25* |
| ![](water_density_10.png) | ![](water_density_25.png) |  |  |  |  |
| *Physical Water density = 10* | *Physical Water density = 25* |  |  |  |  |
| Linear Damping | Value indicating how much the linear velocity of the objects decreases when they get into the *Physical Water*. The higher the value is, the lower the linear velocity will be. |  |  |  |  |
| Angular Damping | Value indicating how much the angular velocity of the objects decreases when they get into the *Physical Water*. The higher the value is, the lower the angular velocity will be. |  |  |  |  |
