# Trigger


![](../node_trigger.png) **Trigger** is a zero-sized node that has no visual representation and triggers events when:


- It is enabled/disabled (the *Enabled* event is triggered).
- Its transformation is changed (the *Position* event is triggered).


The *Node Trigger* node is usually added as a child node to another node, so that the handler functions were executed on the parent node enabling/disabling or transforming.


> **Notice:** The *Enabled* and *Position* event handlers should be implemented in the World script.


The *Node Trigger* can work with procedurally created *[World Clutter](../../../objects/worlds/world_clutter/index.md)* objects.


The *Node Trigger* can be used, for example, to play a sound of thunder when a lightning flashes: when the lightning node is enabled, the *Enabled* event handler that plays a sound is executed.


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


To edit the *Node Trigger*, select it and go to the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window.


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
