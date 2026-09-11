# MeshSkinned Class (CS)


This class is a container for skinned mesh geometry data - vertices, normals, tangents, texture coordinates, colors, indices, and joint skinning weights. It provides an interface for loading, manipulating, and saving skinned meshes.


The geometry is organized into surfaces, each of which can have multiple morph targets. Each vertex stores up to 4 joint influences (indices and weights) for skeletal animation.


Key concepts:


- Source joints - the joint hierarchy (names, parent-child relationships, bind poses) referenced by this mesh.
- Surfaces - subsets of geometry, each with its own vertex/index data and bounding volumes.
- Morph targets - per-surface variants of vertex positions, normals, and tangents for blend shape animation.
- Coordinate indices (*CIndices*) - indices into the vertex position buffer.
- Triangle indices (*TIndices*) - indices into the unique vertex attribute buffer (normals, tangents, UVs).


## MeshSkinned Class

### Properties

## 🔒︎ Skeleton SharedSkeleton

The skeleton instance associated with this mesh, loaded from the shared skeleton path or GUID.
## UGUID SharedSkeletonFileGUID

The file GUID of the skeleton associated with this mesh.
## string SharedSkeletonPath

The file path of the skeleton associated with this mesh.
## 🔒︎ int NumSrcJoints

The total number of source joints in this mesh.
## 🔒︎ int NumSurfaces

The total number of surfaces in this mesh.
## 🔒︎ BoundBox BoundBox

The axis-aligned bounding box enclosing the entire mesh geometry.
## 🔒︎ BoundSphere BoundSphere

The bounding sphere enclosing the entire mesh geometry.
## 🔒︎ ulong SystemMemoryUsage

The total system memory used by this mesh, in bytes.
### Members

---

## MeshSkinned ( )

Creates an empty skinned mesh.
## MeshSkinned ( string path )

Creates a skinned mesh and loads data from the specified file.
### Arguments

- *string* **path** - Path to the mesh file.

## void InitSourceSkeleton ( Skeleton skeleton )

Initializes the source joint hierarchy from the specified skeleton instance.
### Arguments

- *[Skeleton](../../../api/library/animations/skeletal/class.skeleton_cs.md)* **skeleton** - Skeleton instance to initialize source joints from.

## void InitSourceSkeleton ( string path )

Initializes the source joint hierarchy from a skeleton loaded from the specified file path.
### Arguments

- *string* **path** - File path to the skeleton.

## void AssignFrom ( MeshSkinned mesh )

Copies all data from the source mesh: geometry, joints, and surfaces.
### Arguments

- *[MeshSkinned](../../../api/library/rendering/class.meshskinned_cs.md)* **mesh** - Source mesh instance.

## int Info ( string path )

Reads metadata from the specified mesh file without loading the full geometry data.
### Arguments

- *string* **path** - Path to the mesh file.

### Return value

1 if the file metadata was read successfully; otherwise, 0.
## int Load ( string path )

Loads the full mesh data from the specified file.
### Arguments

- *string* **path** - Path to the mesh file.

### Return value

1 if the mesh was loaded successfully; otherwise, 0.
## int Save ( string path )

Saves the mesh data to the specified file. Creates the file and any required subdirectories if they don't exist.
### Arguments

- *string* **path** - Path to the output file.

### Return value

1 if the mesh was saved successfully; otherwise, 0.
## void Clear ( )

Clears all mesh data: geometry, joints, and surfaces.
## bool FlipYZ ( int surface = -1 )

Flips the Y and Z axes for the specified surface (or all surfaces).
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if the operation was successful; otherwise, false.
## bool FlipTangent ( int surface = -1 )

Flips the tangent direction for the specified surface (or all surfaces).
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if the operation was successful; otherwise, false.
## bool CreateBounds ( int surface = -1 )

Recalculates bounding boxes and bounding spheres for the specified surface (or all surfaces).
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if bounds were created successfully; otherwise, false.
## bool RemoveIndices ( int surface = -1 )

Removes all indices from the specified surface (or all surfaces).
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if indices were removed successfully; otherwise, false.
## bool CreateIndices ( int surface = -1 )

Creates triangle and coordinate indices for the specified surface (or all surfaces).
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if indices were created successfully; otherwise, false.
## bool OptimizeIndices ( int flags , int surface = -1 )

Optimizes the index buffer for the specified surface (or all surfaces) using the given flags.
### Arguments

- *int* **flags** - Optimization flags.
- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if optimization was successful; otherwise, false.
## bool CreateNormals ( int surface = -1 , int target = -1 )

Creates normals for the specified surface and morph target by averaging face normals.
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.
- *int* **target** - Morph target index. Use -1 for all targets.

### Return value

true if normals were created successfully; otherwise, false.
## bool CreateNormals ( float angle , int surface = -1 , int target = -1 )

Creates normals with the specified angle threshold for smooth/hard edge detection.
### Arguments

- *float* **angle** - Angle threshold in degrees for smooth/hard edge detection.
- *int* **surface** - Surface index. Use -1 for all surfaces.
- *int* **target** - Morph target index. Use -1 for all targets.

### Return value

true if normals were created successfully; otherwise, false.
## bool CreateTangents ( int surface = -1 , int target = -1 )

Creates tangent basis vectors for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.
- *int* **target** - Morph target index. Use -1 for all targets.

### Return value

true if tangents were created successfully; otherwise, false.
## bool CreateTangents ( float angle , int[] surfaces )

Creates tangent basis vectors for the specified surfaces with the given angle threshold.
### Arguments

- *float* **angle** - Angle threshold in degrees.
- *int[]* **surfaces** - List of surface indices to process.

### Return value

true if tangents were created successfully; otherwise, false.
## int FindSrcJoint ( string name )

Searches for a source joint with the specified name and returns its index.
### Arguments

- *string* **name** - Joint name to search for.

### Return value

Source joint index, or -1 if not found.
## string GetSrcJointName ( int bone )

Returns the name of the source joint at the specified index.
### Arguments

- *int* **bone** - Source joint index.

### Return value

Joint name.
## int GetSrcJointParent ( int bone )

Returns the parent joint index for the specified source joint.
### Arguments

- *int* **bone** - Source joint index.

### Return value

Parent joint index, or -1 if the joint has no parent.
## mat4 GetSrcJointObjectITransform ( int joint )

Returns the inverse bind pose transformation matrix in object space for the specified source joint. Used for skinning calculations.
### Arguments

- *int* **joint** - Source joint index.

### Return value

Inverse bind pose matrix in object space.
## FloatTransform GetSrcJointBindLocalTransform ( int joint )

Returns the bind pose transform in local space (relative to the parent joint) for the specified source joint.
### Arguments

- *int* **joint** - Source joint index.

### Return value

Bind pose transform in local space.
## void SetSrcJointRestLocalTransform ( int index , FloatTransform transform )

Sets the rest pose transform in local space for the specified source joint.
### Arguments

- *int* **index** - Source joint index.
- *FloatTransform* **transform** - Rest pose transform in local space.

## FloatTransform GetSrcJointRestLocalTransform ( int index )

Returns the rest pose transform in local space for the specified source joint.
### Arguments

- *int* **index** - Source joint index.

### Return value

Rest pose transform in local space.
## int FindSurface ( string name )

Searches for a surface with the specified name and returns its index.
### Arguments

- *string* **name** - Surface name to search for.

### Return value

Surface index, or -1 if not found.
## void SortSurfaces ( )

Sorts surfaces alphabetically by name.
## void ClearSurface ( int surface = -1 , int target = -1 )

Clears geometry data for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.
- *int* **target** - Morph target index. Use -1 for all targets.

## int AddSurface ( string name = 0 )

Adds a new empty surface with the specified name.
### Arguments

- *string* **name** - Surface name. Can be empty.

### Return value

Index of the newly added surface.
## void SetSurfaceName ( int surface , string name )

Sets the name of the specified surface.
### Arguments

- *int* **surface** - Surface index.
- *string* **name** - Surface name.

## string GetSurfaceName ( int surface )

Returns the name of the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Surface name.
## void SetNumSurfaceTargets ( int surface , int num )

Sets the number of morph targets for the specified surface.
### Arguments

- *int* **surface** - Surface index.
- *int* **num** - Number of morph targets.

## int GetNumSurfaceTargets ( int surface )

Returns the number of morph targets for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of morph targets.
## void SetSurfaceTargetName ( int surface , int target , string name )

Sets the name of the specified morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.
- *string* **name** - Target name.

## string GetSurfaceTargetName ( int surface , int target )

Returns the name of the specified morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Target name.
## int FindSurfaceTarget ( int surface , string name )

Searches for a morph target by name within the specified surface.
### Arguments

- *int* **surface** - Surface index.
- *string* **name** - Target name to search for.

### Return value

Morph target index, or -1 if not found.
## int SetSurfaceTransform ( mat4 transform , int surface = -1 , int target = -1 )

Applies a transformation matrix to the vertices, normals, and tangents of the specified surface and morph target.
### Arguments

- *mat4* **transform** - Transformation matrix to apply.
- *int* **surface** - Surface index. Use -1 for all surfaces.
- *int* **target** - Morph target index. Use -1 for all targets.

### Return value

1 if the transform was applied successfully; otherwise, 0.
## int AddMeshSurface ( string v , MeshSkinned mesh , int surface , int target = -1 )

Adds a surface from the specified source mesh as a new surface with the given name.
### Arguments

- *string* **v** - Name for the new surface.
- *[MeshSkinned](../../../api/library/rendering/class.meshskinned_cs.md)* **mesh** - Source mesh to copy the surface from.
- *int* **surface** - Surface index in the source mesh.
- *int* **target** - Morph target index in the source surface. Use -1 for all targets.

### Return value

Index of the newly added surface.
## int AddMeshSurface ( int v , MeshSkinned mesh , int surface , int target = -1 )

Appends geometry from the specified source mesh surface to an existing surface in this mesh.
### Arguments

- *int* **v** - Destination surface index to append geometry to.
- *[MeshSkinned](../../../api/library/rendering/class.meshskinned_cs.md)* **mesh** - Source mesh to copy the surface from.
- *int* **surface** - Surface index in the source mesh.
- *int* **target** - Morph target index in the source surface. Use -1 for all targets.

### Return value

Destination surface index.
## int AddEmptySurface ( string name , int num_vertex , int num_indices )

Adds a new surface with pre-allocated vertex and index buffers.
### Arguments

- *string* **name** - Surface name.
- *int* **num_vertex** - Number of vertices to allocate.
- *int* **num_indices** - Number of indices to allocate.

### Return value

Index of the newly added surface.
## int AddSurfaceTarget ( int surface , string name = 0 )

Adds a new morph target to the specified surface.
### Arguments

- *int* **surface** - Surface index.
- *string* **name** - Target name. Can be empty.

### Return value

Index of the newly added morph target.
## int AddBoxSurface ( string name , vec3 size )

Adds a box primitive surface with the specified dimensions.
### Arguments

- *string* **name** - Surface name.
- *vec3* **size** - Box dimensions (width, height, depth).

### Return value

Index of the newly added surface.
## int AddPlaneSurface ( string name , float width , float height , float step )

Adds a plane primitive surface with the specified dimensions and tessellation step.
### Arguments

- *string* **name** - Surface name.
- *float* **width** - Plane width.
- *float* **height** - Plane height.
- *float* **step** - Tessellation step.

### Return value

Index of the newly added surface.
## int AddSphereSurface ( string name , float radius , int stacks , int slices )

Adds a sphere primitive surface with the specified radius and subdivisions.
### Arguments

- *string* **name** - Surface name.
- *float* **radius** - Sphere radius.
- *int* **stacks** - Number of horizontal subdivisions.
- *int* **slices** - Number of vertical subdivisions.

### Return value

Index of the newly added surface.
## int AddCapsuleSurface ( string name , float radius , float height , int stacks , int slices )

Adds a capsule primitive surface with the specified dimensions and subdivisions.
### Arguments

- *string* **name** - Surface name.
- *float* **radius** - Capsule radius.
- *float* **height** - Capsule height (cylinder part).
- *int* **stacks** - Number of horizontal subdivisions.
- *int* **slices** - Number of vertical subdivisions.

### Return value

Index of the newly added surface.
## int AddCylinderSurface ( string name , float radius , float height , int stacks , int slices )

Adds a cylinder primitive surface with the specified dimensions and subdivisions.
### Arguments

- *string* **name** - Surface name.
- *float* **radius** - Cylinder radius.
- *float* **height** - Cylinder height.
- *int* **stacks** - Number of horizontal subdivisions.
- *int* **slices** - Number of vertical subdivisions.

### Return value

Index of the newly added surface.
## int AddPrismSurface ( string name , float size_0 , float size_1 , float height , int sides )

Adds a prism primitive surface with the specified dimensions.
### Arguments

- *string* **name** - Surface name.
- *float* **size_0** - Bottom face size.
- *float* **size_1** - Top face size.
- *float* **height** - Prism height.
- *int* **sides** - Number of sides.

### Return value

Index of the newly added surface.
## int AddIcosahedronSurface ( string name , float radius )

Adds an icosahedron primitive surface with the specified radius.
### Arguments

- *string* **name** - Surface name.
- *float* **radius** - Icosahedron radius.

### Return value

Index of the newly added surface.
## int AddDodecahedronSurface ( string name , float radius )

Adds a dodecahedron primitive surface with the specified radius.
### Arguments

- *string* **name** - Surface name.
- *float* **radius** - Dodecahedron radius.

### Return value

Index of the newly added surface.
## int GetNumCVertex ( int surface = 0 )

Returns the number of unique coordinate vertices (positions) for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of unique coordinate vertices.
## int GetNumTVertex ( int surface = 0 )

Returns the number of unique triangle vertices (attribute combinations) for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of unique triangle vertices.
## int RemapCVertex ( int surface = 0 )

Remaps coordinate vertex indices for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

1 if remapping was successful; otherwise, 0.
## void SetNumWeights ( int size , int surface = 0 )

Sets the number of skinning weight entries for the specified surface.
### Arguments

- *int* **size** - Number of weight entries.
- *int* **surface** - Surface index.

## int GetNumWeights ( int surface = 0 )

Returns the number of skinning weight entries for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of weight entries.
## void SetWeightCount ( int num , int count , int surface = 0 )

Sets the number of joint influences for the specified weight entry.
### Arguments

- *int* **num** - Weight entry index.
- *int* **count** - Number of joint influences (1 to 4).
- *int* **surface** - Surface index.

## int GetWeightCount ( int num , int surface = 0 )

Returns the number of joint influences for the specified weight entry.
### Arguments

- *int* **num** - Weight entry index.
- *int* **surface** - Surface index.

### Return value

Number of joint influences.
## void SetWeightJoints ( int num , ivec4 joints , int surface = 0 )

Sets the joint indices for the specified weight entry. Each component of the ivec4 is a source joint index.
### Arguments

- *int* **num** - Weight entry index.
- *ivec4* **joints** - Four joint indices packed into an ivec4.
- *int* **surface** - Surface index.

## ivec4 GetWeightJoints ( int num , int surface = 0 )

Returns the joint indices for the specified weight entry.
### Arguments

- *int* **num** - Weight entry index.
- *int* **surface** - Surface index.

### Return value

Four joint indices packed into an ivec4.
## void SetWeightWeights ( int num , vec4 weights , int surface = 0 )

Sets the joint weights for the specified weight entry.
### Arguments

- *int* **num** - Weight entry index.
- *vec4* **weights** - Four joint weights packed into a vec4. Components should sum to 1.0.
- *int* **surface** - Surface index.

## vec4 GetWeightWeights ( int num , int surface = 0 )

Returns the joint weights for the specified weight entry.
### Arguments

- *int* **num** - Weight entry index.
- *int* **surface** - Surface index.

### Return value

Four joint weights packed into a vec4.
## void SetNumVertex ( int size , int surface = 0 , int target = 0 )

Sets the number of vertices for the specified surface and morph target.
### Arguments

- *int* **size** - Number of vertices.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## int GetNumVertex ( int surface , int target = 0 )

Returns the number of vertices for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Number of vertices.
## void AddVertex ( vec3[] vertices , int surface = 0 , int target = 0 )

Adds multiple vertices to the specified surface and morph target.
### Arguments

- *vec3[]* **vertices** - Array of vertex positions to add.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## void AddVertex ( vec3 vertex , int surface = 0 , int target = 0 )

Adds a single vertex to the specified surface and morph target.
### Arguments

- *vec3* **vertex** - Vertex position.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## void SetVertex ( int num , vec3 vertex , int surface = 0 , int target = 0 )

Sets the position of the vertex at the specified index.
### Arguments

- *int* **num** - Vertex index.
- *vec3* **vertex** - Vertex position.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## vec3 GetVertex ( int num , int surface = 0 , int target = 0 )

Returns the position of the vertex at the specified index.
### Arguments

- *int* **num** - Vertex index.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Vertex position.
## void SetNumTexCoords0 ( int size , int surface = 0 )

Sets the number of first UV channel texture coordinates for the specified surface.
### Arguments

- *int* **size** - Number of texture coordinates.
- *int* **surface** - Surface index.

## int GetNumTexCoords0 ( int surface = 0 )

Returns the number of first UV channel texture coordinates for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of texture coordinates.
## void AddTexCoords0 ( vec2[] texcoords , int surface = 0 )

Adds multiple first UV channel texture coordinates to the specified surface.
### Arguments

- *vec2[]* **texcoords** - Array of texture coordinates to add.
- *int* **surface** - Surface index.

## void AddTexCoord0 ( vec2 texcoord , int surface = 0 )

Adds a single first UV channel texture coordinate to the specified surface.
### Arguments

- *vec2* **texcoord** - Texture coordinate.
- *int* **surface** - Surface index.

## void SetTexCoord0 ( int num , vec2 texcoord , int surface = 0 )

Sets the first UV channel texture coordinate at the specified index.
### Arguments

- *int* **num** - Texture coordinate index.
- *vec2* **texcoord** - Texture coordinate.
- *int* **surface** - Surface index.

## vec2 GetTexCoord0 ( int num , int surface = 0 )

Returns the first UV channel texture coordinate at the specified index.
### Arguments

- *int* **num** - Texture coordinate index.
- *int* **surface** - Surface index.

### Return value

Texture coordinate.
## void SetNumTexCoords1 ( int size , int surface = 0 )

Sets the number of second UV channel texture coordinates for the specified surface.
### Arguments

- *int* **size** - Number of texture coordinates.
- *int* **surface** - Surface index.

## int GetNumTexCoords1 ( int surface = 0 )

Returns the number of second UV channel texture coordinates for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of texture coordinates.
## void AddTexCoords1 ( vec2[] texcoords , int surface = 0 )

Adds multiple second UV channel texture coordinates to the specified surface.
### Arguments

- *vec2[]* **texcoords** - Array of texture coordinates to add.
- *int* **surface** - Surface index.

## void AddTexCoord1 ( vec2 texcoord , int surface = 0 )

Adds a single second UV channel texture coordinate to the specified surface.
### Arguments

- *vec2* **texcoord** - Texture coordinate.
- *int* **surface** - Surface index.

## void SetTexCoord1 ( int num , vec2 texcoord , int surface = 0 )

Sets the second UV channel texture coordinate at the specified index.
### Arguments

- *int* **num** - Texture coordinate index.
- *vec2* **texcoord** - Texture coordinate.
- *int* **surface** - Surface index.

## vec2 GetTexCoord1 ( int num , int surface = 0 )

Returns the second UV channel texture coordinate at the specified index.
### Arguments

- *int* **num** - Texture coordinate index.
- *int* **surface** - Surface index.

### Return value

Texture coordinate.
## void SetNumNormals ( int size , int surface = 0 , int target = 0 )

Sets the number of normals for the specified surface and morph target.
### Arguments

- *int* **size** - Number of normals.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## int GetNumNormals ( int surface = 0 , int target = 0 )

Returns the number of normals for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Number of normals.
## void AddNormals ( vec3[] normals , int surface = 0 , int target = 0 )

Adds multiple normals to the specified surface and morph target.
### Arguments

- *vec3[]* **normals** - Array of normals to add.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## void AddNormal ( vec3 normal , int surface = 0 , int target = 0 )

Adds a single normal to the specified surface and morph target.
### Arguments

- *vec3* **normal** - Normal vector.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## void SetNormal ( int num , vec3 normal , int surface = 0 , int target = 0 )

Sets the normal at the specified index.
### Arguments

- *int* **num** - Normal index.
- *vec3* **normal** - Normal vector.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## vec3 GetNormal ( int num , int surface = 0 , int target = 0 )

Returns the normal at the specified index.
### Arguments

- *int* **num** - Normal index.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Normal vector.
## void SetNumTangents ( int size , int surface = 0 , int target = 0 )

Sets the number of tangents for the specified surface and morph target.
### Arguments

- *int* **size** - Number of tangents.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## int GetNumTangents ( int surface , int target = 0 )

Returns the number of tangents for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Number of tangents.
## void AddTangents ( quat[] tangents , int surface = 0 , int target = 0 )

Adds multiple tangents to the specified surface and morph target.
### Arguments

- *quat[]* **tangents** - Array of tangent quaternions to add.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## void AddTangent ( quat tangent , int surface = 0 , int target = 0 )

Adds a single tangent to the specified surface and morph target.
### Arguments

- *quat* **tangent** - Tangent quaternion encoding the tangent basis.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## void SetTangent ( int num , quat tangent , int surface = 0 , int target = 0 )

Sets the tangent at the specified index.
### Arguments

- *int* **num** - Tangent index.
- *quat* **tangent** - Tangent quaternion.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## quat GetTangent ( int num , int surface = 0 , int target = 0 )

Returns the tangent at the specified index.
### Arguments

- *int* **num** - Tangent index.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Tangent quaternion.
## void SetNumColors ( int size , int surface = 0 )

Sets the number of vertex colors for the specified surface.
### Arguments

- *int* **size** - Number of vertex colors.
- *int* **surface** - Surface index.

## int GetNumColors ( int surface = 0 )

Returns the number of vertex colors for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of vertex colors.
## void AddColors ( vec4[] colors , int surface = 0 )

Adds multiple vertex colors to the specified surface.
### Arguments

- *vec4[]* **colors** - Array of vertex colors to add.
- *int* **surface** - Surface index.

## void AddColor ( vec4 color , int surface = 0 )

Adds a single vertex color to the specified surface.
### Arguments

- *vec4* **color** - Vertex color (RGBA, 0.0 to 1.0 range).
- *int* **surface** - Surface index.

## void SetColor ( int num , vec4 color , int surface = 0 )

Sets the vertex color at the specified index.
### Arguments

- *int* **num** - Color index.
- *vec4* **color** - Vertex color (RGBA, 0.0 to 1.0 range).
- *int* **surface** - Surface index.

## vec4 GetColor ( int num , int surface = 0 )

Returns the vertex color at the specified index.
### Arguments

- *int* **num** - Color index.
- *int* **surface** - Surface index.

### Return value

Vertex color (RGBA, 0.0 to 1.0 range).
## void SetNumCIndices ( int size , int surface = 0 )

Sets the number of coordinate indices for the specified surface.
### Arguments

- *int* **size** - Number of coordinate indices.
- *int* **surface** - Surface index.

## int GetNumCIndices ( int surface = 0 )

Returns the number of coordinate indices for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of coordinate indices.
## void AddCIndices ( int[] indices , int surface = 0 )

Adds multiple coordinate indices to the specified surface.
### Arguments

- *int[]* **indices** - Array of coordinate indices to add.
- *int* **surface** - Surface index.

## void AddCIndex ( int index , int surface = 0 )

Adds a single coordinate index to the specified surface.
### Arguments

- *int* **index** - Coordinate index to add.
- *int* **surface** - Surface index.

## void SetCIndex ( int num , int index , int surface = 0 )

Sets the coordinate index at the specified position.
### Arguments

- *int* **num** - Position in the coordinate index buffer.
- *int* **index** - Coordinate index value.
- *int* **surface** - Surface index.

## int GetCIndex ( int num , int surface = 0 )

Returns the coordinate index at the specified position.
### Arguments

- *int* **num** - Position in the coordinate index buffer.
- *int* **surface** - Surface index.

### Return value

Coordinate index value.
## void SetNumTIndices ( int size , int surface = 0 )

Sets the number of triangle indices for the specified surface.
### Arguments

- *int* **size** - Number of triangle indices.
- *int* **surface** - Surface index.

## int GetNumTIndices ( int surface = 0 )

Returns the number of triangle indices for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of triangle indices.
## void AddTIndices ( int[] indices , int surface = 0 )

Adds multiple triangle indices to the specified surface.
### Arguments

- *int[]* **indices** - Array of triangle indices to add.
- *int* **surface** - Surface index.

## void AddTIndex ( int index , int surface = 0 )

Adds a single triangle index to the specified surface.
### Arguments

- *int* **index** - Triangle index to add.
- *int* **surface** - Surface index.

## void SetTIndex ( int num , int index , int surface = 0 )

Sets the triangle index at the specified position.
### Arguments

- *int* **num** - Position in the triangle index buffer.
- *int* **index** - Triangle index value.
- *int* **surface** - Surface index.

## int GetTIndex ( int num , int surface = 0 )

Returns the triangle index at the specified position.
### Arguments

- *int* **num** - Position in the triangle index buffer.
- *int* **surface** - Surface index.

### Return value

Triangle index value.
## void SetNumIndices ( int size , int surface = 0 )

Sets the number of rendering indices for the specified surface.
### Arguments

- *int* **size** - Number of rendering indices.
- *int* **surface** - Surface index.

## int GetNumIndices ( int surface = 0 )

Returns the number of rendering indices for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of rendering indices.
## void AddIndices ( int[] indices , int surface = 0 )

Adds multiple rendering indices to the specified surface.
### Arguments

- *int[]* **indices** - Array of rendering indices to add.
- *int* **surface** - Surface index.

## void AddIndex ( int index , int surface = 0 )

Adds a single rendering index to the specified surface.
### Arguments

- *int* **index** - Rendering index to add.
- *int* **surface** - Surface index.

## void SetIndex ( int num , int index , int surface = 0 )

Sets the rendering index at the specified position.
### Arguments

- *int* **num** - Position in the rendering index buffer.
- *int* **index** - Rendering index value.
- *int* **surface** - Surface index.

## int GetIndex ( int num , int surface = 0 )

Returns the rendering index at the specified position.
### Arguments

- *int* **num** - Position in the rendering index buffer.
- *int* **surface** - Surface index.

### Return value

Rendering index value.
## vec3[] GetVertices ( int surface = 0 , int target = 0 )

Returns direct access to the vertex positions array for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Reference to the vertex positions array.
## vec3[] GetNormals ( int surface = 0 , int target = 0 )

Returns direct access to the normals array for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Reference to the normals array.
## quat[] GetTangents ( int surface = 0 , int target = 0 )

Returns direct access to the tangent quaternions array for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Reference to the tangent quaternions array.
## vec2[] GetTexCoords0 ( int surface = 0 )

Returns direct access to the first UV channel texture coordinates array for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Reference to the first UV channel array.
## vec2[] GetTexCoords1 ( int surface = 0 )

Returns direct access to the second UV channel texture coordinates array for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Reference to the second UV channel array.
## bvec4[] GetColors ( int surface = 0 )

Returns direct access to the vertex colors array for the specified surface. Colors are stored as 8-bit per channel (bvec4).
### Arguments

- *int* **surface** - Surface index.

### Return value

Reference to the vertex colors array (8-bit per channel).
## int[] GetCIndices ( int surface = 0 )

Returns direct access to the coordinate indices array for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Reference to the coordinate indices array.
## int[] GetTIndices ( int surface = 0 )

Returns direct access to the triangle indices array for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Reference to the triangle indices array.
## BoundBox GetBoundBox ( int surface )

Returns the axis-aligned bounding box for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Bounding box for the specified surface.
## BoundSphere GetBoundSphere ( int surface )

Returns the bounding sphere for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Bounding sphere for the specified surface.
## void SetBoundBox ( BoundBox bb , int surface )

Sets the bounding box for the specified surface.
### Arguments

- *[BoundBox](../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box to set.
- *int* **surface** - Surface index.

## void SetBoundBox ( BoundBox bb )

Sets the bounding box for the entire mesh.
### Arguments

- *[BoundBox](../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box to set.

## void SetBoundSphere ( BoundSphere bs , int surface )

Sets the bounding sphere for the specified surface.
### Arguments

- *[BoundSphere](../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere to set.
- *int* **surface** - Surface index.

## void SetBoundSphere ( BoundSphere bs )

Sets the bounding sphere for the entire mesh.
### Arguments

- *[BoundSphere](../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere to set.
