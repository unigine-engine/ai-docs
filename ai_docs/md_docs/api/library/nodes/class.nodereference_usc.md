# Unigine.NodeReference Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


[NodeReference](../../../objects/nodes/reference/index.md) is a node that refers to an external `*.node` asset on the disk, which is obtained by [exporting](../../../editor2/exporting_nodes/index.md#export_to_noderef) a node from the world. The world can contain several NodeReference nodes referring to the same `*.node` file.


The `*.node` file usually contains a pre-fabricated node (or a hierarchy of nodes) with links to all materials, properties and physical bodies that are required for its rendering and behaviour. All changes that are made to NodeReference via UNIGINE Editor are saved to this file. When editing NodeReference via code, implement [saving changes](../../../api/library/engine/class.world_usc.md#saveNode_cstr_Node_int_int) to the `*.node` file.


NodeReferences should be used to propagate multiple identical objects repeated in the world: unlike regular nodes, reference nodes are loaded into the world faster because of the [internal cache](../../../principles/world_management/index.md#node_cache) usage. It will also make it easier to apply the same changes to all repeated objects.


> **Notice:** Each NodeReference has its internal copy of nodes loaded from the `*.node` asset, therefore it is required to save changes to the asset and reload all NodeReference nodes. [Automatic reloading](../../../api/library/engine/class.world_usc.md#setAutoReloadNodeReferences_int_void) is available.


NodeReference supports nesting, i.e. a node reference can include other node references, which is helpful for implementing complex [instancing](../../../editor2/instancing_nodes/index.md) solutions.


> **Notice:** A NodeReference itself does not have [bounds](../../../principles/world_management/index.md#bounds) and is excluded from the spatial tree.


A NodeReference instance is a [Possessor](../../../api/library/nodes/class.node_usc.md#getPossessor_Node) of the nodes stored by it, so it is responsible for loading and deleting them. You can [detach](#detachReference_Node) the node from the NodeReference instance to make it managed by the World.


### Automatic Unpacking


The *Automatic Unpacking* mode defines where the content of NodeReferences is placed in the world nodes hierarchy when it is loaded at run time (at the world startup or when a new NodeReference is created). When enabled, the content of NodeReference is extracted to simplify hierarchy management. This is a global setting for all worlds used in your project.


> **Notice:** - **Auto-unpacking is disabled** in *C++* and *UnigineScript only* projects by default for backward compatibility.
> - **Auto-unpacking is enabled** in *C#* projects by default.


Use *[engine.world.isUnpackNodeReferences()](../../../api/library/engine/class.world_usc.md#isUnpackNodeReferences_int)* to check if auto-unpacking is enabled in your project.


You can toggle the auto-unpacking mode by calling *[engine.world.setUnpackNodeReferences()](../../../api/library/engine/class.world_usc.md#setUnpackNodeReferences_int_void)* in the [system script](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_logic) before a world is loaded:


```cpp
#include <core/unigine.h>

int init()
{
	// enable automatic unpacking
	engine.world.setUnpackNodeReferences(1);
	return 1;
}

```


The auto-unpacking mode affects the [relation between the transformations](#node_trasformations) of the NodeReference and the nodes stored by it.


#### Automatic Unpacking Disabled


If auto-unpacking is disabled (by default in *C++ / UnigineScript only* projects), the content of NodeReference nodes is added to the root of the world nodes hierarchy and can be accessed only as [references](#getReference_Node).


![](unpack_off.png)

*Automatic Unpacking is disabled.*


```cpp
#include <core/unigine.h>

int init() {

	// create a NodeReference instance
	NodeReference nodeRef = new NodeReference("unigine_project/nodes/node_reference_0.node");


    // get the reference node
    Node group = nodeRef.getReference();

    // find the desired node
    Node node_2 = group.getChild(group.findChild("Node_2"));

	return 1;
}

```


#### Automatic Unpacking Enabled


When automatic unpacking of NodeReference is enabled (by default in *C#* projects), the content of NodeReference nodes is extracted to simplify hierarchy management. It is done only at run time and does not affect your `*.world` and `*.node` files.


![](unpack_on.png)

*Automatic Unpacking is enabled.*


The heirarchy of NodeReference's contents is attached to it as an immediate child, so you can access it in a straightforward manner:


```cpp
#include <core/unigine.h>

int init() {

	// create a NodeReference instance
	NodeReference nodeRef = new NodeReference("nodes/node_reference_0.node");

	// get the root node of the pre-fabricated hierarchy
	Node group = nodeRef.getChild(0);

	// find the desired node among all descendants
	Node node_2 = nodeRef.findNode("Node_2", 1);

	return 1;
}

```


### NodeReference Transformations


Local transformation of the root node stored by NodeReference is not necessarily identity, it can be displaced relative to the NodeReference position, for example.


> **Notice:** Changing transformation of nodes stored by the NodeReference does not affect the transformation of the NodeReference itself.


If [automatic unpacking of NodeReference](#unpacking) is enabled, the transformations of nodes are simply subject to [parent-child relation](../../../principles/world_structure/index.md#nodes_hierarchy). However, if automatic unpacking is disabled (i.e. the node content has been added to the root of world nodes hierarchy), [matrix hierarchy](../../../code/fundamentals/matrix_transformations/index_usc.md#hierarchy) is used for the content of the NodeReference. Thus, when moving the NodeReference, the root node of its content also moves relatively to this NodeReference. At that, the local transformation matrix of the root reference node changes.


> **Notice:** Changing transformation of the NodeReference **resets all changes** made to the local transformation of the root node stored by it only if *automatic unpacking* is disabled.


This relation of transformations can be destroyed by [detaching](#detachReference_Node) the reference node from the NodeReference instance. Note that the unpacked detached node will remain child of the NodeReference and its tranformation matrix will still be affected by the NodeReference transformation. In this case you may need to unparent the detached node by using [*setParent()*](../../../api/library/nodes/class.node_usc.md#setParent_Node_void) method.


### Internal Nodes Copy


Each NodeReference has its internal copy of nodes loaded from the `*.node` asset and therefore this allows applying unique changes to each instance of identical NodeReferences separately at runtime (adding, deleting, and changing the nodes inside NodeReference).


Other NodeReference instances will not be updated at runtime when changes are applied to a single instance. If you want to propagate these changes at runtime from one instance of a NodeReference to all the other NodeReference in the world that are linked to the same `*.node` asset on disk, you should save changes to the asset and reload all NodeReferences. [Automatic runtime reloading](../../../api/library/engine/class.world_usc.md#setAutoReloadNodeReferences_int_void) is available.


### Creating a Node Reference


To create a NodeReference, you should specify a path to the existing `*.node` file. For example, you can export a node into a `*.node` file and then create a NodeReference by using it:


```cpp
#include <core/unigine.h>

int init() {

	// create a mesh
	Mesh mesh = new Mesh();
	mesh.addBoxSurface("box_0", vec3(1.0f));
	// create a dynamic mesh by using the mesh
	ObjectMeshDynamic dynamic = new ObjectMeshDynamic(mesh);
	// export the dynamic mesh into a *.node file
	engine.world.saveNode("unigine_project/nodes/node_reference_0.node", dynamic);
	// create a node reference
	NodeReference nodeRef = new NodeReference("unigine_project/nodes/node_reference_0.node");

	return 1;
}

```


Also you can cast a Node instance to the NodeReference. However, such type casting is possible only if the Node type is [NODE_REFERENCE](../../../api/library/nodes/class.node_usc.md#NODE_REFERENCE). For example:


```cpp
#include <core/unigine.h>

void nodeCast(Node node) {

	// check if the node is a NodeReference
	if (node.getType() == NODE_REFERENCE)
	{
		// cast the node to the NodeReference
		NodeReference nodeRef = node_cast(node);
		// set a name for the NodeReference
		nodeRef.setName("NodeReference_cast");
	}
}

int init() {

	// create a NodeReference from the file
	NodeReference nodeRef_0 = new NodeReference("unigine_project/nodes/node_reference_0.node");
	// set a name
	nodeRef_0.setName("NodeReference_0");

	// save changes into the *.world file
	engine.console.run("world_save");
	// get the added NodeReference as a Node
	Node node = engine.world.getNodeByName("NodeReference_0");
	// cast the obtained Node to a NodeReference
	nodeCast(node);

	return 1;
}

```


As a result, the *NodeReference_0* node will be converted to the *NodeReference_cast* node.


### Editing a Node Reference


Editing a NodeReference includes:


- [Changing the path](#setNodePath_cstr_void) to the referenced `.node` file.
- Editing the node stored by the reference.


To access the node to which the *NodeReference* refers, use the *[getReference()](#getReference_Node)* method. To save the modified reference node to the same `.node` asset, use *[engine.world.saveNode()](../../../api/library/engine/class.world_usc.md#saveNode_cstr_Node_int_int)* method as follows:


```cpp
#include <core/unigine.h>

int init() {

	// create a NodeReference instance
	NodeReference nodeRef = new NodeReference("unigine_project/nodes/node_reference_0.node");
	// set a name
	nodeRef.setName("NodeReference_0");

	// get a node stored by the reference and check if it is an ObjectMeshDynamic
	if (nodeRef.getReference().getType() == NODE_OBJECT_MESH_DYNAMIC) {
		// cast the referenced node to the ObjectMeshDynamic type
		ObjectMeshDynamic dynamic = node_cast(nodeRef.getReference());
		// save changes on the referenced node into the *.node file
		engine.world.saveNode(nodeRef.getNodePath(), dynamic);
	}

	return 1;
}

```


As a result, the source `*.node` file, to which the NodeReference refers, will be updated and the *NodeReference_0* node will refer to the updated node with the material assigned. If you want all NodeReferences that refer to the modifed `*.node` asset to update automatically, you should enable automatic reloading of NodeReferences by calling the [*setAutoReloadNodeReferences()*](../../../api/library/engine/class.world_usc.md#setAutoReloadNodeReferences_int_void) method preliminarily.


> **Notice:** Saving nodes into a `*.node` asset takes into account their [local transformation](#node_trasformations).


### See Also


- Article on [Nodes](../../../objects/nodes/index.md) that lists the main differences between the regular nodes and reference nodes
- Article on [Node Reference](../../../objects/nodes/reference/index.md)
- [Node References: Must-Knows](../../../videotutorials/essentials/node_reference.md) demonstrating the specifics of *Node Reference*


## NodeReference Class

### Members

## void setNodePath ( string path )

Sets a new reference to a `*.node` file.
```cpp
// create an NodeReference instance
NodeReference nodeRef = new NodeReference("unigine_project/nodes/reference_0.node");
// ...
// change a reference node
nodeRef.setNodePath("unigine_project/nodes/reference_1.node");
// ...
// return the path to the reference node
log.message("The referenced node is: %s\n",nodeRef.getNodePath());

```


### Arguments

- *string* **path** - The path to a `*.node` file.

## const char * getNodePath () const

Returns the current reference to a `*.node` file.
```cpp
// create an NodeReference instance
NodeReference nodeRef = new NodeReference("unigine_project/nodes/reference_0.node");
// ...
// change a reference node
nodeRef.setNodePath("unigine_project/nodes/reference_1.node");
// ...
// return the path to the reference node
log.message("The referenced node is: %s\n",nodeRef.getNodePath());

```


### Return value

Current path to a `*.node` file.
## Node getReference () const

Returns the current node stored by the reference. Use this method when you need to change the referenced node. If a *[NodeDummy](../../../api/library/nodes/class.nodedummy_usc.md)* instance is returned, it means that several nodes of the same hierarchy level have been [converted into the *NodeReference*](../../../objects/nodes/reference/index.md#convert_several_nodes).
```cpp
// create a NodeReference instance
NodeReference nodeRef = new NodeReference("unigine_project/nodes/single_nref.node");
// get a node stored by the reference
Node node = nodeRef.getReference();
// if the node is a NodeDummy
if (node.getType() == NODE_DUMMY){
	// print the type name of each child node of the root node stored by the reference
	forloop(int i = 0; node.getNumChildren();1) {
		log.message("%d: %s\n",i,node.getChild(i).getTypeName());
	}
}

```


### Return value

Current node instance.
---

## static NodeReference ( string name )

Constructor. Creates a new object that references a node from a given file.
### Arguments

- *string* **name** - Path to a `*.node` file.

## static int canBeReference ( string name , Node node )

Returns a value indicating if the hierarchy of the given node does not contain a node reference with the given name.
### Arguments

- *string* **name** - Node reference name.
- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - Node to check.

### Return value

**1** if the hierarchy of the given node does not contain a node reference with the given name; otherwise, **0**.
## Node detachReference ( )

Returns the node stored by the reference and releases this node of ownership so it is no longer owned and referred to by the *NodeReference*. The node is managed by the World.
```cpp
// create a new NodeReference instance
NodeReference nodeRef = new NodeReference("unigine_project/nodes/node_reference_0.node");
// perform something
// ...
// get the node stored by the reference and release NodeReference ownership of the node
Node node = nodeRef.detachReference();

```


### Return value

Root node of the internal hierarchy.
## static int type ( )

Returns the type of the node.
### Return value

[NodeReference](../../../api/library/nodes/class.node_usc.md#NODE_REFERENCE) type identifier.
