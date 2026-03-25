# Unigine::ImportGeometry Class (CS)


This class represents a geometry element within an [ImportMesh](../../../../api/library/common/import/class.importmesh_cs.md) or [ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md). A mesh can contain multiple geometries, each with its own transformation matrix and a set of [ImportSurface](../../../../api/library/common/import/class.importsurface_cs.md) elements defining individual renderable surfaces.


## ImportGeometry Class

### Properties

## WorldBoundBox BoundBox

The bounding box of the geometry element.
## IntPtr Data

The metadata of the imported geometry element.
## dmat4 Transform

The transformation matrix of the imported geometry element.
### Members

---

## void CopyFrom ( ImportGeometry o )

Copies the data from the specified source geometry element.
### Arguments

- *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cs.md)* **o** - Source geometry element.

## ImportSurface AddSurface ( )

Adds a new surface to the list of surfaces of the geometry element and returns the corresponding *[ImportSurface](../../../../api/library/common/import/class.importsurface_cs.md)* instance.
### Return value

New added surface.
## void CopySurfacesFrom ( ImportGeometry other )

Copies all surfaces from the specified source geometry element.
### Arguments

- *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cs.md)* **other** - Source geometry element.

## void MoveSurfacesFrom ( ImportGeometry other )

Moves all surfaces from the specified source geometry element.
### Arguments

- *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cs.md)* **other** - Source geometry element.

## ImportSurface GetSurface ( int index )

Returns a surface of the geometry element by its index in the list.
### Arguments

- *int* **index** - Surface index within the range from 0 to ([total number of surfaces](#getNumSurfaces_int) - 1).

### Return value

Imported surface with the specified index.
## int GetNumSurfaces ( )

Returns the number of surfaces in the list. List of surfaces is represented as a set of *[ImportSurface](../../../../api/library/common/import/class.importsurface_cs.md)* structures.
### Return value

Number of surfaces in the imported geometry element.
## void ClearSurfaces ( )

Clears the list of surfaces of the geometry element.
