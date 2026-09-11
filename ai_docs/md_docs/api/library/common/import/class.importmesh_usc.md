# Unigine::ImportMesh Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is an intermediate representation of a static mesh from a source file. A mesh is organized as a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_usc.md)* elements, each containing *[ImportSurface](../../../../api/library/common/import/class.importsurface_usc.md)* elements with material assignments and rendering settings. During import, it is converted to a UNIGINE *[Mesh](../../../../api/library/rendering/class.mesh_usc.md)* by an [import processor](../../../../api/library/common/import/class.importprocessor_usc.md). For skinned meshes with skeleton support, see *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_usc.md)*.


## ImportMesh Class

### Members

## void setData ( vptr data )

Sets a new metadata of the imported mesh.
### Arguments

- *vptr* **data** - The mesh metadata.

## vptr getData () const

Returns the current metadata of the imported mesh.
### Return value

Current mesh metadata.
## void setName ( string name )

Sets a new name of the mesh.
### Arguments

- *string* **name** - The mesh name.

## const char * getName () const

Returns the current name of the mesh.
### Return value

Current mesh name.
## void setFilepath ( string filepath )

Sets a new path to the output mesh file.
### Arguments

- *string* **filepath** - The output mesh file path.

## const char * getFilepath () const

Returns the current path to the output mesh file.
### Return value

Current output mesh file path.
---

## static ImportMesh ( )

Constructor. Creates an empty *ImportMesh* instance.
## int getNumNodes ( )

Returns the number of import nodes to which the mesh is attached as an attribute.
### Return value

Number of nodes to which the mesh is attached as an attribute.
## void addNode ( ImportNode node )

Adds a new node to the list of import nodes to which the mesh is attached as an attribute.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_usc.md)* **node** - New import node to be added.

## bool removeNode ( ImportNode node )

Removes the specified import node from the list of import nodes to which the mesh is attached as an attribute.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_usc.md)* **node** - Node to be removed.

### Return value

true if the specified import node was successfully removed from the list; otherwise false.
## ImportNode getNode ( int index )

Returns an import node with the specified index from the list of import nodes to which the mesh is attached as an attribute.
### Arguments

- *int* **index** - Index of node in the list.

### Return value

Import node with the specified index (if it exists).
## int getNumGeometries ( )

Returns the number of elements in the mesh geometry list (a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_usc.md)* elements making up the geometry of the mesh).
### Return value

Number of elements in the mesh geometry list.
## ImportGeometry addGeometry ( )

Adds a new element to the mesh geometry list and returns the corresponding *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_usc.md)* instance.
### Return value

New added geometry element.
## void copyGeometriesFrom ( ImportMesh other )

Copies all geometry elements from the specified source mesh and adds them to the mesh geometry list (a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_usc.md)* elements making up the geometry of the mesh).
### Arguments

- *[ImportMesh](../../../../api/library/common/import/class.importmesh_usc.md)* **other** - Source mesh.

## void moveGeometriesFrom ( ImportMesh other )

Moves all geometry elements from the specified source mesh and adds them to the mesh geometry list (a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_usc.md)* elements making up the geometry of the mesh).
### Arguments

- *[ImportMesh](../../../../api/library/common/import/class.importmesh_usc.md)* **other** - Source mesh.

## ImportGeometry getGeometry ( int index )

Returns an element of mesh geometry by its index. Geometry of the mesh can consist of multiple *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_usc.md)* elements.
### Arguments

- *int* **index** - Index of geometry element.

### Return value

Geometry element with the specified index.
## void clearGeometries ( )

Clears the geometry list of the mesh (a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_usc.md)* elements making up the geometry of the mesh).
