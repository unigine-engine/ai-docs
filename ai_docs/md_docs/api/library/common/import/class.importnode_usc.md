# Unigine::ImportNode Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is an intermediate representation of a scene node from a source file (FBX, glTF, etc.). Each node has a transformation matrix and can have child nodes forming a hierarchy. Depending on its role in the source file, a node may reference an *[ImportMesh](../../../../api/library/common/import/class.importmesh_usc.md), [ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_usc.md), [ImportLight](../../../../api/library/common/import/class.importlight_usc.md)*, or *[ImportCamera](../../../../api/library/common/import/class.importcamera_usc.md)*. Nodes are also used as joints in an *[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_usc.md)*. During import, the node hierarchy is converted to UNIGINE [Nodes](../../../../api/library/nodes/class.node_usc.md) by an [import processor](../../../../api/library/common/import/class.importprocessor_usc.md).


## ImportNode Class

### Members

## void setData ( vptr data )

Sets a new metadata of the imported node.
### Arguments

- *vptr* **data** - The node metadata.

## vptr getData () const

Returns the current metadata of the imported node.
### Return value

Current node metadata.
## void setFilepath ( string filepath )

Sets a new path to the output node file.
### Arguments

- *string* **filepath** - The output node file.

## const char * getFilepath () const

Returns the current path to the output node file.
### Return value

Current output node file.
## void setCamera ( ImportCamera camera )

Sets a new camera node attribute.
### Arguments

- *[ImportCamera](../../../../api/library/common/import/class.importcamera_usc.md)* **camera** - The Camera attribute: *[ImportCamera](../../../../api/library/common/import/class.importcamera_usc.md)* class instance if a camera attribute is assigned to the node; otherwise, nullptr.

## ImportCamera getCamera () const

Returns the current camera node attribute.
### Return value

Current Camera attribute: *[ImportCamera](../../../../api/library/common/import/class.importcamera_usc.md)* class instance if a camera attribute is assigned to the node; otherwise, nullptr.
## void setLight ( ImportLight light )

Sets a new light node attribute.
### Arguments

- *[ImportLight](../../../../api/library/common/import/class.importlight_usc.md)* **light** - The light attribute: *[ImportLight](../../../../api/library/common/import/class.importlight_usc.md)* class instance if a light attribute is assigned to the node; otherwise, nullptr.

## ImportLight getLight () const

Returns the current light node attribute.
### Return value

Current light attribute: *[ImportLight](../../../../api/library/common/import/class.importlight_usc.md)* class instance if a light attribute is assigned to the node; otherwise, nullptr.
## void setMesh ( ImportMesh mesh )

Sets a new mesh node attribute.
### Arguments

- *[ImportMesh](../../../../api/library/common/import/class.importmesh_usc.md)* **mesh** - The mesh attribute: *[ImportMesh](../../../../api/library/common/import/class.importmesh_usc.md)* class instance if a mesh attribute is assigned to the node; otherwise, nullptr.

## ImportMesh getMesh () const

Returns the current mesh node attribute.
### Return value

Current mesh attribute: *[ImportMesh](../../../../api/library/common/import/class.importmesh_usc.md)* class instance if a mesh attribute is assigned to the node; otherwise, nullptr.
## void setMeshSkinned ( ImportMeshSkinned skinned )

Sets a new skinned mesh node attribute.
### Arguments

- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_usc.md)* **skinned** - The skinned mesh attribute: *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_usc.md)* class instance if a skinned mesh attribute is assigned to the node; otherwise, nullptr.

## ImportMeshSkinned getMeshSkinned () const

Returns the current skinned mesh node attribute.
### Return value

Current skinned mesh attribute: *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_usc.md)* class instance if a skinned mesh attribute is assigned to the node; otherwise, nullptr.
## void setName ( string name )

Sets a new name of the imported scene node.
### Arguments

- *string* **name** - The scene node name.

## const char * getName () const

Returns the current name of the imported scene node.
### Return value

Current scene node name.
## void setParent ( ImportNode parent )

Sets a new parent node of the imported scene node.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_usc.md)* **parent** - The parent node of the imported scene node.

## ImportNode getParent () const

Returns the current parent node of the imported scene node.
### Return value

Current parent node of the imported scene node.
## void setTransform ( dmat4 transform )

Sets a new transformation matrix of the imported scene node.
### Arguments

- *dmat4* **transform** - The Node's transformation matrix.

## dmat4 getTransform () const

Returns the current transformation matrix of the imported scene node.
### Return value

Current Node's transformation matrix.
---

## static ImportNode ( )

Constructor. Creates an empty *ImportNode* instance.
## void addChild ( ImportNode node )

Adds the specified node as a child to the imported scene node.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_usc.md)* **node** - Node to be added as a child to the imported node.

## bool removeChild ( ImportNode node )

Removes the specified node from the list of children of the imported scene node.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_usc.md)* **node** - Node to be removed from the list of children.

## ImportNode getChild ( int index )

Returns the child node of the imported node having the specified index.
### Arguments

- *int* **index** - Child node index within the range from 0 to ([total number of children](#getNumChildren_int) - 1).

### Return value

Child node of the imported node with the specified index.
## int getNumChildren ( )

Returns the number of children of the imported node.
### Return value

Number of node's children.
