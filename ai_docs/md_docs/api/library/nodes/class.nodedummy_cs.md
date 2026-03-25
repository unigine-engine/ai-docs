# Unigine::NodeDummy Class (CS)

**Inherits from:** Node


A **dummy node** is a zero-sized node that has no visual representation. It is used to organize the other nodes into a hierarchy:  the dummy node serves as a parent node and enables to organize the other nodes that are made its children into a group.

> **Notice:** A bounding box of the dummy node is equal to the bounding boxes of all its child nodes combined together.


### Creating a Dummy Node


Create an instance of the NodeDummy class. You can also specify such settings as a name, transformation and so on.


<details>
<summary>NodeDummyClass.cs | Close</summary>

`NodeDummyClass.cs`


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class NodeDummyClass : Component
{
	private void Init()
	{

		// create a dummy node
		NodeDummy dummy = new NodeDummy();
		// set a name
		dummy.Name = "DummyNode";

	}
}

```

</details>


### Organizing a Nodes Hierarchy


To organize nodes in a hierarchy, do the following:

1. Create an instance of the NodeDummy class.
2. Create a node and add it as a child to the created dummy node.


<details>
<summary>NodeDummyClass.cs | Close</summary>

`NodeDummyClass.cs`


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class NodeDummyClass : Component
{
	private void Init()
	{

		// create a dummy node
		NodeDummy root = new NodeDummy();
		// set a name for the node
		root.Name = "root";

		// create child nodes
		for (int y = -10; y <= 10; y++)
		{
			for (int x = -10; x <= 10; x++)
			{

				// create a node (an instance of the ObjectMeshStatic class from the specified mesh-file)
				ObjectMeshStatic node = new ObjectMeshStatic("core/meshes/box.mesh");

				// set node transformation
				node.WorldTransform = MathLib.Translate(new vec3(x * 2.0f, y * 2.0f, 0.0f));
				// set a name for the node
				node.Name = String.Format("mesh_{0}_{1}", x + 10, y + 10);
				// add the node as a child to the root dummy node
				root.AddWorldChild(node);
			}
		}

	}
}

```

</details>


## NodeDummy Class

### Members

---

## NodeDummy ( )

Constructor. Creates a dummy node.
## static int type ( )

Returns the type of the node.
### Return value

[NodeDummy](../../../api/library/nodes/class.node_cs.md#NODE_DUMMY) type identifier.
