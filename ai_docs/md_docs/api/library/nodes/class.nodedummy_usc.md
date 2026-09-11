# Unigine::NodeDummy Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


A **dummy node** is a zero-sized node that has no visual representation. It is used to organize the other nodes into a hierarchy:  the dummy node serves as a parent node and enables to organize the other nodes that are made its children into a group.

> **Notice:** A bounding box of the dummy node is equal to the bounding boxes of all its child nodes combined together.


### Creating a Dummy Node


Create an instance of the NodeDummy class. You can also specify such settings as a name, transformation and so on.


```cpp
#include <core/unigine.h>

int init() {
	// create a dummy node
	NodeDummy dummy = new NodeDummy();
	// set a name
	dummy.setName("DummyNode");
}

```


### Organizing a Nodes Hierarchy


To organize nodes in a hierarchy, do the following:

1. Create an instance of the NodeDummy class.
2. Create a node and add it as a child to the created dummy node.


```cpp
#include <core/unigine.h>

int init() {

	// create a dummy node
	NodeDummy root = new NodeDummy();
	// set a name for the node
	root.setName("root");


	// create child nodes
	for (int y = -10; y <= 10; y++)
	{
		for (int x = -10; x <=10; x++)
		{

			// create a node (an instance of the ObjectMeshStatic class)
			ObjectMeshStatic node = new ObjectMeshStatic("core/meshes/box.mesh");


			// set node transformation
			node.setWorldTransform(translate(Vec3(x * 2, y * 2, 0.0f)));
			// set a name for the node
			node.setName(format("mesh_%d_%d", x + 10, y + 10));
			// add the node as a child to the root dummy node
			root.addWorldChild(node);
		}
	}
}

```


## NodeDummy Class

---

## static NodeDummy ( )

Constructor. Creates a dummy node.
## static int type ( )

Returns the type of the node.
### Return value

[NodeDummy](../../../api/library/nodes/class.node_usc.md#NODE_DUMMY) type identifier.
