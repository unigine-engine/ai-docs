# Unigine::ImportMesh Class (CS)


This class is an intermediate representation of a static mesh from a source file. A mesh is organized as a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cs.md)* elements, each containing *[ImportSurface](../../../../api/library/common/import/class.importsurface_cs.md)* elements with material assignments and rendering settings. During import, it is converted to a UNIGINE *[Mesh](../../../../api/library/rendering/class.mesh_cs.md)* by an [import processor](../../../../api/library/common/import/class.importprocessor_cs.md). For skinned meshes with skeleton support, see *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)*.


## ImportMesh Class

### Properties

## IntPtr Data

The metadata of the imported mesh.
## string Name

The name of the mesh.
## string Filepath

The path to the output mesh file.
### Members

---

## ImportMesh ( )

Constructor. Creates an empty *ImportMesh* instance.
## int GetNumNodes ( )

Returns the number of import nodes to which the mesh is attached as an attribute.
### Return value

Number of nodes to which the mesh is attached as an attribute.
## void AddNode ( ImportNode node )

Adds a new node to the list of import nodes to which the mesh is attached as an attribute.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **node** - New import node to be added.

## bool RemoveNode ( ImportNode node )

Removes the specified import node from the list of import nodes to which the mesh is attached as an attribute.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **node** - Node to be removed.

### Return value

true if the specified import node was successfully removed from the list; otherwise false.
## ImportNode GetNode ( int index )

Returns an import node with the specified index from the list of import nodes to which the mesh is attached as an attribute.
### Arguments

- *int* **index** - Index of node in the list.

### Return value

Import node with the specified index (if it exists).
## int GetNumGeometries ( )

Returns the number of elements in the mesh geometry list (a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cs.md)* elements making up the geometry of the mesh).
### Return value

Number of elements in the mesh geometry list.
## ImportGeometry AddGeometry ( )

Adds a new element to the mesh geometry list and returns the corresponding *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cs.md)* instance.
### Return value

New added geometry element.
## void CopyGeometriesFrom ( ImportMesh other )

Copies all geometry elements from the specified source mesh and adds them to the mesh geometry list (a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cs.md)* elements making up the geometry of the mesh).
### Arguments

- *[ImportMesh](../../../../api/library/common/import/class.importmesh_cs.md)* **other** - Source mesh.

## void MoveGeometriesFrom ( ImportMesh other )

Moves all geometry elements from the specified source mesh and adds them to the mesh geometry list (a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cs.md)* elements making up the geometry of the mesh).
### Arguments

- *[ImportMesh](../../../../api/library/common/import/class.importmesh_cs.md)* **other** - Source mesh.

## ImportGeometry GetGeometry ( int index )

Returns an element of mesh geometry by its index. Geometry of the mesh can consist of multiple *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cs.md)* elements.
### Arguments

- *int* **index** - Index of geometry element.

### Return value

Geometry element with the specified index.
## void ClearGeometries ( )

Clears the geometry list of the mesh (a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cs.md)* elements making up the geometry of the mesh).
