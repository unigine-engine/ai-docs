# Unigine::ImportMeshSkinned Class (CS)


This class is an intermediate representation of a skinned mesh from a source file. Unlike *[ImportMesh](../../../../api/library/common/import/class.importmesh_cs.md)* (used for static geometry), it also stores a reference to an *[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cs.md)* for joint-based deformation and a path to the associated animation file. During import, it is converted to a *MeshSkinned* asset.


## ImportMeshSkinned Class

### Properties

## IntPtr Data

The metadata of the imported skinned mesh.
## string Name

The name of the skinned mesh.
## string Filepath

The path to the output skinned mesh file.
## string AnimationFilepath

The path to the output animation file associated with this skinned mesh.
## ImportSkeleton Skeleton

The [import skeleton](../../../../api/library/common/import/class.importskeleton_cs.md) assigned to the skinned mesh.
### Members

---

## ImportMeshSkinned ( )

Constructor. Creates an empty *ImportMeshSkinned* instance.
## int GetNumNodes ( )

Returns the number of import nodes to which the skinned mesh is attached as an attribute.
### Return value

Number of nodes to which the skinned mesh is attached as an attribute.
## void AddNode ( ImportNode node )

Adds a new node to the list of import nodes to which the skinned mesh is attached as an attribute.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **node** - New import node to be added.

## bool RemoveNode ( ImportNode node )

Removes the specified import node from the list of import nodes to which the skinned mesh is attached as an attribute.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **node** - Node to be removed.

### Return value

true if the specified import node was successfully removed from the list; otherwise false.
## ImportNode GetNode ( int index )

Returns an import node with the specified index from the list of import nodes to which the skinned mesh is attached as an attribute.
### Arguments

- *int* **index** - Index of node in the list.

### Return value

Import node with the specified index (if it exists).
## int GetNumGeometries ( )

Returns the number of elements in the skinned mesh geometry list (a set of *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cs.md)* elements making up the geometry of the skinned mesh).
### Return value

Number of elements in the skinned mesh geometry list.
## ImportGeometry AddGeometry ( )

Adds a new element to the skinned mesh geometry list and returns the corresponding *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cs.md)* instance.
### Return value

New added geometry element.
## void CopyGeometriesFrom ( ImportMeshSkinned other )

Copies all geometry elements from the specified source skinned mesh and adds them to the skinned mesh geometry list.
### Arguments

- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* **other** - Source skinned mesh.

## void MoveGeometriesFrom ( ImportMeshSkinned other )

Moves all geometry elements from the specified source skinned mesh and adds them to the skinned mesh geometry list.
### Arguments

- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* **other** - Source skinned mesh.

## ImportGeometry GetGeometry ( int index )

Returns an element of skinned mesh geometry by its index. Geometry of the skinned mesh can consist of multiple *[ImportGeometry](../../../../api/library/common/import/class.importgeometry_cs.md)* elements.
### Arguments

- *int* **index** - Index of geometry element.

### Return value

Geometry element with the specified index.
## void ClearGeometries ( )

Clears the geometry list of the skinned mesh.
