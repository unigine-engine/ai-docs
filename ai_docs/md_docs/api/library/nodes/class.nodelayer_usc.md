# Unigine::NodeLayer Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


A [layer node](../../../objects/nodes/layer/index.md) is a zero-sized node that has no visual representation and enables to save all its child nodes into a separate `.node` file. Layer nodes should be used to split the world into several logical parts and save each of them in a `.node` file so that each layer and its child nodes can be edited without affecting the source `.world` file.

> **Notice:** The layer node itself is not stored in the `.node` file.


### Creating a Layer


Create an instance of the NodeLayer class. You can also specify such settings as a name, transformation and so on.


```cpp
#include <core/unigine.h>

int init() {
	// create a layer node
	NodeLayer layer = new NodeLayer();
	// set a name
	layer.setName("LayerNode");
}

```


### Editing a Layer


Editing a layer node includes adding, deleting, modifying its child nodes. For example, you can add new nodes as follows:


```cpp
#include <core/unigine.h>

int init() {

	// create a layer node
	NodeLayer layer = new NodeLayer();
	// set a name for the node
	layer.setName("layer_0");


	// create a mesh
	Mesh mesh = new Mesh();
	mesh.addBoxSurface("box_0", vec3(1.0f));
	// create a node (e.g. an instance of the ObjectMeshDynamic class)
	ObjectMeshDynamic node = new ObjectMeshDynamic(mesh);

	// set node transformation
	node.setWorldTransform(translate(Vec3(x * 2, y * 2, 0.0f)));
	// set a name for the node
	node.setName(format("mesh_%d_%d", x + 10, y + 10));

	// add the node as a child to the layer node
	layer.addWorldChild(node);

	return 1;
}

```


### Saving a Layer


```cpp
#include <core/unigine.h>

int init() {

	// create a layer node
	NodeLayer layer = new NodeLayer("unigine_project/nodes/layer_0.node");
	// set a name for the node
	layer.setName("layer_0");


	// create child nodes
	for (int y = -4; y <= 4; y++)
	{
		for (int x = -4; x <= 4; x++)
		{

			// create a mesh
			Mesh mesh = new Mesh();
			mesh.addBoxSurface("box_0", vec3(1.0f));
			// create a node (e.g. an instance of the ObjectMeshDynamic class)
			ObjectMeshDynamic node = new ObjectMeshDynamic(mesh);

			// set node transformation
			node.setWorldTransform(translate(Vec3(x * 2, y * 2, 0.0f)));
			// set a name for the node
			node.setName(format("mesh_%d_%d", x + 4, y + 4));

			// add the node as a child to the layer node
			layer.addWorldChild(node);
		}
	}

	// save the world
	engine.console.run("world_save unigine_project");

	return 1;
}

```


Instead of saving the world, you can manually save child nodes of the layer into the `.node` file by using the [engine.world.saveNodes()](../../../api/library/engine/class.world_usc.md#saveNodes_cstr_VECNode_int_int) function:


```cpp
// declare an array of nodes
Node nodes[0] = ();
// add child nodes of the layer to the declared array
for (int i = 0; i < layer.getNumChildren(); i++) {
    nodes.append(layer.getChild(i));
}
// save nodes to the .node file
if (engine.world.saveNodes(layer.getNodePath(), nodes) == 0) {
	log.error("Layer hasn't been saved\n");
}

```


### See Also


- Article on [*Layer*](../../../objects/nodes/layer/index.md)


## NodeLayer Class

### Members

## void setNodePath ( string path )

Sets a new path to the node layer: a path to a `*.node` file where child nodes of the layer are stored.
### Arguments

- *string* **path** - The path to a `.node` file.

## const char * getNodePath () const

Returns the current path to the node layer: a path to a `*.node` file where child nodes of the layer are stored.
### Return value

Current path to a `.node` file.
---

## static NodeLayer ( string name )

Constructor. Creates a node layer with specified file name to store it.
### Arguments

- *string* **name** - Name of the layer.

## static int type ( )

Returns the type of the node.
### Return value

[NodeLayer](../../../api/library/nodes/class.node_usc.md#NODE_LAYER) type identifier.
