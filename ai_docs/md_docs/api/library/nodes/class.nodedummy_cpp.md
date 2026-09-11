# Unigine::NodeDummy Class (CPP)

**Header:** #include <UnigineNodes.h>

**Inherits from:** Node


A **dummy node** is a zero-sized node that has no visual representation. It is used to organize the other nodes into a hierarchy:  the dummy node serves as a parent node and enables to organize the other nodes that are made its children into a group.

> **Notice:** A bounding box of the dummy node is equal to the bounding boxes of all its child nodes combined together.


### Creating a Dummy Node


Create an instance of the NodeDummy class. You can also specify such settings as a name, transformation and so on.


<details>
<summary>AppWorldLogic.cpp | Close</summary>

`AppWorldLogic.cpp`


```cpp
#include "AppWorldLogic.h"
#include <UnigineObjects.h>
#include <UnigineWorld.h>

using namespace Unigine;
using namespace Math;

int AppWorldLogic::init()
{

	// create a dummy node
	NodeDummyPtr dummy = NodeDummy::create();
	// set a name
	dummy->setName("DummyNode");

	return 1;
}


```

</details>


### Organizing a Nodes Hierarchy


To organize nodes in a hierarchy, do the following:

1. Create an instance of the NodeDummy class.
2. Create a node and add it as a child to the created dummy node.


<details>
<summary>AppWorldLogic.cpp | Close</summary>

`AppWorldLogic.cpp`


```cpp
#include "AppWorldLogic.h"
#include <UnigineObjects.h>
#include <UnigineWorld.h>

using namespace Unigine;
using namespace Math;

int AppWorldLogic::init()
{

	// create a dummy node
	NodeDummyPtr root = NodeDummy::create();
	// set a name for the node
	root->setName("root");

	// create child nodes
	for (int y = -10; y <= 10; y++)
	{
		for (int x = -10; x <= 10; x++)
		{

			// create a node (an instance of the ObjectMeshStatic class from the specified mesh-file)
			ObjectMeshStaticPtr node = ObjectMeshStatic::create("core/meshes/box.mesh");
			// set node transformation
			node->setWorldTransform(translate(Vec3(x * 2.0f, y * 2.0f, 0.0f)));
			// set a name for the node
			node->setName(String::format("mesh_%d_%d", x + 10, y + 10).get());
			// add the node as a child to the root dummy node
			root->addWorldChild(node);
		}
	}

	return 1;
}


```

</details>


## NodeDummy Class

---

## static NodeDummyPtr create ( )

Constructor. Creates a dummy node.
## static int type ( )

Returns the type of the node.
### Return value

[NodeDummy](../../../api/library/nodes/class.node_cpp.md#NODE_DUMMY) type identifier.
