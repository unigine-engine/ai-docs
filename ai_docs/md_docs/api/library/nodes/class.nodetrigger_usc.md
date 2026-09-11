# Unigine::NodeTrigger Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


A *[Trigger](../../../objects/nodes/trigger/index.md)* node is a zero-sized node that has no visual representation and triggers events when:


- It is enabled/disabled (the *Enabled* event is triggered).
- Its transformation is changed (the *Position* event is triggered).


The *Trigger* node is usually added as a child node to another node, so that the handler functions were executed on the parent node enabling/disabling or transforming.


For example, to detect if some node has been enabled (for example, a world clutter node that renders nodes only around the camera that has enabled it), the *Trigger* node is added as a child to this node and executes the corresponding function.


### Creating a Trigger Node


To create a *Trigger* node, simply call the NodeTrigger [constructor](#NodeTrigger) and then add the node as a child to another node, for which handlers should be executed.


```cpp
#include <core/unigine.h>

int init() {

	NodeTrigger trigger;
	ObjectMeshStatic object;

	// create a node (e.g. an instance of the ObjectMeshStatic class)
	object = new ObjectMeshStatic("core/meshes/box.mesh");
	// change material albedo color
    object.setMaterialParameterFloat4("albedo_color", vec4(1.0f, 0.0f, 0.0f, 1.0f), 0);
	// release script ownership
	node_remove(object);

	// create a trigger node
	trigger = new NodeTrigger();
	node_remove(trigger);
	// add it as a child to the static mesh
	object.addWorldChild(trigger);

	return 1;
}

```


### Editing a Trigger Node


Editing a trigger node includes implementing and specifying the *Enabled* and *Position* event handlers that are executed on enabling or positioning the *Trigger* node correspondingly.


### See Also


- Video tutorial on [How To Use Node Triggers to Detect Changes in Node States](../../../videotutorials/how_to/how_to_cs/node_trigger.md)
- Article on [Event Handling](../../../code/fundamentals/events/index.md#triggers)
- C++ sample
- C# Component sample


## NodeTrigger Class

### Members

## getEventPosition () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEnabled () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## static NodeTrigger ( )

Constructor. Creates a new trigger node.
## void setEnabledCallbackName ( string name )

Sets a callback function to be fired when the trigger node is enabled. The callback function can take no arguments, a *[Node](../../../api/library/nodes/class.node_usc.md)*or a *NodeTrigger*.
> **Notice:** The method allows for setting a callback with **0** or **1** argument only.


```cpp
// implement the enabled callback
void enabled_callback(Node node) {
	log.message("The enabled flag is %d\n", node.isEnabled());
}

NodeTrigger trigger;

int init() {

	// create a trigger node
	trigger = new NodeTrigger();
	// set the enabled callback to be fired when the node is enabled/disabled
	trigger.setEnabledCallbackName("enabled_callback");

	return 1;
}

```


### Arguments

- *string* **name** - Name of the callback function implemented in the world script (UnigineScript side).

## string getEnabledCallbackName ( )

Returns the name of callback function to be fired on enabling the trigger node. This callback function is set via *[setEnabledCallbackName()](#setEnabledCallbackName_cstr_void)*.
### Return value

Name of the callback function implemented in the world script (UnigineScript side).
## void setPositionCallbackName ( string name )

Sets a callback function to be fired when the trigger node position has changed. The callback function can take no arguments or a *[Node](../../../api/library/nodes/class.node_usc.md)*or a *NodeTrigger* as the first argument.
> **Notice:** The method allows for setting a callback with **0** or **1** argument only.


```cpp
// implement the position callback
void position_callback(Node node) {
	log.message("A new position of the node is %s\n", typeinfo(node.getWorldPosition()));
}

NodeTrigger trigger;

int init() {

	// create a trigger node
	trigger = new NodeTrigger();
	// set the position callback to be fired when the node position is changed
	trigger.setPositionCallbackName("position_callback");

	return 1;
}

```


### Arguments

- *string* **name** - Name of the callback function implemented in the world script (UnigineScript side).

## string getPositionCallbackName ( )

Returns the name of callback function to be fired on changing the trigger node position. This function is set by using the *[setPositionCallbackName()](#setPositionCallbackName_cstr_void)*function.
### Return value

Name of the callback function implemented in the world script (UnigineScript side).
