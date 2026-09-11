# Physical Wind


The **Physical Wind** is a cuboid shaped area that simulates the blowing wind inside of it. The wind velocity can [gradually decrease](#threshold) up to box boundaries.


The wind will affect only an object that meets the following requirements:


- The object's bounds must be inside the *Physical Wind* box.
- A [physical body](../../../../principles/physics/bodies/index.md) must be assigned to the object. > **Notice:** The *Physical Wind* can affect only a *[Cloth](../../../../principles/physics/bodies/cloth/index.md)* body or a *[Rigid](../../../../principles/physics/bodies/rigid/index.md)* body. If the *Rigid* body is used, a [shape](../../../../principles/physics/shapes/index.md) should be also assigned.


The wind differently affects objects with different physical properties. Therefore, in addition to editing [*Physical Wind* parameters](#edit_physical), you should adjust parameters of the physical body.


For example, if you place a node, to which the *Cloth* body is assigned, inside the *Physical Wind* node, the node will "wave in the wind" differently depending on the *Cloth* body [mass](../../../../principles/physics/bodies/index.md#mass):


| ![](physicalwind_mass_1.gif) | ![](physicalwind_mass_8.gif) |
|---|---|
| *Wind velocity = (2.0,4.0,2.0); Body mass = 1.0* | *Wind velocity = (2.0,4.0,2.0); Body mass = 8.0* |


### See also


- The *[PhysicalWind](../../../../api/library/physics/class.physicalwind_cpp.md)* class to edit *Physical Wind* nodes via API
- A set of samples located in the `data/samples/physicals` folder:

  1. `wind_00`
  2. `wind_01`
  3. `wind_02`
  4. `wind_03`
  5. `wind_04`
  6. `wind_05`
- The fragment from the [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=1388s) demonstrating creation of the wind.


## Adding Physical Wind


To add a *Physical Wind* to the scene via UnigineEditor:


1. [Run](../../../../sdk/projects/index_cpp.md#run) the project with UnigineEditor.
2. On the Menu bar, click *Create -> Physics -> Physical Wind*. ![](add_physical_wind.png)
3. Click somewhere in the world to place the *Physical Wind* node. ![](added_physical_wind.png)


A new *Physical Wind* node will be added to UnigineEditor, and you will be able to edit it via the *Parameters* window. By default, the size of the node is 1�1�1 unit.


## Editing Physical Wind


In the *Physical Wind* section (*[Parameters](../../../../editor2/node_parameters/index.md)* window -> *Node* tab), you can adjust the following parameters of the *Physical Wind*:


![](edit_physical_wind.png)


| Edit Size | Toggles the editing mode for the *Physical Wind* node. When enabled, the *Physical Wind* box sides that can be resized are highlighted with the colored rectangles. To change the size of a side, drag the corresponding rectangle. ![](../physical_noise/editing_mode.png) |
|---|---|
| Physical Mask | *Physical* mask. The physical mask of the *Physical Wind* must [match](../../../../principles/bit_masking/index.md) the *Physical* mask of the physical object. Otherwise, the *Physical Wind*, inside which the wind flows with the specified velocity, won't affect the object. |
| Size | Size of the *Physical Wind* box along the axes in units. |
| Threshold | Threshold distance along the axes. The threshold determines the distance of gradual change from zero to full wind velocity. These values are relative to the size of the *Physical Wind* box. It means that the threshold values should be less than the size of the *Physical Wind* box. The threshold values form an invisible box, inside which the wind blows with full [velocity](#velocity): ![](../threshold.png) |
| Velocity | Velocity of the *Physical Wind* flow along the axes. |
| Linear damping | Value indicating how much the linear velocity of the objects decreases when they get inside the wind node. The higher the value is, the lower the linear velocity will be. |
| Angular damping | Value indicating how much the angular velocity of the objects decreases when they get inside the wind node. The higher the value is, the lower the angular velocity will be. > **Notice:** *Angular damping* parameter affects only objects with a *[Cloth](../../../../principles/physics/bodies/cloth/index.md)* body assigned. |
