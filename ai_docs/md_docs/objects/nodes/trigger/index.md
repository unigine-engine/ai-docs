# Node Trigger


Trigger types available in UNIGINE:


| Node Trigger | [World Trigger](../../../objects/worlds/world_trigger/index.md) | [Physical Trigger](../../../objects/effects/physicals/physical_trigger/index.md) |
|---|---|---|
| **Catches changes in the parent node state** (enabled/disabled, transforms changed) ![](../../triggers_images/node_trigger.png) | **Catches nodes with bounds** entering/leaving the trigger area ![](../../triggers_images/world_trigger.png) | **Catches physical objects** (with [body](../../../principles/physics/bodies/index.md) and [shape](../../../principles/physics/shapes/index.md)) entering/leaving the trigger area (detected by physical contact) ![](../../triggers_images/physical_trigger.png) |
| ![](../../../vr_development/yes.png) **Used with:** Any node except [Dummy Node](../../../objects/nodes/dummy/index.md) | ![](../../../vr_development/yes.png) **Used with:** - All nodes having bounds (such nodes have the **[Triggers Interaction](../../../editor2/node_parameters/transformation_common/index.md#common_params)** option in the Editor interface which should be enabled, **by default it is disabled**) - [Dummy Object](../../../objects/objects/dummy/index.md) with [body](../../../principles/physics/bodies/index.md) | ![](../../../vr_development/yes.png) **Used with:** Physical objects (with [body](../../../principles/physics/bodies/index.md) and [shape](../../../principles/physics/shapes/index.md) assigned), such as: *[Dummy Object](../../../objects/objects/dummy/index.md), [Static Mesh](../../../objects/objects/mesh/index.md), [Skinned Mesh](../../../objects/objects/mesh_skinned/index.md), [Dynamic Mesh](../../../objects/objects/mesh_dynamic/index.md), [Billboards](../../../objects/objects/billboards/index.md)* |
| ![](../../../vr_development/no.png) **Doesn't work with:** - [Dummy Node](../../../objects/nodes/dummy/index.md) | ![](../../../vr_development/no.png) **Doesn't work with:** [Dummy Node](../../../objects/nodes/dummy/index.md), [Node Reference](../../../objects/nodes/reference/index.md), [Node Layer](../../../objects/nodes/layer/index.md), [World Switcher](../../../objects/worlds/world_switcher/index.md), [World Transform Path](../../../objects/worlds/world_transforms/transform_path/index.md), [World Transform Joint](../../../objects/worlds/world_transforms/transform_bone/index.md), [World Expression](../../../objects/worlds/world_expression/index.md) [Dummy Object](../../../objects/objects/dummy/index.md) with no [body](../../../principles/physics/bodies/index.md) assigned | ![](../../../vr_development/no.png) **Doesn't work with:** - Non-physical [objects](../../../objects/objects/index.md) (no [physical body](../../../principles/physics/bodies/index.md) and [shape](../../../principles/physics/shapes/index.md)) - Nodes that are not [objects](../../../objects/objects/index.md) |


![](../node_trigger.png) **Node Trigger** is a zero-sized node that has no visual representation and triggers events when:


- It is enabled/disabled (the *Enabled* event is triggered).
- Its transformation is changed (the *Position* event is triggered).


*Node Trigger* node is usually added as a child node to another node, so that the handler functions were executed on the parent node enabling/disabling or transforming.


> **Notice:** The *Enabled* and *Position* event handlers should be implemented in the World script.


*Node Trigger* can work with procedurally created *[World Clutter](../../../objects/worlds/world_clutter/index.md)* objects.


*Node Trigger* can be used, for example, to play a sound of thunder when a lightning flashes: when the lightning node is enabled, the *Enabled* event handler that plays a sound is executed.


![](node_trigger_usage.jpg)

*Lightning node enabled*


### See also


- The *[NodeTrigger](../../../api/library/nodes/class.nodetrigger_cpp.md)* class to edit triggers via API
- Video tutorial on [How To Use Node Triggers to Detect Changes in Node States](../../../videotutorials/how_to/how_to_cs/node_trigger.md)


## Adding a Node Trigger


To add a new *Node Trigger* via UnigineEditor do the following:


1. In UnigineEditor, on the Menu bar, click *Create -> Logic -> Node Trigger*. ![](trigger_create.png)
2. Place the *Node Trigger* in the world. ![](add_trigger_node.png)
3. Add the *Node Trigger* as a child to a node for which handlers should be executed: select the *Node Trigger* in the *[World Nodes Hierarchy](../../../editor2/organizing_nodes/index.md)* window and drag it inside the required node. ![](trigger_child.gif)


## Editing a Node Trigger


To edit *Node Trigger*, select it and go to the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window.


![](edit_trigger_node.png)

*Node Triggersettings*


## Handling Events


Editing a trigger node includes implementing and specifying the *Enabled* and *Position* event handlers that are executed on enabling or positioning the *Trigger* node correspondingly.


The event handler must receive at least **1** argument of the *NodeTrigger* type. In addition, it can also take another 2 arguments of any type.


The event handlers are set via pointers specified when subscribing to the following events: *[Enabled](../../../api/library/nodes/class.nodetrigger_cpp.md#getEventEnabled_Event)* and *[Position](../../../api/library/nodes/class.nodetrigger_cpp.md#getEventPosition_Event)*.


```cpp
// subscribe to the Enabled event when the trigger is enabled
nodeTrigger->getEventEnabled().connect(enabled_event_handler);
// subscribe to the Position event when the trigger's transformation is changed
nodeTrigger->getEventPosition().connect(position_event_handler);

```


```csharp
// subscribe to the Enabled event when the trigger is enabled
nodeTrigger.EventEnabled.Connect(enabled_event_handler);
// subscribe to the Position event when the trigger's transformation is changed
nodeTrigger.EventPosition.Connect(position_event_handler);

```
