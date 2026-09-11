# Unigine::ImportMesh Class (CPP)

**Header:** #include <UnigineImport.h>


This class is an intermediate representation of a static mesh from a source file. A mesh is organized as a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cpp.md)* elements, each containing *[ImportSurface](../../../../api/library/common/import/class.importsurface_cpp.md)* elements with material assignments and rendering settings. During import, it is converted to a UNIGINE *[Mesh](../../../../api/library/rendering/class.mesh_cpp.md)* by an [import processor](../../../../api/library/common/import/class.importprocessor_cpp.md). For skinned meshes with skeleton support, see *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cpp.md)*.


## ImportMesh Class

### Members

## void setData ( void * data )

Sets a new metadata of the imported mesh.
### Arguments

- *void ** **data** - The mesh metadata.

## void * getData () const

Returns the current metadata of the imported mesh.
### Return value

Current mesh metadata.
## void setName ( const char * name )

Sets a new name of the mesh.
### Arguments

- *const char ** **name** - The mesh name.

## const char * getName () const

Returns the current name of the mesh.
### Return value

Current mesh name.
## void setFilepath ( const char * filepath )

Sets a new path to the output mesh file.
### Arguments

- *const char ** **filepath** - The output mesh file path.

## const char * getFilepath () const

Returns the current path to the output mesh file.
### Return value

Current output mesh file path.
---

## static ImportMeshPtr create ( )

Constructor. Creates an empty *ImportMesh* instance.
## int getNumNodes ( ) const

Returns the number of import nodes to which the mesh is attached as an attribute.
### Return value

Number of nodes to which the mesh is attached as an attribute.
## void addNode ( const Ptr < ImportNode > & node )

Adds a new node to the list of import nodes to which the mesh is attached as an attribute.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)> &* **node** - New import node to be added.

## bool removeNode ( const Ptr < ImportNode > & node )

Removes the specified import node from the list of import nodes to which the mesh is attached as an attribute.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)> &* **node** - Node to be removed.

### Return value

true if the specified import node was successfully removed from the list; otherwise false.
## Ptr < ImportNode > getNode ( int index ) const

Returns an import node with the specified index from the list of import nodes to which the mesh is attached as an attribute.
### Arguments

- *int* **index** - Index of node in the list.

### Return value

Import node with the specified index (if it exists).
## int getNumGeometries ( ) const

Returns the number of elements in the mesh geometry list (a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cpp.md)* elements making up the geometry of the mesh).
### Return value

Number of elements in the mesh geometry list.
## Ptr < ImportGeometry > addGeometry ( )

Adds a new element to the mesh geometry list and returns the corresponding *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cpp.md)* instance.
### Return value

New added geometry element.
## void copyGeometriesFrom ( const Ptr < ImportMesh > & other )

Copies all geometry elements from the specified source mesh and adds them to the mesh geometry list (a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cpp.md)* elements making up the geometry of the mesh).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportMesh](../../../../api/library/common/import/class.importmesh_cpp.md)> &* **other** - Source mesh.

## void moveGeometriesFrom ( const Ptr < ImportMesh > & other )

Moves all geometry elements from the specified source mesh and adds them to the mesh geometry list (a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cpp.md)* elements making up the geometry of the mesh).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportMesh](../../../../api/library/common/import/class.importmesh_cpp.md)> &* **other** - Source mesh.

## Ptr < ImportGeometry > getGeometry ( int index ) const

Returns an element of mesh geometry by its index. Geometry of the mesh can consist of multiple *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cpp.md)* elements.
### Arguments

- *int* **index** - Index of geometry element.

### Return value

Geometry element with the specified index.
## void clearGeometries ( )

Clears the geometry list of the mesh (a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cpp.md)* elements making up the geometry of the mesh).
