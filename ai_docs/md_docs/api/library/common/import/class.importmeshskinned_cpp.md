# Unigine::ImportMeshSkinned Class (CPP)

**Header:** #include <UnigineImport.h>


This class is an intermediate representation of a skinned mesh from a source file. Unlike *[ImportMesh](../../../../api/library/common/import/class.importmesh_cpp.md)* (used for static geometry), it also stores a reference to an *[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cpp.md)* for joint-based deformation and a path to the associated animation file. During import, it is converted to a *MeshSkinned* asset.


## ImportMeshSkinned Class

### Members

## void setData ( void * data )

Sets a new metadata of the imported skinned mesh.
### Arguments

- *void ** **data** - The skinned mesh metadata.

## void * getData () const

Returns the current metadata of the imported skinned mesh.
### Return value

Current skinned mesh metadata.
## void setName ( const char * name )

Sets a new name of the skinned mesh.
### Arguments

- *const char ** **name** - The skinned mesh name.

## const char * getName () const

Returns the current name of the skinned mesh.
### Return value

Current skinned mesh name.
## void setFilepath ( const char * filepath )

Sets a new path to the output skinned mesh file.
### Arguments

- *const char ** **filepath** - The output skinned mesh file path.

## const char * getFilepath () const

Returns the current path to the output skinned mesh file.
### Return value

Current output skinned mesh file path.
## void setAnimationFilepath ( const char * filepath )

Sets a new path to the output animation file associated with this skinned mesh.
### Arguments

- *const char ** **filepath** - The output animation file path.

## const char * getAnimationFilepath () const

Returns the current path to the output animation file associated with this skinned mesh.
### Return value

Current output animation file path.
## void setSkeleton ( const Ptr < ImportSkeleton >& skeleton )

Sets a new [import skeleton](../../../../api/library/common/import/class.importskeleton_cpp.md) assigned to the skinned mesh.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cpp.md)>&* **skeleton** - The skeleton assigned to the skinned mesh.

## Ptr < ImportSkeleton > getSkeleton () const

Returns the current [import skeleton](../../../../api/library/common/import/class.importskeleton_cpp.md) assigned to the skinned mesh.
### Return value

Current skeleton assigned to the skinned mesh.
---

## static ImportMeshSkinnedPtr create ( )

Constructor. Creates an empty *ImportMeshSkinned* instance.
## int getNumNodes ( ) const

Returns the number of import nodes to which the skinned mesh is attached as an attribute.
### Return value

Number of nodes to which the skinned mesh is attached as an attribute.
## void addNode ( const Ptr < ImportNode > & node )

Adds a new node to the list of import nodes to which the skinned mesh is attached as an attribute.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)> &* **node** - New import node to be added.

## bool removeNode ( const Ptr < ImportNode > & node )

Removes the specified import node from the list of import nodes to which the skinned mesh is attached as an attribute.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)> &* **node** - Node to be removed.

### Return value

true if the specified import node was successfully removed from the list; otherwise false.
## Ptr < ImportNode > getNode ( int index ) const

Returns an import node with the specified index from the list of import nodes to which the skinned mesh is attached as an attribute.
### Arguments

- *int* **index** - Index of node in the list.

### Return value

Import node with the specified index (if it exists).
## int getNumGeometries ( ) const

Returns the number of elements in the skinned mesh geometry list (a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cpp.md)* elements making up the geometry of the skinned mesh).
### Return value

Number of elements in the skinned mesh geometry list.
## Ptr < ImportGeometry > addGeometry ( )

Adds a new element to the skinned mesh geometry list and returns the corresponding *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cpp.md)* instance.
### Return value

New added geometry element.
## void copyGeometriesFrom ( const Ptr < ImportMeshSkinned > & other )

Copies all geometry elements from the specified source skinned mesh and adds them to the skinned mesh geometry list.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cpp.md)> &* **other** - Source skinned mesh.

## void moveGeometriesFrom ( const Ptr < ImportMeshSkinned > & other )

Moves all geometry elements from the specified source skinned mesh and adds them to the skinned mesh geometry list.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cpp.md)> &* **other** - Source skinned mesh.

## Ptr < ImportGeometry > getGeometry ( int index ) const

Returns an element of skinned mesh geometry by its index. Geometry of the skinned mesh can consist of multiple *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cpp.md)* elements.
### Arguments

- *int* **index** - Index of geometry element.

### Return value

Geometry element with the specified index.
## void clearGeometries ( )

Clears the geometry list of the skinned mesh.
