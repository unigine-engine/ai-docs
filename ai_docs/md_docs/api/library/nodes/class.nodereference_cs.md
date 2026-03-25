# Unigine.NodeReference Class (CS)

**Inherits from:** Node


[NodeReference](../../../objects/nodes/reference/index.md) is a node that refers to an external `*.node` asset on the disk, which is obtained by [exporting](../../../editor2/exporting_nodes/index.md#export_to_noderef) a node from the world. The world can contain several NodeReference nodes referring to the same `*.node` file.


The `*.node` file usually contains a pre-fabricated node (or a hierarchy of nodes) with links to all materials, properties and physical bodies that are required for its rendering and behaviour. All changes that are made to NodeReference via UNIGINE Editor are saved to this file. When editing NodeReference via code, implement [saving changes](../../../api/library/engine/class.world_cs.md#saveNode_cstr_Node_int_int) to the `*.node` file.


NodeReferences should be used to propagate multiple identical objects repeated in the world: unlike regular nodes, reference nodes are loaded into the world faster because of the [internal cache](../../../principles/world_management/index.md#node_cache) usage. It will also make it easier to apply the same changes to all repeated objects.


> **Notice:** Each NodeReference has its internal copy of nodes loaded from the `*.node` asset, therefore it is required to save changes to the asset and reload all NodeReference nodes. [Automatic reloading](../../../api/library/engine/class.world_cs.md#setAutoReloadNodeReferences_int_void) is available.


NodeReference supports nesting, i.e. a node reference can include other node references, which is helpful for implementing complex [instancing](../../../editor2/instancing_nodes/index.md) solutions.


> **Notice:** A NodeReference itself does not have [bounds](../../../principles/world_management/index.md#bounds) and is excluded from the spatial tree.


A NodeReference instance is a [Possessor](../../../api/library/nodes/class.node_cs.md#getPossessor_Node) of the nodes stored by it, so it is responsible for loading and deleting them. You can [detach](#detachReference_Node) the node from the NodeReference instance to make it managed by the World.


### Automatic Unpacking


The *Automatic Unpacking* mode defines where the content of NodeReferences is placed in the world nodes hierarchy when it is loaded at run time (at the world startup or when a new NodeReference is created). When enabled, the content of NodeReference is extracted to simplify hierarchy management. This is a global setting for all worlds used in your project.


> **Notice:** - **Auto-unpacking is disabled** in *C++* and *UnigineScript only* projects by default for backward compatibility.
> - **Auto-unpacking is enabled** in *C#* projects by default.


Use the *[World.UnpackNodeReferences](../../../api/library/engine/class.world_cs.md#isUnpackNodeReferences_int)* flag to check if auto-unpacking is enabled in your project.


You can toggle the auto-unpacking mode by changing the *[World.UnpackNodeReferences](../../../api/library/engine/class.world_cs.md#isUnpackNodeReferences_int)* flag in the [system logic](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_logic) before a world is loaded:


```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Reflection;
using System.Runtime.InteropServices;
using System.Text;
using Unigine;

namespace UnigineApp
{
	internal class AppSystemLogic : SystemLogic
	{

		public override bool Init()
		{


			// disable automatic unpacking before the world is loaded
			World.UnpackNodeReferences = false;

			return true;
		}

	}
}


```


The auto-unpacking mode affects the [relation between the transformations](#node_trasformations) of the NodeReference and the nodes stored by it.


#### Automatic Unpacking Disabled


If auto-unpacking is disabled (by default in *C++ / UnigineScript only* projects), the content of NodeReference nodes is added to the root of the world nodes hierarchy and can be accessed only as [references](#getReference_Node).


![](unpack_off.png)

*Automatic Unpacking is disabled.*


```csharp
private void Init()
{

	// create a NodeReference instance
	NodeReference nodeRef = new NodeReference("nodes/node_reference_0.node");

	// get the reference node
	Node group = nodeRef.Reference;

	// find the desired node
	Node node_2 = group.GetChild(group.FindChild("Node_2"));
}


```


#### Automatic Unpacking Enabled


When automatic unpacking of NodeReference is enabled (by default in *C#* projects), the content of NodeReference nodes is extracted to simplify hierarchy management. It is done only at run time and does not affect your `*.world` and `*.node` files.


![](unpack_on.png)

*Automatic Unpacking is enabled.*


The heirarchy of NodeReference's contents is attached to it as an immediate child, so you can access it in a straightforward manner:


```csharp
private void Init()
{

	// create a NodeReference instance
	NodeReference nodeRef = new NodeReference("nodes/node_reference_0.node");

	// get the root node of the pre-fabricated hierarchy
	Node group = nodeRef.GetChild(0);

	// find the desired node among all descendants
	Node node_2 = nodeRef.FindNode("Node_2", 1);
}


```


### NodeReference Transformations


Local transformation of the root node stored by NodeReference is not necessarily identity, it can be displaced relative to the NodeReference position, for example.


> **Notice:** Changing transformation of nodes stored by the NodeReference does not affect the transformation of the NodeReference itself.


If [automatic unpacking of NodeReference](#unpacking) is enabled, the transformations of nodes are simply subject to [parent-child relation](../../../principles/world_structure/index.md#nodes_hierarchy). However, if automatic unpacking is disabled (i.e. the node content has been added to the root of world nodes hierarchy), [matrix hierarchy](../../../code/fundamentals/matrix_transformations/index_cs.md#hierarchy) is used for the content of the NodeReference. Thus, when moving the NodeReference, the root node of its content also moves relatively to this NodeReference. At that, the local transformation matrix of the root reference node changes.


> **Notice:** Changing transformation of the NodeReference **resets all changes** made to the local transformation of the root node stored by it only if *automatic unpacking* is disabled.


This relation of transformations can be destroyed by [detaching](#detachReference_Node) the reference node from the NodeReference instance. Note that the unpacked detached node will remain child of the NodeReference and its tranformation matrix will still be affected by the NodeReference transformation. In this case you may need to unparent the detached node by using [*setParent()*](../../../api/library/nodes/class.node_cs.md#setParent_Node_void) method.


### Internal Nodes Copy


Each NodeReference has its internal copy of nodes loaded from the `*.node` asset and therefore this allows applying unique changes to each instance of identical NodeReferences separately at runtime (adding, deleting, and changing the nodes inside NodeReference).


Other NodeReference instances will not be updated at runtime when changes are applied to a single instance. If you want to propagate these changes at runtime from one instance of a NodeReference to all the other NodeReference in the world that are linked to the same `*.node` asset on disk, you should save changes to the asset and reload all NodeReferences. [Automatic runtime reloading](../../../api/library/engine/class.world_cs.md#setAutoReloadNodeReferences_int_void) is available.


### Creating a Node Reference


To create a NodeReference, you should specify a path to the existing `*.node` file. For example, you can export a node into a `*.node` file and then create a NodeReference by using it:


```csharp
private void Init()
{

	// create a mesh
	Mesh mesh = new Mesh();
	mesh.AddBoxSurface("box_0", new vec3(1.0f));

	// create a dynamic mesh by using the mesh
	ObjectMeshDynamic dynamic = new ObjectMeshDynamic(mesh);

	// export the dynamic mesh into a *.node file
	World.SaveNode("unigine_project/nodes/node_reference_0.node", dynamic);

	// create a node reference
	NodeReference nodeRef = new NodeReference("unigine_project/nodes/node_reference_0.node");
}


```


Also you can cast a Node instance to the NodeReference. However, such type casting is possible only if the Node type is [NODE_REFERENCE](../../../api/library/nodes/class.node_cs.md#NODE_REFERENCE). For example:


```csharp
public void nodeCast(Node node)
{

	// check if the node is a NodeReference
	if (node.Type == Node.TYPE.NODE_REFERENCE)
	{
		// cast the node to the NodeReference
		NodeReference nodeRef = node as NodeReference;
		// set a name for the NodeReference
		nodeRef.Name = "NodeReference_cast";
	}
}

private void Init()
{

	// create a NodeReference from the file
	NodeReference nodeRef_0 = new NodeReference("unigine_project_10/nodes/node_reference_0.node");

	// set a name
	nodeRef_0.Name = "NodeReference_0";

	// save changes into the *.world file
	Unigine.Console.Run("world_save");

	// get the added NodeReference as a Node
	Node node = World.GetNodeByName("NodeReference_0");

	// cast the obtained Node to a NodeReference
	nodeCast(node);
}


```


As a result, the *NodeReference_0* node will be converted to the *NodeReference_cast* node.


### Editing a Node Reference


Editing a NodeReference includes:


- [Changing the path](#setNodePath_cstr_void) to the referenced `.node` file.
- Editing the node stored by the reference.


To access the node to which the *NodeReference* refers, use the *[Reference](#getReference_Node)* property. To save the modified reference node to the same `*.node` asset, use *[World.SaveNode()](../../../api/library/engine/class.world_cs.md#saveNode_cstr_Node_int_int)* method as follows:


```csharp
private void Init()
{

	// create a NodeReference instance
	NodeReference nodeRef = new NodeReference("unigine_project_10/nodes/node_reference_0.node");

	// set a name
	nodeRef.Name = "NodeReference_0";

	// get a node stored by the reference and check if it is an ObjectMeshDynamic
	if (nodeRef.Reference.Type == Node.TYPE.OBJECT_MESH_DYNAMIC)
	{
		// cast the referenced node to the ObjectMeshDynamic type
		ObjectMeshDynamic dynamic = nodeRef.Reference as ObjectMeshDynamic;

		// save changes on the referenced node into the *.node file
		World.SaveNode(nodeRef.NodePath, dynamic);
	}
}


```


As a result, the source `*.node` file, to which the NodeReference refers, will be updated and the *NodeReference_0* node will refer to the updated node with the material assigned. If you want all NodeReferences that refer to the modifed `*.node` asset to update automatically, you should enable automatic reloading of NodeReferences by calling the [*setAutoReloadNodeReferences()*](../../../api/library/engine/class.world_cs.md#setAutoReloadNodeReferences_int_void) method preliminarily.


> **Notice:** Saving nodes into a `*.node` asset takes into account their [local transformation](#node_trasformations).


### See Also


- Article on [Nodes](../../../objects/nodes/index.md) that lists the main differences between the regular nodes and reference nodes
- Article on [Node Reference](../../../objects/nodes/reference/index.md)
- [Node References: Must-Knows](../../../videotutorials/essentials/node_reference.md) demonstrating the specifics of *Node Reference*


## NodeReference Class

### Properties

## string NodePath

The path to the referenced `*.node` file.
```csharp
// create a NodeReference instance
NodeReference nodeRef = new NodeReference("unigine_project/nodes/reference_0.node");
// ...

// change a reference node
nodeRef.NodePath = "unigine_project/nodes/reference_1.node";
// ...

// return the path to the reference node
Log.Message("The referenced node is: {0}\n",nodeRef.NodePath);


```


## 🔒︎ Node Reference

The node stored by the reference. Use this property when you need to change the referenced node. If a *[NodeDummy](../../../api/library/nodes/class.nodedummy_cs.md)* instance is returned, it means that several nodes of the same hierarchy level have been [converted into the *NodeReference*](../../../objects/nodes/reference/index.md#convert_several_nodes).
```csharp
// create a NodeReference instance
NodeReference nodeRef = new NodeReference("unigine_project/nodes/single_nref.node");

// get a node stored by the reference
Node node = nodeRef.Reference;

// if the node is a NodeDummy
if (node.Type == Node.TYPE.NODE_DUMMY){
	// print the type name of each child node of the root node stored by the reference
	for(int i = 0; i < node.NumChildren; i++) {
		Log.Message("{0}: {1}\n",i,node.GetChild(i).TypeName);
	}
}


```


### Members

---

## NodeReference ( string name )

Constructor. Creates a new object that references a node from a given file.
### Arguments

- *string* **name** - Path to a `*.node` file.

## static bool CanBeReference ( string name , Node node )

Returns a value indicating if the hierarchy of the given node does not contain a node reference with the given name.
### Arguments

- *string* **name** - Node reference name.
- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Node to check.

### Return value

true if the hierarchy of the given node does not contain a node reference with the given name; otherwise, false.
## Node DetachReference ( )

Returns the node stored by the reference and releases this node of ownership so it is no longer owned and referred to by the *NodeReference*. The node is managed by the World.
```csharp
// create a new NodeReference instance
NodeReference nodeRef = new NodeReference("unigine_project/nodes/node_reference_0.node");
// perform something
// ...
// get the node stored by the reference and release NodeReference ownership of the node
Node node = nodeRef.DetachReference();
// destroy the NodeReference pointer as the NodeReference doesn't refer to a node any more
nodeRef.DeleteForce();


```


### Return value

Root node of the internal hierarchy.
