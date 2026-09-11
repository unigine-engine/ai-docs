# Unigine::WorldTrigger Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


### Example


The example below allows creating a line of boxes moving in and out of the World Trigger area and triggering the events. Getting inside the World Trigger enables emission for the boxes, and getting out of it disables the emission.


### See Also


- Video tutorial on [How To Use World Triggers to Detect Nodes by Their Bounds](../../../videotutorials/how_to/how_to_cs/world_trigger.md)
- Article on [Event Handling](../../../code/fundamentals/events/index.md#triggers)
- C++ sample
- C# Component sample
- UnigineScript samples:

  -
  -
  -


## WorldTrigger Class

### Members

## void setLeaveCallbackName ( string name )

Sets a new
### Arguments

- *string* **name** - The name of the handler function name to be executed on leaving the world trigger.

## const char * getLeaveCallbackName () const

Returns the current
### Return value

Current name of the handler function name to be executed on leaving the world trigger.
## void setEnterCallbackName ( string name )

Sets a new name of handler function to be executed on entering the world trigger. This handler function is set via [getEventEnter()](#getEventEnter_Event).
### Arguments

- *string* **name** - The name of the handler function.

## const char * getEnterCallbackName () const

Returns the current name of handler function to be executed on entering the world trigger. This handler function is set via [getEventEnter()](#getEventEnter_Event).
### Return value

Current name of the handler function.
## int getNumNodes () const

Returns the current number of nodes contained in the world trigger.
### Return value

Current number of nodes contained in the world trigger.
## void setSize ( vec3 size )

Sets a new current dimensions of the world trigger.
### Arguments

- *vec3* **size** - The current dimensions of the world trigger.

## vec3 getSize () const

Returns the current current dimensions of the world trigger.
### Return value

Current current dimensions of the world trigger.
## void setTouch ( )

Sets a new value indicating if a touch mode is enabled for the trigger. With this mode on, the trigger will react to the node by partial contact. When set to off, the trigger reacts only if the whole bounding sphere/box gets inside or outside of it.
### Arguments

- **touch** - The the touch mode for the trigger

## isTouch () const

Returns the current value indicating if a touch mode is enabled for the trigger. With this mode on, the trigger will react to the node by partial contact. When set to off, the trigger reacts only if the whole bounding sphere/box gets inside or outside of it.
### Return value

Current the touch mode for the trigger
## getEventLeave () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEnter () const

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

## static WorldTrigger ( vec3 size )

Constructor. Creates a new world trigger with given dimensions.
### Arguments

- *vec3* **size** - Dimensions of the new world trigger. If negative values are provided, **0** will be used instead of them.

## void setExcludeNodes ( int nodes[] )

Sets a list of excluded nodes, on which the world trigger will not react.
### Arguments

- *int* **nodes[]** - ID of the array with excluded nodes.

## getExcludeNodes ( int nodes[] )

Returns the current list of excluded nodes, on which the world trigger does not react.
### Arguments

- *int* **nodes[]** - ID of the array with excluded nodes.

## void setExcludeTypes ( int nodes[] )

Sets a list of excluded node types, on which the world trigger will not react.
### Arguments

- *int* **nodes[]** - ID of the array with excluded node types.

## Set<int> getExcludeTypes ( int nodes[] )

Returns the current list of excluded node types, on which the world trigger does not react.
### Arguments

- *int* **nodes[]** - ID of the array with excluded node types.

## Node getNode ( int num )

Returns a specified node contained in the world trigger.
```csharp
WorldTrigger trigger;

private void Init()
{

	// create a world trigger
	trigger = new WorldTrigger(new vec3(3.0f));
}

private void Update()
{

	// press the i key to get the info about nodes inside the trigger
	if (trigger != null && Input.IsKeyDown(Input.KEY.I))
	{
		//get the number of nodes inside the trigger
		int numNodes = trigger.NumNodes;
		Unigine.Log.Message("The number of nodes inside the trigger is " + numNodes + "\n");

		//loop through all nodes to print their names and types
		for (int i = 0; i < numNodes; i++)
		{
			Node node = trigger.GetNode(i);
			Unigine.Log.Message("The type of the " + node.Name + " node is " + node.Type + "\n");
		}
	}
}


```


### Arguments

- *int* **num** - Node number in range from 0 to the total number of nodes.

### Return value

Specified node.
## getNodes ( int id )

Gets nodes contained in the trigger and appends them to the vector with a given ID.
### Arguments

- *int* **id** - ID of the vector with nodes.

## void setTargetNodes ( int nodes[] )

Sets a list of target nodes, which will fire callbacks. If this list is empty, all nodes fire callbacks.
### Arguments

- *int* **nodes[]** - ID of the array with target nodes.

## getTargetNodes ( int nodes[] )

Returns the current list of target nodes, which fire callbacks. If this list is empty, all nodes fire callbacks.
### Arguments

- *int* **nodes[]** - ID of the array with target nodes.

## void setTargetTypes ( int nodes[] )

Sets a list of target node types, which will fire callbacks. If this list is empty, all nodes fire callbacks.
### Arguments

- *int* **nodes[]** - ID of the array with target node types.

## Set<int> getTargetTypes ( int nodes[] )

Returns the current list of target node types, which fire callbacks. If this list is empty, all nodes fire callbacks.
### Arguments

- *int* **nodes[]** - ID of the array with target node types.

## static int type ( )

Returns the type of the node.
### Return value

[World](../../../api/library/engine/class.world_usc.md) type identifier.
