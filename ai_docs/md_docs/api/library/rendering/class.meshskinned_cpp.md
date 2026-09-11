# MeshSkinned Class (CPP)

**Header:** #include <UnigineMesh.h>


This class is a container for skinned mesh geometry data - vertices, normals, tangents, texture coordinates, colors, indices, and joint skinning weights. It provides an interface for loading, manipulating, and saving skinned meshes.


The geometry is organized into surfaces, each of which can have multiple morph targets. Each vertex stores up to 4 joint influences (indices and weights) for skeletal animation.


Key concepts:


- Source joints - the joint hierarchy (names, parent-child relationships, bind poses) referenced by this mesh.
- Surfaces - subsets of geometry, each with its own vertex/index data and bounding volumes.
- Morph targets - per-surface variants of vertex positions, normals, and tangents for blend shape animation.
- Coordinate indices (*CIndices*) - indices into the vertex position buffer.
- Triangle indices (*TIndices*) - indices into the unique vertex attribute buffer (normals, tangents, UVs).


## MeshSkinned Class

### Members

## getSharedSkeleton () const

Returns the current skeleton instance associated with this mesh, loaded from the shared skeleton path or GUID.
### Return value

Current shared skeleton instance.
## void setSharedSkeletonFileGUID ( )

Sets a new file GUID of the skeleton associated with this mesh.
### Arguments

- **guid** - The shared skeleton file GUID.

## getSharedSkeletonFileGUID () const

Returns the current file GUID of the skeleton associated with this mesh.
### Return value

Current shared skeleton file GUID.
## void setSharedSkeletonPath ( )

Sets a new file path of the skeleton associated with this mesh.
### Arguments

- **path** - The shared skeleton file path.

## const char * getSharedSkeletonPath () const

Returns the current file path of the skeleton associated with this mesh.
### Return value

Current shared skeleton file path.
## getNumSrcJoints () const

Returns the current total number of source joints in this mesh.
### Return value

Current number of source joints.
## getNumSurfaces () const

Returns the current total number of surfaces in this mesh.
### Return value

Current number of surfaces.
## getBoundBox () const

Returns the current axis-aligned bounding box enclosing the entire mesh geometry.
### Return value

Current mesh bounding box.
## getBoundSphere () const

Returns the current bounding sphere enclosing the entire mesh geometry.
### Return value

Current mesh bounding sphere.
## getSystemMemoryUsage () const

Returns the current total system memory used by this mesh, in bytes.
### Return value

Current system memory usage in bytes.
---

## static MeshSkinnedPtr create ( )

Creates an empty skinned mesh.
## static MeshSkinnedPtr create ( const char * path )

Creates a skinned mesh and loads data from the specified file.
### Arguments

- *const char ** **path** - Path to the mesh file.

## void initSourceSkeleton ( const Ptr <ConstSkeleton> & skeleton )

Initializes the source joint hierarchy from the specified skeleton instance.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<ConstSkeleton> &* **skeleton** - Skeleton instance to initialize source joints from.

## void initSourceSkeleton ( const char * path )

Initializes the source joint hierarchy from a skeleton loaded from the specified file path.
### Arguments

- *const char ** **path** - File path to the skeleton.

## void assignFrom ( const Ptr < MeshSkinned > & mesh )

Copies all data from the source mesh: geometry, joints, and surfaces.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[MeshSkinned](../../../api/library/rendering/class.meshskinned_cpp.md)> &* **mesh** - Source mesh instance.

## int info ( const char * path ) const

Reads metadata from the specified mesh file without loading the full geometry data.
### Arguments

- *const char ** **path** - Path to the mesh file.

### Return value

1 if the file metadata was read successfully; otherwise, 0.
## int load ( const char * path )

Loads the full mesh data from the specified file.
### Arguments

- *const char ** **path** - Path to the mesh file.

### Return value

1 if the mesh was loaded successfully; otherwise, 0.
## int save ( const char * path ) const

Saves the mesh data to the specified file. Creates the file and any required subdirectories if they don't exist.
### Arguments

- *const char ** **path** - Path to the output file.

### Return value

1 if the mesh was saved successfully; otherwise, 0.
## void clear ( )

Clears all mesh data: geometry, joints, and surfaces.
## bool flipYZ ( int surface = -1 )

Flips the Y and Z axes for the specified surface (or all surfaces).
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if the operation was successful; otherwise, false.
## bool flipTangent ( int surface = -1 )

Flips the tangent direction for the specified surface (or all surfaces).
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if the operation was successful; otherwise, false.
## bool createBounds ( int surface = -1 )

Recalculates bounding boxes and bounding spheres for the specified surface (or all surfaces).
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if bounds were created successfully; otherwise, false.
## bool removeIndices ( int surface = -1 )

Removes all indices from the specified surface (or all surfaces).
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if indices were removed successfully; otherwise, false.
## bool createIndices ( int surface = -1 )

Creates triangle and coordinate indices for the specified surface (or all surfaces).
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if indices were created successfully; otherwise, false.
## bool optimizeIndices ( int flags , int surface = -1 )

Optimizes the index buffer for the specified surface (or all surfaces) using the given flags.
### Arguments

- *int* **flags** - Optimization flags.
- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if optimization was successful; otherwise, false.
## bool createNormals ( int surface = -1 , int target = -1 )

Creates normals for the specified surface and morph target by averaging face normals.
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.
- *int* **target** - Morph target index. Use -1 for all targets.

### Return value

true if normals were created successfully; otherwise, false.
## bool createNormals ( float angle , int surface = -1 , int target = -1 )

Creates normals with the specified angle threshold for smooth/hard edge detection.
### Arguments

- *float* **angle** - Angle threshold in degrees for smooth/hard edge detection.
- *int* **surface** - Surface index. Use -1 for all surfaces.
- *int* **target** - Morph target index. Use -1 for all targets.

### Return value

true if normals were created successfully; otherwise, false.
## bool createTangents ( int surface = -1 , int target = -1 )

Creates tangent basis vectors for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.
- *int* **target** - Morph target index. Use -1 for all targets.

### Return value

true if tangents were created successfully; otherwise, false.
## bool createTangents ( float angle , const Vector <int> & surfaces )

Creates tangent basis vectors for the specified surfaces with the given angle threshold.
### Arguments

- *float* **angle** - Angle threshold in degrees.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **surfaces** - List of surface indices to process.

### Return value

true if tangents were created successfully; otherwise, false.
## int findSrcJoint ( const char * name ) const

Searches for a source joint with the specified name and returns its index.
### Arguments

- *const char ** **name** - Joint name to search for.

### Return value

Source joint index, or -1 if not found.
## const char * getSrcJointName ( int bone ) const

Returns the name of the source joint at the specified index.
### Arguments

- *int* **bone** - Source joint index.

### Return value

Joint name.
## int getSrcJointParent ( int bone ) const

Returns the parent joint index for the specified source joint.
### Arguments

- *int* **bone** - Source joint index.

### Return value

Parent joint index, or -1 if the joint has no parent.
## Math:: mat4 getSrcJointObjectITransform ( int joint ) const

Returns the inverse bind pose transformation matrix in object space for the specified source joint. Used for skinning calculations.
### Arguments

- *int* **joint** - Source joint index.

### Return value

Inverse bind pose matrix in object space.
## Math::Transform getSrcJointBindLocalTransform ( int joint ) const

Returns the bind pose transform in local space (relative to the parent joint) for the specified source joint.
### Arguments

- *int* **joint** - Source joint index.

### Return value

Bind pose transform in local space.
## void setSrcJointRestLocalTransform ( int index , Math::Transform & transform )

Sets the rest pose transform in local space for the specified source joint.
### Arguments

- *int* **index** - Source joint index.
- *Math::Transform &* **transform** - Rest pose transform in local space.

## Math::Transform getSrcJointRestLocalTransform ( int index ) const

Returns the rest pose transform in local space for the specified source joint.
### Arguments

- *int* **index** - Source joint index.

### Return value

Rest pose transform in local space.
## int findSurface ( const char * name ) const

Searches for a surface with the specified name and returns its index.
### Arguments

- *const char ** **name** - Surface name to search for.

### Return value

Surface index, or -1 if not found.
## void sortSurfaces ( )

Sorts surfaces alphabetically by name.
## void clearSurface ( int surface = -1 , int target = -1 )

Clears geometry data for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.
- *int* **target** - Morph target index. Use -1 for all targets.

## int addSurface ( const char * name = 0 )

Adds a new empty surface with the specified name.
### Arguments

- *const char ** **name** - Surface name. Can be empty.

### Return value

Index of the newly added surface.
## void setSurfaceName ( int surface , const char * name )

Sets the name of the specified surface.
### Arguments

- *int* **surface** - Surface index.
- *const char ** **name** - Surface name.

## const char * getSurfaceName ( int surface ) const

Returns the name of the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Surface name.
## void setNumSurfaceTargets ( int surface , int num )

Sets the number of morph targets for the specified surface.
### Arguments

- *int* **surface** - Surface index.
- *int* **num** - Number of morph targets.

## int getNumSurfaceTargets ( int surface ) const

Returns the number of morph targets for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of morph targets.
## void setSurfaceTargetName ( int surface , int target , const char * name )

Sets the name of the specified morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.
- *const char ** **name** - Target name.

## const char * getSurfaceTargetName ( int surface , int target ) const

Returns the name of the specified morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Target name.
## int findSurfaceTarget ( int surface , const char * name ) const

Searches for a morph target by name within the specified surface.
### Arguments

- *int* **surface** - Surface index.
- *const char ** **name** - Target name to search for.

### Return value

Morph target index, or -1 if not found.
## int setSurfaceTransform ( const Math:: mat4 & transform , int surface = -1 , int target = -1 )

Applies a transformation matrix to the vertices, normals, and tangents of the specified surface and morph target.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix to apply.
- *int* **surface** - Surface index. Use -1 for all surfaces.
- *int* **target** - Morph target index. Use -1 for all targets.

### Return value

1 if the transform was applied successfully; otherwise, 0.
## int addMeshSurface ( const char * v , const Ptr <ConstMeshSkinned> & mesh , int surface , int target = -1 )

Adds a surface from the specified source mesh as a new surface with the given name.
### Arguments

- *const char ** **v** - Name for the new surface.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<ConstMeshSkinned> &* **mesh** - Source mesh to copy the surface from.
- *int* **surface** - Surface index in the source mesh.
- *int* **target** - Morph target index in the source surface. Use -1 for all targets.

### Return value

Index of the newly added surface.
## int addMeshSurface ( int v , const Ptr <ConstMeshSkinned> & mesh , int surface , int target = -1 )

Appends geometry from the specified source mesh surface to an existing surface in this mesh.
### Arguments

- *int* **v** - Destination surface index to append geometry to.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<ConstMeshSkinned> &* **mesh** - Source mesh to copy the surface from.
- *int* **surface** - Surface index in the source mesh.
- *int* **target** - Morph target index in the source surface. Use -1 for all targets.

### Return value

Destination surface index.
## int addEmptySurface ( const char * name , int num_vertex , int num_indices )

Adds a new surface with pre-allocated vertex and index buffers.
### Arguments

- *const char ** **name** - Surface name.
- *int* **num_vertex** - Number of vertices to allocate.
- *int* **num_indices** - Number of indices to allocate.

### Return value

Index of the newly added surface.
## int addSurfaceTarget ( int surface , const char * name = 0 )

Adds a new morph target to the specified surface.
### Arguments

- *int* **surface** - Surface index.
- *const char ** **name** - Target name. Can be empty.

### Return value

Index of the newly added morph target.
## int addBoxSurface ( const char * name , const Math:: vec3 & size )

Adds a box primitive surface with the specified dimensions.
### Arguments

- *const char ** **name** - Surface name.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Box dimensions (width, height, depth).

### Return value

Index of the newly added surface.
## int addPlaneSurface ( const char * name , float width , float height , float step )

Adds a plane primitive surface with the specified dimensions and tessellation step.
### Arguments

- *const char ** **name** - Surface name.
- *float* **width** - Plane width.
- *float* **height** - Plane height.
- *float* **step** - Tessellation step.

### Return value

Index of the newly added surface.
## int addSphereSurface ( const char * name , float radius , int stacks , int slices )

Adds a sphere primitive surface with the specified radius and subdivisions.
### Arguments

- *const char ** **name** - Surface name.
- *float* **radius** - Sphere radius.
- *int* **stacks** - Number of horizontal subdivisions.
- *int* **slices** - Number of vertical subdivisions.

### Return value

Index of the newly added surface.
## int addCapsuleSurface ( const char * name , float radius , float height , int stacks , int slices )

Adds a capsule primitive surface with the specified dimensions and subdivisions.
### Arguments

- *const char ** **name** - Surface name.
- *float* **radius** - Capsule radius.
- *float* **height** - Capsule height (cylinder part).
- *int* **stacks** - Number of horizontal subdivisions.
- *int* **slices** - Number of vertical subdivisions.

### Return value

Index of the newly added surface.
## int addCylinderSurface ( const char * name , float radius , float height , int stacks , int slices )

Adds a cylinder primitive surface with the specified dimensions and subdivisions.
### Arguments

- *const char ** **name** - Surface name.
- *float* **radius** - Cylinder radius.
- *float* **height** - Cylinder height.
- *int* **stacks** - Number of horizontal subdivisions.
- *int* **slices** - Number of vertical subdivisions.

### Return value

Index of the newly added surface.
## int addPrismSurface ( const char * name , float size_0 , float size_1 , float height , int sides )

Adds a prism primitive surface with the specified dimensions.
### Arguments

- *const char ** **name** - Surface name.
- *float* **size_0** - Bottom face size.
- *float* **size_1** - Top face size.
- *float* **height** - Prism height.
- *int* **sides** - Number of sides.

### Return value

Index of the newly added surface.
## int addIcosahedronSurface ( const char * name , float radius )

Adds an icosahedron primitive surface with the specified radius.
### Arguments

- *const char ** **name** - Surface name.
- *float* **radius** - Icosahedron radius.

### Return value

Index of the newly added surface.
## int addDodecahedronSurface ( const char * name , float radius )

Adds a dodecahedron primitive surface with the specified radius.
### Arguments

- *const char ** **name** - Surface name.
- *float* **radius** - Dodecahedron radius.

### Return value

Index of the newly added surface.
## int getNumCVertex ( int surface = 0 ) const

Returns the number of unique coordinate vertices (positions) for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of unique coordinate vertices.
## int getNumTVertex ( int surface = 0 ) const

Returns the number of unique triangle vertices (attribute combinations) for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of unique triangle vertices.
## int remapCVertex ( int surface = 0 )

Remaps coordinate vertex indices for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

1 if remapping was successful; otherwise, 0.
## void setNumWeights ( int size , int surface = 0 )

Sets the number of skinning weight entries for the specified surface.
### Arguments

- *int* **size** - Number of weight entries.
- *int* **surface** - Surface index.

## int getNumWeights ( int surface = 0 ) const

Returns the number of skinning weight entries for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of weight entries.
## void setWeightCount ( int num , int count , int surface = 0 )

Sets the number of joint influences for the specified weight entry.
### Arguments

- *int* **num** - Weight entry index.
- *int* **count** - Number of joint influences (1 to 4).
- *int* **surface** - Surface index.

## int getWeightCount ( int num , int surface = 0 ) const

Returns the number of joint influences for the specified weight entry.
### Arguments

- *int* **num** - Weight entry index.
- *int* **surface** - Surface index.

### Return value

Number of joint influences.
## void setWeightJoints ( int num , const Math:: ivec4 & joints , int surface = 0 )

Sets the joint indices for the specified weight entry. Each component of the ivec4 is a source joint index.
### Arguments

- *int* **num** - Weight entry index.
- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **joints** - Four joint indices packed into an ivec4.
- *int* **surface** - Surface index.

## Math:: ivec4 getWeightJoints ( int num , int surface = 0 ) const

Returns the joint indices for the specified weight entry.
### Arguments

- *int* **num** - Weight entry index.
- *int* **surface** - Surface index.

### Return value

Four joint indices packed into an ivec4.
## void setWeightWeights ( int num , const Math:: vec4 & weights , int surface = 0 )

Sets the joint weights for the specified weight entry.
### Arguments

- *int* **num** - Weight entry index.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **weights** - Four joint weights packed into a vec4. Components should sum to 1.0.
- *int* **surface** - Surface index.

## Math:: vec4 getWeightWeights ( int num , int surface = 0 ) const

Returns the joint weights for the specified weight entry.
### Arguments

- *int* **num** - Weight entry index.
- *int* **surface** - Surface index.

### Return value

Four joint weights packed into a vec4.
## void setNumVertex ( int size , int surface = 0 , int target = 0 )

Sets the number of vertices for the specified surface and morph target.
### Arguments

- *int* **size** - Number of vertices.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## int getNumVertex ( int surface , int target = 0 ) const

Returns the number of vertices for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Number of vertices.
## void addVertex ( const Vector < Math:: vec3 > & vertices , int surface = 0 , int target = 0 )

Adds multiple vertices to the specified surface and morph target.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[vec3](../../../api/library/math/class.vec3_cpp.md)> &* **vertices** - Array of vertex positions to add.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## void addVertex ( const Math:: vec3 & vertex , int surface = 0 , int target = 0 )

Adds a single vertex to the specified surface and morph target.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **vertex** - Vertex position.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## void setVertex ( int num , const Math:: vec3 & vertex , int surface = 0 , int target = 0 )

Sets the position of the vertex at the specified index.
### Arguments

- *int* **num** - Vertex index.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **vertex** - Vertex position.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## Math:: vec3 getVertex ( int num , int surface = 0 , int target = 0 ) const

Returns the position of the vertex at the specified index.
### Arguments

- *int* **num** - Vertex index.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Vertex position.
## void setNumTexCoords0 ( int size , int surface = 0 )

Sets the number of first UV channel texture coordinates for the specified surface.
### Arguments

- *int* **size** - Number of texture coordinates.
- *int* **surface** - Surface index.

## int getNumTexCoords0 ( int surface = 0 ) const

Returns the number of first UV channel texture coordinates for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of texture coordinates.
## void addTexCoords0 ( const Vector < Math:: vec2 > & texcoords , int surface = 0 )

Adds multiple first UV channel texture coordinates to the specified surface.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[vec2](../../../api/library/math/class.vec2_cpp.md)> &* **texcoords** - Array of texture coordinates to add.
- *int* **surface** - Surface index.

## void addTexCoord0 ( const Math:: vec2 & texcoord , int surface = 0 )

Adds a single first UV channel texture coordinate to the specified surface.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **texcoord** - Texture coordinate.
- *int* **surface** - Surface index.

## void setTexCoord0 ( int num , const Math:: vec2 & texcoord , int surface = 0 )

Sets the first UV channel texture coordinate at the specified index.
### Arguments

- *int* **num** - Texture coordinate index.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **texcoord** - Texture coordinate.
- *int* **surface** - Surface index.

## Math:: vec2 getTexCoord0 ( int num , int surface = 0 ) const

Returns the first UV channel texture coordinate at the specified index.
### Arguments

- *int* **num** - Texture coordinate index.
- *int* **surface** - Surface index.

### Return value

Texture coordinate.
## void setNumTexCoords1 ( int size , int surface = 0 )

Sets the number of second UV channel texture coordinates for the specified surface.
### Arguments

- *int* **size** - Number of texture coordinates.
- *int* **surface** - Surface index.

## int getNumTexCoords1 ( int surface = 0 ) const

Returns the number of second UV channel texture coordinates for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of texture coordinates.
## void addTexCoords1 ( const Vector < Math:: vec2 > & texcoords , int surface = 0 )

Adds multiple second UV channel texture coordinates to the specified surface.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[vec2](../../../api/library/math/class.vec2_cpp.md)> &* **texcoords** - Array of texture coordinates to add.
- *int* **surface** - Surface index.

## void addTexCoord1 ( const Math:: vec2 & texcoord , int surface = 0 )

Adds a single second UV channel texture coordinate to the specified surface.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **texcoord** - Texture coordinate.
- *int* **surface** - Surface index.

## void setTexCoord1 ( int num , const Math:: vec2 & texcoord , int surface = 0 )

Sets the second UV channel texture coordinate at the specified index.
### Arguments

- *int* **num** - Texture coordinate index.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **texcoord** - Texture coordinate.
- *int* **surface** - Surface index.

## Math:: vec2 getTexCoord1 ( int num , int surface = 0 ) const

Returns the second UV channel texture coordinate at the specified index.
### Arguments

- *int* **num** - Texture coordinate index.
- *int* **surface** - Surface index.

### Return value

Texture coordinate.
## void setNumNormals ( int size , int surface = 0 , int target = 0 )

Sets the number of normals for the specified surface and morph target.
### Arguments

- *int* **size** - Number of normals.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## int getNumNormals ( int surface = 0 , int target = 0 ) const

Returns the number of normals for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Number of normals.
## void addNormals ( const Vector < Math:: vec3 > & normals , int surface = 0 , int target = 0 )

Adds multiple normals to the specified surface and morph target.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[vec3](../../../api/library/math/class.vec3_cpp.md)> &* **normals** - Array of normals to add.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## void addNormal ( const Math:: vec3 & normal , int surface = 0 , int target = 0 )

Adds a single normal to the specified surface and morph target.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **normal** - Normal vector.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## void setNormal ( int num , const Math:: vec3 & normal , int surface = 0 , int target = 0 )

Sets the normal at the specified index.
### Arguments

- *int* **num** - Normal index.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **normal** - Normal vector.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## Math:: vec3 getNormal ( int num , int surface = 0 , int target = 0 ) const

Returns the normal at the specified index.
### Arguments

- *int* **num** - Normal index.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Normal vector.
## void setNumTangents ( int size , int surface = 0 , int target = 0 )

Sets the number of tangents for the specified surface and morph target.
### Arguments

- *int* **size** - Number of tangents.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## int getNumTangents ( int surface , int target = 0 ) const

Returns the number of tangents for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Number of tangents.
## void addTangents ( const Vector < Math:: quat > & tangents , int surface = 0 , int target = 0 )

Adds multiple tangents to the specified surface and morph target.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[quat](../../../api/library/math/class.quat_cpp.md)> &* **tangents** - Array of tangent quaternions to add.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## void addTangent ( const Math:: quat & tangent , int surface = 0 , int target = 0 )

Adds a single tangent to the specified surface and morph target.
### Arguments

- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **tangent** - Tangent quaternion encoding the tangent basis.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## void setTangent ( int num , const Math:: quat & tangent , int surface = 0 , int target = 0 )

Sets the tangent at the specified index.
### Arguments

- *int* **num** - Tangent index.
- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **tangent** - Tangent quaternion.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## Math:: quat getTangent ( int num , int surface = 0 , int target = 0 ) const

Returns the tangent at the specified index.
### Arguments

- *int* **num** - Tangent index.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Tangent quaternion.
## void setNumColors ( int size , int surface = 0 )

Sets the number of vertex colors for the specified surface.
### Arguments

- *int* **size** - Number of vertex colors.
- *int* **surface** - Surface index.

## int getNumColors ( int surface = 0 ) const

Returns the number of vertex colors for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of vertex colors.
## void addColors ( const Vector < Math:: vec4 > & colors , int surface = 0 )

Adds multiple vertex colors to the specified surface.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[vec4](../../../api/library/math/class.vec4_cpp.md)> &* **colors** - Array of vertex colors to add.
- *int* **surface** - Surface index.

## void addColor ( const Math:: vec4 & color , int surface = 0 )

Adds a single vertex color to the specified surface.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Vertex color (RGBA, 0.0 to 1.0 range).
- *int* **surface** - Surface index.

## void setColor ( int num , const Math:: vec4 & color , int surface = 0 )

Sets the vertex color at the specified index.
### Arguments

- *int* **num** - Color index.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Vertex color (RGBA, 0.0 to 1.0 range).
- *int* **surface** - Surface index.

## Math:: vec4 getColor ( int num , int surface = 0 ) const

Returns the vertex color at the specified index.
### Arguments

- *int* **num** - Color index.
- *int* **surface** - Surface index.

### Return value

Vertex color (RGBA, 0.0 to 1.0 range).
## void setNumCIndices ( int size , int surface = 0 )

Sets the number of coordinate indices for the specified surface.
### Arguments

- *int* **size** - Number of coordinate indices.
- *int* **surface** - Surface index.

## int getNumCIndices ( int surface = 0 ) const

Returns the number of coordinate indices for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of coordinate indices.
## void addCIndices ( const Vector <int> & indices , int surface = 0 )

Adds multiple coordinate indices to the specified surface.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **indices** - Array of coordinate indices to add.
- *int* **surface** - Surface index.

## void addCIndex ( int index , int surface = 0 )

Adds a single coordinate index to the specified surface.
### Arguments

- *int* **index** - Coordinate index to add.
- *int* **surface** - Surface index.

## void setCIndex ( int num , int index , int surface = 0 )

Sets the coordinate index at the specified position.
### Arguments

- *int* **num** - Position in the coordinate index buffer.
- *int* **index** - Coordinate index value.
- *int* **surface** - Surface index.

## int getCIndex ( int num , int surface = 0 ) const

Returns the coordinate index at the specified position.
### Arguments

- *int* **num** - Position in the coordinate index buffer.
- *int* **surface** - Surface index.

### Return value

Coordinate index value.
## void setNumTIndices ( int size , int surface = 0 )

Sets the number of triangle indices for the specified surface.
### Arguments

- *int* **size** - Number of triangle indices.
- *int* **surface** - Surface index.

## int getNumTIndices ( int surface = 0 ) const

Returns the number of triangle indices for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of triangle indices.
## void addTIndices ( const Vector <int> & indices , int surface = 0 )

Adds multiple triangle indices to the specified surface.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **indices** - Array of triangle indices to add.
- *int* **surface** - Surface index.

## void addTIndex ( int index , int surface = 0 )

Adds a single triangle index to the specified surface.
### Arguments

- *int* **index** - Triangle index to add.
- *int* **surface** - Surface index.

## void setTIndex ( int num , int index , int surface = 0 )

Sets the triangle index at the specified position.
### Arguments

- *int* **num** - Position in the triangle index buffer.
- *int* **index** - Triangle index value.
- *int* **surface** - Surface index.

## int getTIndex ( int num , int surface = 0 ) const

Returns the triangle index at the specified position.
### Arguments

- *int* **num** - Position in the triangle index buffer.
- *int* **surface** - Surface index.

### Return value

Triangle index value.
## void setNumIndices ( int size , int surface = 0 )

Sets the number of rendering indices for the specified surface.
### Arguments

- *int* **size** - Number of rendering indices.
- *int* **surface** - Surface index.

## int getNumIndices ( int surface = 0 ) const

Returns the number of rendering indices for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of rendering indices.
## void addIndices ( const Vector <int> & indices , int surface = 0 )

Adds multiple rendering indices to the specified surface.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **indices** - Array of rendering indices to add.
- *int* **surface** - Surface index.

## void addIndex ( int index , int surface = 0 )

Adds a single rendering index to the specified surface.
### Arguments

- *int* **index** - Rendering index to add.
- *int* **surface** - Surface index.

## void setIndex ( int num , int index , int surface = 0 )

Sets the rendering index at the specified position.
### Arguments

- *int* **num** - Position in the rendering index buffer.
- *int* **index** - Rendering index value.
- *int* **surface** - Surface index.

## int getIndex ( int num , int surface = 0 ) const

Returns the rendering index at the specified position.
### Arguments

- *int* **num** - Position in the rendering index buffer.
- *int* **surface** - Surface index.

### Return value

Rendering index value.
## Vector < Math:: vec3 > & getVertices ( int surface = 0 , int target = 0 )

Returns direct access to the vertex positions array for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Reference to the vertex positions array.
## Vector < Math:: vec3 > & getNormals ( int surface = 0 , int target = 0 )

Returns direct access to the normals array for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Reference to the normals array.
## Vector < Math:: quat > & getTangents ( int surface = 0 , int target = 0 )

Returns direct access to the tangent quaternions array for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Reference to the tangent quaternions array.
## Vector < Math:: vec2 > & getTexCoords0 ( int surface = 0 )

Returns direct access to the first UV channel texture coordinates array for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Reference to the first UV channel array.
## Vector < Math:: vec2 > & getTexCoords1 ( int surface = 0 )

Returns direct access to the second UV channel texture coordinates array for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Reference to the second UV channel array.
## Vector < Math:: bvec4 > & getColors ( int surface = 0 )

Returns direct access to the vertex colors array for the specified surface. Colors are stored as 8-bit per channel (bvec4).
### Arguments

- *int* **surface** - Surface index.

### Return value

Reference to the vertex colors array (8-bit per channel).
## Vector <int> & getCIndices ( int surface = 0 )

Returns direct access to the coordinate indices array for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Reference to the coordinate indices array.
## Vector <int> & getTIndices ( int surface = 0 )

Returns direct access to the triangle indices array for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Reference to the triangle indices array.
## const Vector < Math:: vec3 > & getVertices ( int surface = 0 , int target = 0 ) const

Returns read-only access to the vertex positions array for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Const reference to the vertex positions array.
## const Vector < Math:: vec3 > & getNormals ( int surface = 0 , int target = 0 ) const

Returns read-only access to the normals array for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Const reference to the normals array.
## const Vector < Math:: quat > & getTangents ( int surface = 0 , int target = 0 ) const

Returns read-only access to the tangent quaternions array for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Const reference to the tangent quaternions array.
## const Vector < Math:: vec2 > & getTexCoords0 ( int surface = 0 ) const

Returns read-only access to the first UV channel texture coordinates array for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Const reference to the first UV channel array.
## const Vector < Math:: vec2 > & getTexCoords1 ( int surface = 0 ) const

Returns read-only access to the second UV channel texture coordinates array for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Const reference to the second UV channel array.
## const Vector < Math:: bvec4 > & getColors ( int surface = 0 ) const

Returns read-only access to the vertex colors array for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Const reference to the vertex colors array (8-bit per channel).
## const Vector <int> & getCIndices ( int surface = 0 ) const

Returns read-only access to the coordinate indices array for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Const reference to the coordinate indices array.
## const Vector <int> & getTIndices ( int surface = 0 ) const

Returns read-only access to the triangle indices array for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Const reference to the triangle indices array.
## Math:: BoundBox getBoundBox ( int surface ) const

Returns the axis-aligned bounding box for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Bounding box for the specified surface.
## Math:: BoundSphere getBoundSphere ( int surface ) const

Returns the bounding sphere for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Bounding sphere for the specified surface.
## void setBoundBox ( const Math:: BoundBox & bb , int surface )

Sets the bounding box for the specified surface.
### Arguments

- *const  Math::[BoundBox](../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box to set.
- *int* **surface** - Surface index.

## void setBoundBox ( const Math:: BoundBox & bb )

Sets the bounding box for the entire mesh.
### Arguments

- *const  Math::[BoundBox](../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box to set.

## void setBoundSphere ( const Math:: BoundSphere & bs , int surface )

Sets the bounding sphere for the specified surface.
### Arguments

- *const  Math::[BoundSphere](../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere to set.
- *int* **surface** - Surface index.

## void setBoundSphere ( const Math:: BoundSphere & bs )

Sets the bounding sphere for the entire mesh.
### Arguments

- *const  Math::[BoundSphere](../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere to set.
