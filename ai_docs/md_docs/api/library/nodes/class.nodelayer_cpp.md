# Unigine::NodeLayer Class (CPP)

**Header:** #include <UnigineNodes.h>

**Inherits from:** Node


A [layer node](../../../objects/nodes/layer/index.md) is a zero-sized node that has no visual representation and enables to save all its child nodes into a separate `.node` file. Layer nodes should be used to split the world into several logical parts and save each of them in a `.node` file so that each layer and its child nodes can be edited without affecting the source `.world` file.

> **Notice:** The layer node itself is not stored in the `.node` file.


### Creating a Layer


Create an instance of the NodeLayer class. You can also specify such settings as a name, transformation and so on.


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

	// create a layer node
	NodeLayerPtr layer = NodeLayer::create("nodes/layer_0.node");
	// set a name for the node
	layer->setName("layer_0");

	return 1;
}


```

</details>


### Editing a Layer


Editing a layer node includes adding, deleting, modifying its child nodes. For example, you can add new nodes as follows:


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

	// create a layer node
	NodeLayerPtr layer = NodeLayer::create("nodes/layer_0.node");
	// set a name for the node
	layer->setName("layer_0");

	// create child nodes
	for (int y = -10; y <= 10; y++)
	{
		for (int x = -10; x <= 10; x++)
		{

			// create a mesh
			MeshPtr mesh = Mesh::create();
			mesh->addBoxSurface("box_0", vec3(1.0f));
			// create a node (e.g. an instance of the ObjectMeshDynamic class)
			ObjectMeshDynamicPtr node = ObjectMeshDynamic::create(mesh);

			// set node transformation
			node->setWorldTransform(translate(Vec3(x * 2.0f, y * 2.0f, 0.0f)));
			// set a name for the node
			node->setName(String::format("mesh_%d_%d", x + 10, y + 10).get());
			// add the node as a child to the layer node
			layer->addWorldChild(node);
		}
	}

	return 1;
}


```

</details>


### Saving a Layer


Changes made in the child nodes of the layer node can be saved on the disk by saving the world. The nodes will be saved in the separate `.node` file specified for the layer, not in the `.world` file.


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

	// create a layer node
	NodeLayerPtr layer = NodeLayer::create("nodes/layer_0.node");
	// set a name for the node
	layer->setName("layer_0");

	// create child nodes
	for (int y = -10; y <= 10; y++)
	{
		for (int x = -10; x <= 10; x++)
		{

			// create a mesh
			MeshPtr mesh = Mesh::create();
			mesh->addBoxSurface("box_0", vec3(1.0f));
			// create a node (e.g. an instance of the ObjectMeshDynamic class)
			ObjectMeshDynamicPtr node = ObjectMeshDynamic::create(mesh);

			// set node transformation
			node->setWorldTransform(translate(Vec3(x * 2.0f, y * 2.0f, 0.0f)));
			// set a name for the node
			node->setName(String::format("mesh_%d_%d", x + 10, y + 10).get());
			// add the node as a child to the layer node
			layer->addWorldChild(node);
		}
	}

	// check if the node layer and its ancestors can be saved to the .world file
	if (!layer->isSaveToWorldEnabled()) layer->setSaveToWorldEnabledRecursive(true);
	// save the world
	World::saveWorld();

	return 1;
}


```

</details>


Instead of saving the world, you can manually save child nodes of the layer into the `.node` file by using the [World::saveNodes()](../../../api/library/engine/class.world_cpp.md#saveNodes_cstr_VECNode_int_int) function:


```cpp
// declare array of nodes
Vector<NodePtr> nodes;
// append child nodes of the layer to the declared array
for (int i = 0; i < layer->getNumChildren(); i++) {
	nodes.append(layer->getChild(i));
}
// save nodes to the .node file
if (World::saveNodes(layer->getNodePath(), nodes) == 0) {
	Log::error("Layer hasn't been saved\n");
}


```


### See Also


- Article on [*Layer*](../../../objects/nodes/layer/index.md)


## NodeLayer Class

### Members

## void setNodePath ( const char * path )

Sets a new path to the node layer: a path to a `*.node` file where child nodes of the layer are stored.
### Arguments

- *const char ** **path** - The path to a `.node` file.

## const char * getNodePath () const

Returns the current path to the node layer: a path to a `*.node` file where child nodes of the layer are stored.
### Return value

Current path to a `.node` file.
---

## static NodeLayerPtr create ( const char * name )

Constructor. Creates a node layer with specified file name to store it.
### Arguments

- *const char ** **name** - Name of the layer.

## static int type ( )

Returns the type of the node.
### Return value

[NodeLayer](../../../api/library/nodes/class.node_cpp.md#NODE_LAYER) type identifier.
