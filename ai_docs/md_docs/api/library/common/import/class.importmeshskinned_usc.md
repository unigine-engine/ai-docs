# Unigine::ImportMeshSkinned Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is an intermediate representation of a skinned mesh from a source file. Unlike *[ImportMesh](../../../../api/library/common/import/class.importmesh_usc.md)* (used for static geometry), it also stores a reference to an *[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_usc.md)* for joint-based deformation and a path to the associated animation file. During import, it is converted to a *MeshSkinned* asset.


## ImportMeshSkinned Class

### Members

## void setData ( vptr data )

Sets a new metadata of the imported skinned mesh.
### Arguments

- *vptr* **data** - The skinned mesh metadata.

## vptr getData () const

Returns the current metadata of the imported skinned mesh.
### Return value

Current skinned mesh metadata.
## void setName ( string name )

Sets a new name of the skinned mesh.
### Arguments

- *string* **name** - The skinned mesh name.

## const char * getName () const

Returns the current name of the skinned mesh.
### Return value

Current skinned mesh name.
## void setFilepath ( string filepath )

Sets a new path to the output skinned mesh file.
### Arguments

- *string* **filepath** - The output skinned mesh file path.

## const char * getFilepath () const

Returns the current path to the output skinned mesh file.
### Return value

Current output skinned mesh file path.
## void setAnimationFilepath ( string filepath )

Sets a new path to the output animation file associated with this skinned mesh.
### Arguments

- *string* **filepath** - The output animation file path.

## const char * getAnimationFilepath () const

Returns the current path to the output animation file associated with this skinned mesh.
### Return value

Current output animation file path.
## void setSkeleton ( ImportSkeleton skeleton )

Sets a new [import skeleton](../../../../api/library/common/import/class.importskeleton_usc.md) assigned to the skinned mesh.
### Arguments

- *[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_usc.md)* **skeleton** - The skeleton assigned to the skinned mesh.

## ImportSkeleton getSkeleton () const

Returns the current [import skeleton](../../../../api/library/common/import/class.importskeleton_usc.md) assigned to the skinned mesh.
### Return value

Current skeleton assigned to the skinned mesh.
---

## static ImportMeshSkinned ( )

Constructor. Creates an empty *ImportMeshSkinned* instance.
## int getNumNodes ( )

Returns the number of import nodes to which the skinned mesh is attached as an attribute.
### Return value

Number of nodes to which the skinned mesh is attached as an attribute.
## void addNode ( ImportNode node )

Adds a new node to the list of import nodes to which the skinned mesh is attached as an attribute.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_usc.md)* **node** - New import node to be added.

## bool removeNode ( ImportNode node )

Removes the specified import node from the list of import nodes to which the skinned mesh is attached as an attribute.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_usc.md)* **node** - Node to be removed.

### Return value

true if the specified import node was successfully removed from the list; otherwise false.
## ImportNode getNode ( int index )

Returns an import node with the specified index from the list of import nodes to which the skinned mesh is attached as an attribute.
### Arguments

- *int* **index** - Index of node in the list.

### Return value

Import node with the specified index (if it exists).
## int getNumGeometries ( )

Returns the number of elements in the skinned mesh geometry list (a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_usc.md)* elements making up the geometry of the skinned mesh).
### Return value

Number of elements in the skinned mesh geometry list.
## ImportGeometry addGeometry ( )

Adds a new element to the skinned mesh geometry list and returns the corresponding *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_usc.md)* instance.
### Return value

New added geometry element.
## void copyGeometriesFrom ( ImportMeshSkinned other )

Copies all geometry elements from the specified source skinned mesh and adds them to the skinned mesh geometry list.
### Arguments

- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_usc.md)* **other** - Source skinned mesh.

## void moveGeometriesFrom ( ImportMeshSkinned other )

Moves all geometry elements from the specified source skinned mesh and adds them to the skinned mesh geometry list.
### Arguments

- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_usc.md)* **other** - Source skinned mesh.

## ImportGeometry getGeometry ( int index )

Returns an element of skinned mesh geometry by its index. Geometry of the skinned mesh can consist of multiple *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_usc.md)* elements.
### Arguments

- *int* **index** - Index of geometry element.

### Return value

Geometry element with the specified index.
## void clearGeometries ( )

Clears the geometry list of the skinned mesh.
