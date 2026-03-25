# Unigine::ImportGeometry Class (CPP)

**Header:** #include <UnigineImport.h>


This class represents a geometry element within an [ImportMesh](../../../../api/library/common/import/class.importmesh_cpp.md) or [ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cpp.md). A mesh can contain multiple geometries, each with its own transformation matrix and a set of [ImportSurface](../../../../api/library/common/import/class.importsurface_cpp.md) elements defining individual renderable surfaces.


## ImportGeometry Class

### Members

## void setBoundBox ( const Math:: WorldBoundBox & box )

Sets a new bounding box of the geometry element.
### Arguments

- *const  Math::[WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md)&* **box** - The geometry element bounding box.

## Math:: WorldBoundBox getBoundBox () const

Returns the current bounding box of the geometry element.
### Return value

Current geometry element bounding box.
## void setData ( void * data )

Sets a new metadata of the imported geometry element.
### Arguments

- *void ** **data** - The geometry element metadata.

## void * getData () const

Returns the current metadata of the imported geometry element.
### Return value

Current geometry element metadata.
## void setTransform ( const Math:: dmat4 & transform )

Sets a new transformation matrix of the imported geometry element.
### Arguments

- *const  Math::[dmat4](../../../../api/library/math/class.dmat4_cpp.md)&* **transform** - The geometry element transformation matrix.

## Math:: dmat4 getTransform () const

Returns the current transformation matrix of the imported geometry element.
### Return value

Current geometry element transformation matrix.
---

## void copyFrom ( const Ptr < ImportGeometry > & o )

Copies the data from the specified source geometry element.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cpp.md)> &* **o** - Source geometry element.

## Ptr < ImportSurface > addSurface ( )

Adds a new surface to the list of surfaces of the geometry element and returns the corresponding *[ImportSurface](../../../../api/library/common/import/class.importsurface_cpp.md)* instance.
### Return value

New added surface.
## void copySurfacesFrom ( const Ptr < ImportGeometry > & other )

Copies all surfaces from the specified source geometry element.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cpp.md)> &* **other** - Source geometry element.

## void moveSurfacesFrom ( const Ptr < ImportGeometry > & other )

Moves all surfaces from the specified source geometry element.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cpp.md)> &* **other** - Source geometry element.

## Ptr < ImportSurface > getSurface ( int index ) const

Returns a surface of the geometry element by its index in the list.
### Arguments

- *int* **index** - Surface index within the range from 0 to ([total number of surfaces](#getNumSurfaces_int) - 1).

### Return value

Imported surface with the specified index.
## int getNumSurfaces ( ) const

Returns the number of surfaces in the list. List of surfaces is represented as a set of *[ImportSurface](../../../../api/library/common/import/class.importsurface_cpp.md)* structures.
### Return value

Number of surfaces in the imported geometry element.
## void clearSurfaces ( )

Clears the list of surfaces of the geometry element.
