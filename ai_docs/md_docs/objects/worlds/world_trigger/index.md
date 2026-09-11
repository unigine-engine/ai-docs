# World Trigger


Trigger types available in UNIGINE:


| [Node Trigger](../../../objects/nodes/trigger/index.md) | World Trigger | [Physical Trigger](../../../objects/effects/physicals/physical_trigger/index.md) |
|---|---|---|
| **Catches changes in the parent node state** (enabled/disabled, transforms changed) ![](../../triggers_images/node_trigger.png) | **Catches nodes with bounds** entering/leaving the trigger area ![](../../triggers_images/world_trigger.png) | **Catches physical objects** (with [body](../../../principles/physics/bodies/index.md) and [shape](../../../principles/physics/shapes/index.md)) entering/leaving the trigger area (detected by physical contact) ![](../../triggers_images/physical_trigger.png) |
| ![](../../../vr_development/yes.png) **Used with:** Any node except [Dummy Node](../../../objects/nodes/dummy/index.md) | ![](../../../vr_development/yes.png) **Used with:** - All nodes having bounds (such nodes have the **[Triggers Interaction](../../../editor2/node_parameters/transformation_common/index.md#common_params)** option in the Editor interface which should be enabled, **by default it is disabled**) - [Dummy Object](../../../objects/objects/dummy/index.md) with [body](../../../principles/physics/bodies/index.md) | ![](../../../vr_development/yes.png) **Used with:** Physical objects (with [body](../../../principles/physics/bodies/index.md) and [shape](../../../principles/physics/shapes/index.md) assigned), such as: *[Dummy Object](../../../objects/objects/dummy/index.md), [Static Mesh](../../../objects/objects/mesh/index.md), [Skinned Mesh](../../../objects/objects/mesh_skinned/index.md), [Dynamic Mesh](../../../objects/objects/mesh_dynamic/index.md), [Billboards](../../../objects/objects/billboards/index.md)* |
| ![](../../../vr_development/no.png) **Doesn't work with:** - [Dummy Node](../../../objects/nodes/dummy/index.md) | ![](../../../vr_development/no.png) **Doesn't work with:** [Dummy Node](../../../objects/nodes/dummy/index.md), [Node Reference](../../../objects/nodes/reference/index.md), [Node Layer](../../../objects/nodes/layer/index.md), [World Switcher](../../../objects/worlds/world_switcher/index.md), [World Transform Path](../../../objects/worlds/world_transforms/transform_path/index.md), [World Transform Joint](../../../objects/worlds/world_transforms/transform_bone/index.md), [World Expression](../../../objects/worlds/world_expression/index.md) [Dummy Object](../../../objects/objects/dummy/index.md) with no [body](../../../principles/physics/bodies/index.md) assigned | ![](../../../vr_development/no.png) **Doesn't work with:** - Non-physical [objects](../../../objects/objects/index.md) (no [physical body](../../../principles/physics/bodies/index.md) and [shape](../../../principles/physics/shapes/index.md)) - Nodes that are not [objects](../../../objects/objects/index.md) |


**World Trigger** is a cuboid shaped node that triggers events when any node (physical or not) gets inside or outside it. *World Trigger* can detect a node of any type by its [bound](../../../api/library/math/bounds/index.md) and can be used to access node's components and parameters.


**World Triggers** detect only the nodes with *Triggers Interaction* enabled - either in the Editor or via .


![](../../../start/quick_start/pqr/triggers_interaction.png)


> **Notice:** The following "abstract" nodes do not have bounds; therefore, they do not interact with *World Trigger* (regardless of the *Triggers Interaction* option state):
>
>
> - [Dummy Node](../../../objects/nodes/dummy/index.md)
> - [Node Reference](../../../objects/nodes/reference/index.md)
> - [Node Layer](../../../objects/nodes/layer/index.md)
> - [World Switcher](../../../objects/worlds/world_switcher/index.md)
> - [World Transform Path](../../../objects/worlds/world_transforms/transform_path/index.md)
> - [World Transform Bone](../../../objects/worlds/world_transforms/transform_bone/index.md)
> - [World Expression](../../../objects/worlds/world_expression/index.md)
> - *[Dummy Object](../../../objects/objects/dummy/index.md)* (if it has no [body](../../../principles/physics/bodies/index.md) assigned)


![](index.jpg)

*World Triggeraffecting meshes*


### See also


- *[WorldTrigger](../../../api/library/worlds/class.worldtrigger_cpp.md)* class to manage *World Trigger* via API
- A set of samples located in the `data/samples/worlds` folder:

  1. `trigger_01`
  2. `trigger_02`
- Videotutorial on [How To Use World Triggers to Detect Nodes by Their Bounds](../../../videotutorials/how_to/how_to_cs/world_trigger.md)


## Creating a World Trigger


To create *World Trigger* via UnigineEditor:


1. On the Menu bar, choose *Create -> Logic -> World Trigger*. ![](creation.png)
2. Place the node in the scene.


## Editing a World Trigger


In the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window, you can adjust the following parameters of *World Trigger*:


![](parameters.png)

*Nodetab of theWorld Triggernode*


### Bounding Box Parameters


A set of bounding box parameters:


| Edit Size | Toggles the editing mode for the *World Trigger* node on and off. When enabled, the bounding box sides that can be resized are highlighted with the colored rectangles. To change the size of a side, drag the corresponding rectangle. ![](editing_mode.jpg) |
|---|---|
| Touch | Toggles the touch mode for *World Trigger* on and off. With this mode on, *World Trigger* reacts to the node at a partial contact. Otherwise, *World Trigger* reacts only if the whole bounding box gets inside it. |
| Size | The size of the *World Trigger* bounding box along the *X, Y*, and *Z* axes, in units. |


## Handling Events


To perform specific actions when a node enters or leaves the World Trigger, you should implement event handlers that receive a [Node](../../../api/library/nodes/class.node_cpp.md) as the first argument. Then, you should subscribe to the *[Enter](../../../api/library/worlds/class.worldtrigger_cpp.md#getEventEnter_Event)* and/or *[Leave](../../../api/library/worlds/class.worldtrigger_cpp.md#getEventLeave_Event)* events and call *connect()*.


```cpp
// subscribe to the Enter event when a node enters the world trigger with your handler
worldTrigger->getEventEnter().connect(enter_event_handler);
// subscribe to the Leave event when a node leaves the world trigger with your handler
worldTrigger->getEventLeave().connect(leave_event_handler);

```


```csharp
// subscribe to the Enter event when a node enters the world trigger with your handler
worldTrigger.EventEnter.Connect(enter_event_handler);
// subscribe to the Leave event when a node leaves the world trigger with your handler
worldTrigger.EventLeave.Connect(leave_event_handler);

```
