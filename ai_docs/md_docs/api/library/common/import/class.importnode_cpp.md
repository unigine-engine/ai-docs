# Unigine::ImportNode Class (CPP)

**Header:** #include <UnigineImport.h>


This class is an intermediate representation of a scene node from a source file (FBX, glTF, etc.). Each node has a transformation matrix and can have child nodes forming a hierarchy. Depending on its role in the source file, a node may reference an *[ImportMesh](../../../../api/library/common/import/class.importmesh_cpp.md), [ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cpp.md), [ImportLight](../../../../api/library/common/import/class.importlight_cpp.md)*, or *[ImportCamera](../../../../api/library/common/import/class.importcamera_cpp.md)*. Nodes are also used as joints in an *[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cpp.md)*. During import, the node hierarchy is converted to UNIGINE [Nodes](../../../../api/library/nodes/class.node_cpp.md) by an [import processor](../../../../api/library/common/import/class.importprocessor_cpp.md).


## ImportNode Class

### Members

## void setData ( void * data )

Sets a new metadata of the imported node.
### Arguments

- *void ** **data** - The node metadata.

## void * getData () const

Returns the current metadata of the imported node.
### Return value

Current node metadata.
## void setFilepath ( const char * filepath )

Sets a new path to the output node file.
### Arguments

- *const char ** **filepath** - The output node file.

## const char * getFilepath () const

Returns the current path to the output node file.
### Return value

Current output node file.
## void setCamera ( const Ptr < ImportCamera >& camera )

Sets a new camera node attribute.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportCamera](../../../../api/library/common/import/class.importcamera_cpp.md)>&* **camera** - The Camera attribute: *[ImportCamera](../../../../api/library/common/import/class.importcamera_cpp.md)* class instance if a camera attribute is assigned to the node; otherwise, nullptr.

## Ptr < ImportCamera > getCamera () const

Returns the current camera node attribute.
### Return value

Current Camera attribute: *[ImportCamera](../../../../api/library/common/import/class.importcamera_cpp.md)* class instance if a camera attribute is assigned to the node; otherwise, nullptr.
## void setLight ( const Ptr < ImportLight >& light )

Sets a new light node attribute.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportLight](../../../../api/library/common/import/class.importlight_cpp.md)>&* **light** - The light attribute: *[ImportLight](../../../../api/library/common/import/class.importlight_cpp.md)* class instance if a light attribute is assigned to the node; otherwise, nullptr.

## Ptr < ImportLight > getLight () const

Returns the current light node attribute.
### Return value

Current light attribute: *[ImportLight](../../../../api/library/common/import/class.importlight_cpp.md)* class instance if a light attribute is assigned to the node; otherwise, nullptr.
## void setMesh ( const Ptr < ImportMesh >& mesh )

Sets a new mesh node attribute.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportMesh](../../../../api/library/common/import/class.importmesh_cpp.md)>&* **mesh** - The mesh attribute: *[ImportMesh](../../../../api/library/common/import/class.importmesh_cpp.md)* class instance if a mesh attribute is assigned to the node; otherwise, nullptr.

## Ptr < ImportMesh > getMesh () const

Returns the current mesh node attribute.
### Return value

Current mesh attribute: *[ImportMesh](../../../../api/library/common/import/class.importmesh_cpp.md)* class instance if a mesh attribute is assigned to the node; otherwise, nullptr.
## void setMeshSkinned ( const Ptr < ImportMeshSkinned >& skinned )

Sets a new skinned mesh node attribute.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cpp.md)>&* **skinned** - The skinned mesh attribute: *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cpp.md)* class instance if a skinned mesh attribute is assigned to the node; otherwise, nullptr.

## Ptr < ImportMeshSkinned > getMeshSkinned () const

Returns the current skinned mesh node attribute.
### Return value

Current skinned mesh attribute: *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cpp.md)* class instance if a skinned mesh attribute is assigned to the node; otherwise, nullptr.
## void setName ( const char * name )

Sets a new name of the imported scene node.
### Arguments

- *const char ** **name** - The scene node name.

## const char * getName () const

Returns the current name of the imported scene node.
### Return value

Current scene node name.
## void setParent ( const Ptr < ImportNode >& parent )

Sets a new parent node of the imported scene node.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)>&* **parent** - The parent node of the imported scene node.

## Ptr < ImportNode > getParent () const

Returns the current parent node of the imported scene node.
### Return value

Current parent node of the imported scene node.
## void setTransform ( const Math:: dmat4 & transform )

Sets a new transformation matrix of the imported scene node.
### Arguments

- *const  Math::[dmat4](../../../../api/library/math/class.dmat4_cpp.md)&* **transform** - The Node's transformation matrix.

## Math:: dmat4 getTransform () const

Returns the current transformation matrix of the imported scene node.
### Return value

Current Node's transformation matrix.
---

## static ImportNodePtr create ( )

Constructor. Creates an empty *ImportNode* instance.
## void addChild ( const Ptr < ImportNode > & node )

Adds the specified node as a child to the imported scene node.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)> &* **node** - Node to be added as a child to the imported node.

## bool removeChild ( const Ptr < ImportNode > & node )

Removes the specified node from the list of children of the imported scene node.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)> &* **node** - Node to be removed from the list of children.

## Ptr < ImportNode > getChild ( int index ) const

Returns the child node of the imported node having the specified index.
### Arguments

- *int* **index** - Child node index within the range from 0 to ([total number of children](#getNumChildren_int) - 1).

### Return value

Child node of the imported node with the specified index.
## int getNumChildren ( ) const

Returns the number of children of the imported node.
### Return value

Number of node's children.
