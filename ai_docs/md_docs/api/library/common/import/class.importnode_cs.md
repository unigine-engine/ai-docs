# Unigine::ImportNode Class (CS)


This class is an intermediate representation of a scene node from a source file (FBX, glTF, etc.). Each node has a transformation matrix and can have child nodes forming a hierarchy. Depending on its role in the source file, a node may reference an *[ImportMesh](../../../../api/library/common/import/class.importmesh_cs.md), [ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md), [ImportLight](../../../../api/library/common/import/class.importlight_cs.md)*, or *[ImportCamera](../../../../api/library/common/import/class.importcamera_cs.md)*. Nodes are also used as joints in an *[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cs.md)*. During import, the node hierarchy is converted to UNIGINE [Nodes](../../../../api/library/nodes/class.node_cs.md) by an [import processor](../../../../api/library/common/import/class.importprocessor_cs.md).


## ImportNode Class

### Properties

## IntPtr Data

The metadata of the imported node.
## string Filepath

The path to the output node file.
## ImportCamera Camera

The camera node attribute.
## ImportLight Light

The light node attribute.
## ImportMesh Mesh

The mesh node attribute.
## ImportMeshSkinned MeshSkinned

The skinned mesh node attribute.
## string Name

The name of the imported scene node.
## ImportNode Parent

The parent node of the imported scene node.
## dmat4 Transform

The transformation matrix of the imported scene node.
### Members

---

## ImportNode ( )

Constructor. Creates an empty *ImportNode* instance.
## void AddChild ( ImportNode node )

Adds the specified node as a child to the imported scene node.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **node** - Node to be added as a child to the imported node.

## bool RemoveChild ( ImportNode node )

Removes the specified node from the list of children of the imported scene node.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **node** - Node to be removed from the list of children.

## ImportNode GetChild ( int index )

Returns the child node of the imported node having the specified index.
### Arguments

- *int* **index** - Child node index within the range from 0 to ([total number of children](#getNumChildren_int) - 1).

### Return value

Child node of the imported node with the specified index.
## int GetNumChildren ( )

Returns the number of children of the imported node.
### Return value

Number of node's children.
