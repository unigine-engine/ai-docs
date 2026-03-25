# Unigine::ImportGeometry Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class represents a geometry element within an [ImportMesh](../../../../api/library/common/import/class.importmesh_usc.md) or [ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_usc.md). A mesh can contain multiple geometries, each with its own transformation matrix and a set of [ImportSurface](../../../../api/library/common/import/class.importsurface_usc.md) elements defining individual renderable surfaces.


## ImportGeometry Class

### Members

## void setBoundBox ( WorldBoundBox box )

Sets a new bounding box of the geometry element.
### Arguments

- *WorldBoundBox* **box** - The geometry element bounding box.

## WorldBoundBox getBoundBox () const

Returns the current bounding box of the geometry element.
### Return value

Current geometry element bounding box.
## void setData ( vptr data )

Sets a new metadata of the imported geometry element.
### Arguments

- *vptr* **data** - The geometry element metadata.

## vptr getData () const

Returns the current metadata of the imported geometry element.
### Return value

Current geometry element metadata.
## void setTransform ( dmat4 transform )

Sets a new transformation matrix of the imported geometry element.
### Arguments

- *dmat4* **transform** - The geometry element transformation matrix.

## dmat4 getTransform () const

Returns the current transformation matrix of the imported geometry element.
### Return value

Current geometry element transformation matrix.
---

## void copyFrom ( ImportGeometry o )

Copies the data from the specified source geometry element.
### Arguments

- *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_usc.md)* **o** - Source geometry element.

## ImportSurface addSurface ( )

Adds a new surface to the list of surfaces of the geometry element and returns the corresponding *[ImportSurface](../../../../api/library/common/import/class.importsurface_usc.md)* instance.
### Return value

New added surface.
## void copySurfacesFrom ( ImportGeometry other )

Copies all surfaces from the specified source geometry element.
### Arguments

- *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_usc.md)* **other** - Source geometry element.

## void moveSurfacesFrom ( ImportGeometry other )

Moves all surfaces from the specified source geometry element.
### Arguments

- *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_usc.md)* **other** - Source geometry element.

## ImportSurface getSurface ( int index )

Returns a surface of the geometry element by its index in the list.
### Arguments

- *int* **index** - Surface index within the range from 0 to ([total number of surfaces](#getNumSurfaces_int) - 1).

### Return value

Imported surface with the specified index.
## int getNumSurfaces ( )

Returns the number of surfaces in the list. List of surfaces is represented as a set of *[ImportSurface](../../../../api/library/common/import/class.importsurface_usc.md)* structures.
### Return value

Number of surfaces in the imported geometry element.
## void clearSurfaces ( )

Clears the list of surfaces of the geometry element.
