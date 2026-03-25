# Unigine::NodeLayer Class (CS)

**Inherits from:** Node


A [layer node](../../../objects/nodes/layer/index.md) is a zero-sized node that has no visual representation and enables to save all its child nodes into a separate `.node` file. Layer nodes should be used to split the world into several logical parts and save each of them in a `.node` file so that each layer and its child nodes can be edited without affecting the source `.world` file.

> **Notice:** The layer node itself is not stored in the `.node` file.


### Creating a Layer


Create an instance of the NodeLayer class. You can also specify such settings as a name, transformation and so on.


<details>
<summary>NodeLayerClass.cs | Close</summary>

`NodeLayerClass.cs`


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class NodeLayerClass : Component
{
	private void Init()
	{

		// create a layer node
		NodeLayer layer = new NodeLayer("nodes/layer_0.node");
		// set a name for the node
		layer.Name = "layer_0";

	}
}

```

</details>


### Editing a Layer


Editing a layer node includes adding, deleting, modifying its child nodes. For example, you can add new nodes as follows:


<details>
<summary>NodeLayerClass.cs | Close</summary>

`NodeLayerClass.cs`


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class NodeLayerClass : Component
{
	private void Init()
	{

		// create a layer node
		NodeLayer layer = new NodeLayer("nodes/layer_0.node");
		// set a name for the node
		layer.Name = "layer_0";

		// create child nodes
		for (int y = -10; y <= 10; y++)
		{
			for (int x = -10; x <= 10; x++)
			{

				// create a mesh
				Mesh mesh = new Mesh();
				mesh.AddBoxSurface("box_0", new vec3(1.0f));
				// create a node (e.g. an instance of the ObjectMeshDynamic class)
				ObjectMeshDynamic node = new ObjectMeshDynamic(mesh);

				// set node transformation
				node. WorldTransform = MathLib.Translate(new vec3(x * 2.0f, y * 2.0f, 0.0f));
				// set a name for the node
				node.Name = String.Format("mesh_{0}_{1}", x + 10.0f, y + 10.0f);

				// add the node as a child to the layer node
				layer.AddWorldChild(node);
			}
		}

	}
}

```

</details>


### Saving a Layer


Changes made in the child nodes of the layer node can be saved into the `.node` file by using the [World.SaveNodes()](../../../api/library/engine/class.world_cs.md#saveNodes_cstr_VECNode_int_int) function:


<details>
<summary>NodeLayerClass.cs | Close</summary>

`NodeLayerClass.cs`


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class NodeLayerClass : Component
{
	private void Init()
	{

		// create a layer node
		NodeLayer layer = new NodeLayer("nodes/layer_0.node");
		// set a name for the node
		layer.Name = "layer_0";

		// create child nodes
		for (int y = -10; y <= 10; y++)
		{
			for (int x = -10; x <= 10; x++)
			{

				// create a mesh
				Mesh mesh = new Mesh();
				mesh.AddBoxSurface("box_0", new vec3(1.0f));
				// create a node (e.g. an instance of the ObjectMeshDynamic class)
				ObjectMeshDynamic node = new ObjectMeshDynamic(mesh);

				// set node transformation
				node. WorldTransform = MathLib.Translate(new vec3(x * 2.0f, y * 2.0f, 0.0f));
				// set a name for the node
				node.Name = String.Format("mesh_{0}_{1}", x + 10.0f, y + 10.0f);

				// add the node as a child to the layer node
				layer.AddWorldChild(node);
			}
		}

		// declare a list of nodes
		List<Node> nodes_list = new List<Node>();
		// add child nodes of the layer to the declared list
		for (int i = 0; i < layer.NumChildren; i++) {
			nodes_list.Add(layer.GetChild(i));
		}
		// convert the list to Unigine.Node[] array so that nodes can be saved to a file later
		Node[] nodes = nodes_list.ToArray();

		// save nodes to the .node file
		if (!World.SaveNodes(layer.NodePath, nodes)) {
			Log.Error("Layer hasn't been saved\n");
		}

	}
}

```

</details>


### See Also


- Article on [*Layer*](../../../objects/nodes/layer/index.md)


## NodeLayer Class

### Properties

## string NodePath

The path to the node layer: a path to a `*.node` file where child nodes of the layer are stored.
### Members

---

## NodeLayer ( string name )

Constructor. Creates a node layer with specified file name to store it.
### Arguments

- *string* **name** - Name of the layer.

## static int type ( )

Returns the type of the node.
### Return value

[NodeLayer](../../../api/library/nodes/class.node_cs.md#NODE_LAYER) type identifier.
