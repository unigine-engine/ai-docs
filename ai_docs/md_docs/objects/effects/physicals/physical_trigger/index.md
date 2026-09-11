# Physical Trigger


Trigger types available in UNIGINE:


| [Node Trigger](../../../../objects/nodes/trigger/index.md) | [World Trigger](../../../../objects/worlds/world_trigger/index.md) | Physical Trigger |
|---|---|---|
| **Catches changes in the parent node state** (enabled/disabled, transforms changed) ![](../../../triggers_images/node_trigger.png) | **Catches nodes with bounds** entering/leaving the trigger area ![](../../../triggers_images/world_trigger.png) | **Catches physical objects** (with [body](../../../../principles/physics/bodies/index.md) and [shape](../../../../principles/physics/shapes/index.md)) entering/leaving the trigger area (detected by physical contact) ![](../../../triggers_images/physical_trigger.png) |
| ![](../../../../vr_development/yes.png) **Used with:** Any node except [Dummy Node](../../../../objects/nodes/dummy/index.md) | ![](../../../../vr_development/yes.png) **Used with:** - All nodes having bounds (such nodes have the **[Triggers Interaction](../../../../editor2/node_parameters/transformation_common/index.md#common_params)** option in the Editor interface which should be enabled, **by default it is disabled**) - [Dummy Object](../../../../objects/objects/dummy/index.md) with [body](../../../../principles/physics/bodies/index.md) | ![](../../../../vr_development/yes.png) **Used with:** Physical objects (with [body](../../../../principles/physics/bodies/index.md) and [shape](../../../../principles/physics/shapes/index.md) assigned), such as: *[Dummy Object](../../../../objects/objects/dummy/index.md), [Static Mesh](../../../../objects/objects/mesh/index.md), [Skinned Mesh](../../../../objects/objects/mesh_skinned/index.md), [Dynamic Mesh](../../../../objects/objects/mesh_dynamic/index.md), [Billboards](../../../../objects/objects/billboards/index.md)* |
| ![](../../../../vr_development/no.png) **Doesn't work with:** - [Dummy Node](../../../../objects/nodes/dummy/index.md) | ![](../../../../vr_development/no.png) **Doesn't work with:** [Dummy Node](../../../../objects/nodes/dummy/index.md), [Node Reference](../../../../objects/nodes/reference/index.md), [Node Layer](../../../../objects/nodes/layer/index.md), [World Switcher](../../../../objects/worlds/world_switcher/index.md), [World Transform Path](../../../../objects/worlds/world_transforms/transform_path/index.md), [World Transform Joint](../../../../objects/worlds/world_transforms/transform_bone/index.md), [World Expression](../../../../objects/worlds/world_expression/index.md) [Dummy Object](../../../../objects/objects/dummy/index.md) with no [body](../../../../principles/physics/bodies/index.md) assigned | ![](../../../../vr_development/no.png) **Doesn't work with:** - Non-physical [objects](../../../../objects/objects/index.md) (no [physical body](../../../../principles/physics/bodies/index.md) and [shape](../../../../principles/physics/shapes/index.md)) - Nodes that are not [objects](../../../../objects/objects/index.md) |


The **Physical Trigger** is a node that triggers events when physical objects get inside or outside it. There are 4 types of physical triggers based on their shape:


- *Sphere trigger* of the specified radius
- *Capsule trigger* of the specified radius and height
- *Cylinder trigger* of the specified radius and height
- *Box trigger* of the specified size along the axes


To be detected by the trigger, a physical object must have both a [physical body](../../../../principles/physics/bodies/index.md) (with the *[Physical](../../../../principles/bit_masking/index.md#physical_mask)* mask that matches the *Physical* mask of the trigger) and a [shape](../../../../principles/physics/shapes/index.md) (with the *Collision* mask that matches the *[Collision](../../../../principles/bit_masking/index.md#collision_mask)* mask of the trigger).


It is also possible to specify the *[Exclusion](../../../../principles/bit_masking/index.md#exclusion_mask)* mask for the *Physical Trigger* that is used to prevent detecting collisions with shapes. This mask is independent of the *Collision* mask.


- For a body with a shape, the *Exclusion* mask can be set on the *Physics* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* panel.
- For the *Physical Trigger*, the mask can be set via [C++, C# or UnigineScript API](../../../../api/library/physics/class.physicaltrigger_cpp.md#setExclusionMask_int_void).


To **avoid collision detection** between a shape and a *Physical Trigger*, **either** of the following conditions must be met:


- The *Collision* mask set for the shape must [not match](../../../../principles/bit_masking/index.md) the *Collision* mask of the *Physical Trigger*.
- The *Exclusion* mask set for the shape must [match](../../../../principles/bit_masking/index.md) the *Exclusion* mask of the *Physical Trigger*. If the *Exclusion* masks match, the *Collision* masks of these nodes are not taken into account.


Physical objects participating in the contact with the *Physical Trigger* can be obtained via API. The shape of such object scan also be obtained. Moreover, you can get the depth of the object penetration, coordinates of the contact point, and its normal.


### See also


- The *[PhysicalTrigger](../../../../api/library/physics/class.physicaltrigger_cpp.md)* class to manage *Physical Trigger* nodes via API
- A set of samples located in the `data/samples/physicals` folder:

  - `trigger_00`
  - `trigger_01`
  - `trigger_02`
- The fragment from the [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=1482s) demonstrating the *Physical Trigger*
- Videotutorial on [How To Use Physical Triggers to Catch Physical Objects](../../../../videotutorials/how_to/how_to_cs/physical_trigger.md)


## Adding Physical Trigger


To add a *Physical Trigger* to the scene via UnigineEditor:


1. [Run](../../../../sdk/projects/index_cpp.md#run) the project with UnigineEditor.
2. On the Menu bar, click *Create -> Logic -> Physical Trigger*. ![](add_physical_trigger.png)
3. Click somewhere in the world to place the *Physical Trigger*. ![](added_physical_trigger.png)


A new *Physical Trigger* node will be added to UnigineEditor, and you will be able to edit it via the *Parameters* window. By default, the sphere trigger with 1-unit radius is created.


## Editing Physical Trigger


In the *Physical Trigger* section (*[Parameters](../../../../editor2/node_parameters/index.md)* window -> *Node* tab), you can adjust the following parameters of the physical trigger:


![](edit_physical_trigger.png)


| Edit Size | Toggles the editing mode for the *Physical Trigger* node. When enabled, the size or the radius of the node (depending on its [type](#type)) can be changed: each side/axis is highlighted with the colored rectangle/circle. To change the size/radius, drag the corresponding rectangle/circle. ![](editing_mode.png) *Editing of sphere-shaped physical trigger* |
|---|---|
| Physical Mask | The *Physical* mask of the *Physical Trigger* must [match](../../../../principles/bit_masking/index.md) the *Physical* mask of the physical object. Otherwise, the *Physical Trigger* won't trigger events when the object enters or leaves it. |
| Collision Mask | The *Collision* mask of the *Physical Trigger* must [match](../../../../principles/bit_masking/index.md) the *Collision* mask of the physical object's shape. |
| Type | Type of the *Physical Trigger*: *sphere, capsule, cylinder*, or *box*. |
| Size | Size of the *Physical Trigger*, namely: - *Radius* in case of a sphere - *Radius* and *height* in case of a capsule or a cylinder - *Dimensions* in case of a box |


## Handling Events


To perform specific actions when physical objects enter or leave the Trigger, you should create a handler function that receives a *[Body](../../../../api/library/physics/class.body_cpp.md)* as its first argument and implements the desired actions. Then subscribe to the [*Enter*](../../../../api/library/physics/class.physicaltrigger_cpp.md#getEventEnter_Event) and/or [*Leave*](../../../../api/library/physics/class.physicaltrigger_cpp.md#getEventLeave_Event) events and call *connect()*.


```cpp
// subscribe to Enter event when a body enters the physical trigger with your handler
physicalTrigger->getEventEnter().connect(enter_event_handler);
// subscribe to Leave event when a body leaves the physical trigger with your handler
physicalTrigger->getEventLeave().connect(leave_event_handler);

```


```csharp
// subscribe to Enter event when a body enters the physical trigger with your handler
physicalTrigger.EventEnter.Connect(enter_event_handler);
// subscribe to Leave event when a body leaves the physical trigger with your handler
physicalTrigger.EventLeave.Connect(leave_event_handler);

```
