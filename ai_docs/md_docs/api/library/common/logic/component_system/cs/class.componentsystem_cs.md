# ComponentSystem Class (CS)

> **Notice:** This class is a singleton.


This class implements functionality of the C# Component System and is used to create, destroy, and manage components.


### See Also


- C# Sample:


## ComponentSystem Class

### Properties

## 🔒︎ bool Enabled

The Value indicating whether the C# Component System is enabled: true if the C# Component System is enabled; otherwise false.
### Members

---

## public static ChangedProperties SaveProperties ( )


Creates property files for all components. Parameters of each component are stored in a separate `*.prop` file. If these property files do not exist, they will be created in the `data/.runtimes` folder.


```csharp
// Saving properties generated for all components
// and getting the list of changed properties (created, modified, and broken)
ComponentSystem.ChangedProperties changedProperties = ComponentSystem.SaveProperties();

// printing out all created, modified, and broken properties
foreach (var e in changedProperties.Created)
	Log.Message($"Created:  {e.Name} -> {e.Path}\n");

foreach (var e in changedProperties.Modified)
	Log.Message($"Modified: {e.Name} -> {e.Path}\n");

foreach (var e in changedProperties.Broken)
	Log.Message($"Broken:   {e.Name} -> {e.Path}\n");

```


### Return value


List of created, modified and broken properties (names and paths) as an instance of the *ChangedProperties* class declared as follows:


```csharp
public class ChangedProperties
{
	public struct NamePath
	{
		public readonly string Name;
		public readonly string Path;
	}

	public readonly List<NamePath> Created;
	public readonly List<NamePath> Modified;
	public readonly List<NamePath> Broken;
}

```


## public static Component AddComponent ( Node node , String component_name )

Adds the component with the specified name to the specified node.
### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, to which the component is to be added.
- *String* **component_name** - Name of the component to be added.

### Return value

New added component instance, if it was successfully added to the specified node; otherwise null.
## public static T AddComponent < T > ( Node node ) # where T : Component

Adds the component to the specified node.
### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, to which the component is to be added.

### Return value

New added component instance, if it was successfully added to the specified node; otherwise null.
## public static Component GetComponent ( Node node , String component_name , bool enabled_only = false )

Returns the first component with the specified name associated with the specified node.
### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, for which the component of this type is to be found.
- *String* **component_name** - Name of the component to be taken.
- *bool* **enabled_only** - Enabled flag: true to get enabled component only, false to get component in any case.

### Return value

Component if it exists; otherwise, null.
## public static T GetComponent < T > ( Node node , bool enabled_only = false ) # where T : Class

Returns the first component of the specified type associated with the specified node.
### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, for which the component of this type is to be found.
- *bool* **enabled_only** - Enabled flag: true to get enabled component only, false to get component in any case.

### Return value

Component if it exists; otherwise, null.
## public static T[] GetComponents < T > ( Node node , bool enabled_only = false ) # where T : Class

Returns all components of this type assigned to the specified node.
### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, whose components are to be retrieved.
- *bool* **enabled_only** - Enabled flag: true to get only enabled components, false to get all components.

### Return value

Array containing all found components of this type (if any); otherwise null.
## public static T GetComponentInChildren < T > ( Node node , bool enabled_only = false ) # where T : Class


Returns the first component of this type found among all the children of the specified node (including the node itself). This method searches for the component in the following order:


- node itself
- node reference
- node's children
- children of node's children


### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, whose hierarchy is to be checked for the components of this type.
- *bool* **enabled_only** - Enabled flag: true to get enabled component only, false to get component in any case.

### Return value

Component if it exists; otherwise, null.
## public static T[] GetComponentsInChildren < T > ( Node node , bool enabled_only = false ) # where T : Class

Searches for all components of this type down the hierarchy of the specified node.
### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, whose hierarchy is to be checked for the components of this type.
- *bool* **enabled_only** - Enabled flag: true to get only enabled components, false to get all components.

### Return value

Array containing all found components of this type (if any); otherwise null.
## public static T GetComponentInParent < T > ( Node node , bool enabled_only = false ) # where T : Class

Returns the first component of this type found among all predecessors and [posessors](../../../../../../api/library/nodes/class.node_cs.md#getPossessor_Node) of the specified node.
### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, whose hierarchy is to be checked for the components of this type.
- *bool* **enabled_only** - Enabled flag: true to get enabled component only, false to get component in any case.

### Return value

Component if it exists; otherwise, null.
## public static T[] GetComponentsInParent < T > ( Node node , bool enabled_only = false ) # where T : Class

Searches for all components of this type up the hierarchy of the specified node.
### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, whose hierarchy is to be checked for the components of this type.
- *bool* **enabled_only** - Enabled flag: true to get only enabled components, false to get all components.

### Return value

Array containing all found components of this type (if any); otherwise null.
## public static T FindComponentInWorld < T > ( bool enabled_only = false ) # where T : Class

Returns the first component of this type found in the current world.
### Arguments

- *bool* **enabled_only** - Enabled flag: true to get enabled component only, false to get component in any case.

### Return value

Component if it exists; otherwise, null.
## public static T[] FindComponentsInWorld < T > ( bool enabled_only = false ) # where T : Class

Returns the list of all components of this type found in the current world.
### Arguments

- *bool* **enabled_only** - Enabled flag: true to get only enabled components, false to get all components.

### Return value

Array containing all found components of this type (if any); otherwise null.
## public static int RemoveComponent < T > ( Node node ) # where T : Class

Removes the component from the specified node.
### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, from which the component is to be removed.

### Return value

1 if the component was successfully removed from the specified node; otherwise 0.
## public static int RemoveComponent ( Node node , String component_name )

Removes the component with the specified name from the specified node.
### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, from which the component is to be removed.
- *String* **component_name** - Name of the component to be removed.

### Return value

1 if the component with the specified name was successfully removed from the specified node; otherwise 0.
## public static int RemoveComponent ( Component component )

Removes the specified component.
### Arguments

- *Component* **component** - Component to be removed.

### Return value

**1** if the specified component was successfully removed; otherwise **0**.
## public static bool CheckComponentMethods ( List<string> error_messages )

Checks signatures of all methods in all components. If all methods are correct, true is returned. Otherwise, the specified messages will be printed to the console.
### Arguments

- *List<string>* **error_messages** - Error messages to be sent to the console.

### Return value

**true** if all methods are correct.
## void GetStatistics ( out int nodes , out int components , out int methods )

Returns the current state of the Component System (total number of components, nodes having components assigned, as well as methods for components) putting the values to corresponding variables.
### Arguments

- *out int* **nodes** - Total number of nodes with components.
- *out int* **components** - Total number of components.
- *out int* **methods** - Total number of methods in the Component System.
