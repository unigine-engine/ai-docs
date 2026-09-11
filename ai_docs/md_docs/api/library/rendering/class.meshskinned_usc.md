# MeshSkinned Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


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

## static MeshSkinned ( )

Creates an empty skinned mesh.
## static MeshSkinned ( string path )

Creates a skinned mesh and loads data from the specified file.
### Arguments

- *string* **path** - Path to the mesh file.

## void assignFrom ( MeshSkinned mesh )

Copies all data from the source mesh: geometry, joints, and surfaces.
### Arguments

- *[MeshSkinned](../../../api/library/rendering/class.meshskinned_usc.md)* **mesh** - Source mesh instance.

## int info ( string path )

Reads metadata from the specified mesh file without loading the full geometry data.
### Arguments

- *string* **path** - Path to the mesh file.

### Return value

1 if the file metadata was read successfully; otherwise, 0.
## int load ( string path )

Loads the full mesh data from the specified file.
### Arguments

- *string* **path** - Path to the mesh file.

### Return value

1 if the mesh was loaded successfully; otherwise, 0.
## int save ( string path )

Saves the mesh data to the specified file. Creates the file and any required subdirectories if they don't exist.
### Arguments

- *string* **path** - Path to the output file.

### Return value

1 if the mesh was saved successfully; otherwise, 0.
## void clear ( )

Clears all mesh data: geometry, joints, and surfaces.
## int flipYZ ( int surface = -1 )

Flips the Y and Z axes for the specified surface (or all surfaces).
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if the operation was successful; otherwise, false.
## int flipTangent ( int surface = -1 )

Flips the tangent direction for the specified surface (or all surfaces).
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if the operation was successful; otherwise, false.
## int createBounds ( int surface = -1 )

Recalculates bounding boxes and bounding spheres for the specified surface (or all surfaces).
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if bounds were created successfully; otherwise, false.
## int removeIndices ( int surface = -1 )

Removes all indices from the specified surface (or all surfaces).
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if indices were removed successfully; otherwise, false.
## int createIndices ( int surface = -1 )

Creates triangle and coordinate indices for the specified surface (or all surfaces).
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if indices were created successfully; otherwise, false.
## int optimizeIndices ( int flags , int surface = -1 )

Optimizes the index buffer for the specified surface (or all surfaces) using the given flags.
### Arguments

- *int* **flags** - Optimization flags.
- *int* **surface** - Surface index. Use -1 for all surfaces.

### Return value

true if optimization was successful; otherwise, false.
## int createTangents ( int surface = -1 , int target = -1 )

Creates tangent basis vectors for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.
- *int* **target** - Morph target index. Use -1 for all targets.

### Return value

true if tangents were created successfully; otherwise, false.
## int findSrcJoint ( string name )

Searches for a source joint with the specified name and returns its index.
### Arguments

- *string* **name** - Joint name to search for.

### Return value

Source joint index, or -1 if not found.
## string getSrcJointName ( int bone )

Returns the name of the source joint at the specified index.
### Arguments

- *int* **bone** - Source joint index.

### Return value

Joint name.
## int getSrcJointParent ( int bone )

Returns the parent joint index for the specified source joint.
### Arguments

- *int* **bone** - Source joint index.

### Return value

Parent joint index, or -1 if the joint has no parent.
## mat4 getSrcJointObjectITransform ( int joint )

Returns the inverse bind pose transformation matrix in object space for the specified source joint. Used for skinning calculations.
### Arguments

- *int* **joint** - Source joint index.

### Return value

Inverse bind pose matrix in object space.
## FloatTransform getSrcJointBindLocalTransform ( int joint )

Returns the bind pose transform in local space (relative to the parent joint) for the specified source joint.
### Arguments

- *int* **joint** - Source joint index.

### Return value

Bind pose transform in local space.
## void setSrcJointRestLocalTransform ( int index , FloatTransform transform )

Sets the rest pose transform in local space for the specified source joint.
### Arguments

- *int* **index** - Source joint index.
- *FloatTransform* **transform** - Rest pose transform in local space.

## FloatTransform getSrcJointRestLocalTransform ( int index )

Returns the rest pose transform in local space for the specified source joint.
### Arguments

- *int* **index** - Source joint index.

### Return value

Rest pose transform in local space.
## int findSurface ( string name )

Searches for a surface with the specified name and returns its index.
### Arguments

- *string* **name** - Surface name to search for.

### Return value

Surface index, or -1 if not found.
## void sortSurfaces ( )

Sorts surfaces alphabetically by name.
## void clearSurface ( int surface = -1 , int target = -1 )

Clears geometry data for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index. Use -1 for all surfaces.
- *int* **target** - Morph target index. Use -1 for all targets.

## int addSurface ( string name = 0 )

Adds a new empty surface with the specified name.
### Arguments

- *string* **name** - Surface name. Can be empty.

### Return value

Index of the newly added surface.
## void setSurfaceName ( int surface , string name )

Sets the name of the specified surface.
### Arguments

- *int* **surface** - Surface index.
- *string* **name** - Surface name.

## string getSurfaceName ( int surface )

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

## int getNumSurfaceTargets ( int surface )

Returns the number of morph targets for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of morph targets.
## void setSurfaceTargetName ( int surface , int target , string name )

Sets the name of the specified morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.
- *string* **name** - Target name.

## string getSurfaceTargetName ( int surface , int target )

Returns the name of the specified morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Target name.
## int findSurfaceTarget ( int surface , string name )

Searches for a morph target by name within the specified surface.
### Arguments

- *int* **surface** - Surface index.
- *string* **name** - Target name to search for.

### Return value

Morph target index, or -1 if not found.
## int setSurfaceTransform ( mat4 transform , int surface = -1 , int target = -1 )

Applies a transformation matrix to the vertices, normals, and tangents of the specified surface and morph target.
### Arguments

- *mat4* **transform** - Transformation matrix to apply.
- *int* **surface** - Surface index. Use -1 for all surfaces.
- *int* **target** - Morph target index. Use -1 for all targets.

### Return value

1 if the transform was applied successfully; otherwise, 0.
## int addMeshSurface ( string v , MeshSkinned mesh , int surface , int target = -1 )

Adds a surface from the specified source mesh as a new surface with the given name.
### Arguments

- *string* **v** - Name for the new surface.
- *[MeshSkinned](../../../api/library/rendering/class.meshskinned_usc.md)* **mesh** - Source mesh to copy the surface from.
- *int* **surface** - Surface index in the source mesh.
- *int* **target** - Morph target index in the source surface. Use -1 for all targets.

### Return value

Index of the newly added surface.
## int addEmptySurface ( string name , int num_vertex , int num_indices )

Adds a new surface with pre-allocated vertex and index buffers.
### Arguments

- *string* **name** - Surface name.
- *int* **num_vertex** - Number of vertices to allocate.
- *int* **num_indices** - Number of indices to allocate.

### Return value

Index of the newly added surface.
## int addSurfaceTarget ( int surface , string name = 0 )

Adds a new morph target to the specified surface.
### Arguments

- *int* **surface** - Surface index.
- *string* **name** - Target name. Can be empty.

### Return value

Index of the newly added morph target.
## int addBoxSurface ( string name , vec3 size )

Adds a box primitive surface with the specified dimensions.
### Arguments

- *string* **name** - Surface name.
- *vec3* **size** - Box dimensions (width, height, depth).

### Return value

Index of the newly added surface.
## int addPlaneSurface ( string name , float width , float height , float step )

Adds a plane primitive surface with the specified dimensions and tessellation step.
### Arguments

- *string* **name** - Surface name.
- *float* **width** - Plane width.
- *float* **height** - Plane height.
- *float* **step** - Tessellation step.

### Return value

Index of the newly added surface.
## int addSphereSurface ( string name , float radius , int stacks , int slices )

Adds a sphere primitive surface with the specified radius and subdivisions.
### Arguments

- *string* **name** - Surface name.
- *float* **radius** - Sphere radius.
- *int* **stacks** - Number of horizontal subdivisions.
- *int* **slices** - Number of vertical subdivisions.

### Return value

Index of the newly added surface.
## int addCapsuleSurface ( string name , float radius , float height , int stacks , int slices )

Adds a capsule primitive surface with the specified dimensions and subdivisions.
### Arguments

- *string* **name** - Surface name.
- *float* **radius** - Capsule radius.
- *float* **height** - Capsule height (cylinder part).
- *int* **stacks** - Number of horizontal subdivisions.
- *int* **slices** - Number of vertical subdivisions.

### Return value

Index of the newly added surface.
## int addCylinderSurface ( string name , float radius , float height , int stacks , int slices )

Adds a cylinder primitive surface with the specified dimensions and subdivisions.
### Arguments

- *string* **name** - Surface name.
- *float* **radius** - Cylinder radius.
- *float* **height** - Cylinder height.
- *int* **stacks** - Number of horizontal subdivisions.
- *int* **slices** - Number of vertical subdivisions.

### Return value

Index of the newly added surface.
## int addPrismSurface ( string name , float size_0 , float size_1 , float height , int sides )

Adds a prism primitive surface with the specified dimensions.
### Arguments

- *string* **name** - Surface name.
- *float* **size_0** - Bottom face size.
- *float* **size_1** - Top face size.
- *float* **height** - Prism height.
- *int* **sides** - Number of sides.

### Return value

Index of the newly added surface.
## int addIcosahedronSurface ( string name , float radius )

Adds an icosahedron primitive surface with the specified radius.
### Arguments

- *string* **name** - Surface name.
- *float* **radius** - Icosahedron radius.

### Return value

Index of the newly added surface.
## int addDodecahedronSurface ( string name , float radius )

Adds a dodecahedron primitive surface with the specified radius.
### Arguments

- *string* **name** - Surface name.
- *float* **radius** - Dodecahedron radius.

### Return value

Index of the newly added surface.
## int getNumCVertex ( int surface = 0 )

Returns the number of unique coordinate vertices (positions) for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of unique coordinate vertices.
## int getNumTVertex ( int surface = 0 )

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

## int getNumWeights ( int surface = 0 )

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

## int getWeightCount ( int num , int surface = 0 )

Returns the number of joint influences for the specified weight entry.
### Arguments

- *int* **num** - Weight entry index.
- *int* **surface** - Surface index.

### Return value

Number of joint influences.
## void setWeightJoints ( int num , ivec4 joints , int surface = 0 )

Sets the joint indices for the specified weight entry. Each component of the ivec4 is a source joint index.
### Arguments

- *int* **num** - Weight entry index.
- *ivec4* **joints** - Four joint indices packed into an ivec4.
- *int* **surface** - Surface index.

## ivec4 getWeightJoints ( int num , int surface = 0 )

Returns the joint indices for the specified weight entry.
### Arguments

- *int* **num** - Weight entry index.
- *int* **surface** - Surface index.

### Return value

Four joint indices packed into an ivec4.
## void setWeightWeights ( int num , vec4 weights , int surface = 0 )

Sets the joint weights for the specified weight entry.
### Arguments

- *int* **num** - Weight entry index.
- *vec4* **weights** - Four joint weights packed into a vec4. Components should sum to 1.0.
- *int* **surface** - Surface index.

## vec4 getWeightWeights ( int num , int surface = 0 )

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

## int getNumVertex ( int surface , int target = 0 )

Returns the number of vertices for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Number of vertices.
## void addVertex ( vec3 vertex , int surface = 0 , int target = 0 )

Adds a single vertex to the specified surface and morph target.
### Arguments

- *vec3* **vertex** - Vertex position.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## void setVertex ( int num , vec3 vertex , int surface = 0 , int target = 0 )

Sets the position of the vertex at the specified index.
### Arguments

- *int* **num** - Vertex index.
- *vec3* **vertex** - Vertex position.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## vec3 getVertex ( int num , int surface = 0 , int target = 0 )

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

## int getNumTexCoords0 ( int surface = 0 )

Returns the number of first UV channel texture coordinates for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of texture coordinates.
## void addTexCoord0 ( vec2 texcoord , int surface = 0 )

Adds a single first UV channel texture coordinate to the specified surface.
### Arguments

- *vec2* **texcoord** - Texture coordinate.
- *int* **surface** - Surface index.

## void setTexCoord0 ( int num , vec2 texcoord , int surface = 0 )

Sets the first UV channel texture coordinate at the specified index.
### Arguments

- *int* **num** - Texture coordinate index.
- *vec2* **texcoord** - Texture coordinate.
- *int* **surface** - Surface index.

## vec2 getTexCoord0 ( int num , int surface = 0 )

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

## int getNumTexCoords1 ( int surface = 0 )

Returns the number of second UV channel texture coordinates for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of texture coordinates.
## void addTexCoord1 ( vec2 texcoord , int surface = 0 )

Adds a single second UV channel texture coordinate to the specified surface.
### Arguments

- *vec2* **texcoord** - Texture coordinate.
- *int* **surface** - Surface index.

## void setTexCoord1 ( int num , vec2 texcoord , int surface = 0 )

Sets the second UV channel texture coordinate at the specified index.
### Arguments

- *int* **num** - Texture coordinate index.
- *vec2* **texcoord** - Texture coordinate.
- *int* **surface** - Surface index.

## vec2 getTexCoord1 ( int num , int surface = 0 )

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

## int getNumNormals ( int surface = 0 , int target = 0 )

Returns the number of normals for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Number of normals.
## void addNormal ( vec3 normal , int surface = 0 , int target = 0 )

Adds a single normal to the specified surface and morph target.
### Arguments

- *vec3* **normal** - Normal vector.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## void setNormal ( int num , vec3 normal , int surface = 0 , int target = 0 )

Sets the normal at the specified index.
### Arguments

- *int* **num** - Normal index.
- *vec3* **normal** - Normal vector.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## vec3 getNormal ( int num , int surface = 0 , int target = 0 )

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

## int getNumTangents ( int surface , int target = 0 )

Returns the number of tangents for the specified surface and morph target.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Number of tangents.
## void addTangent ( quat tangent , int surface = 0 , int target = 0 )

Adds a single tangent to the specified surface and morph target.
### Arguments

- *quat* **tangent** - Tangent quaternion encoding the tangent basis.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## void setTangent ( int num , quat tangent , int surface = 0 , int target = 0 )

Sets the tangent at the specified index.
### Arguments

- *int* **num** - Tangent index.
- *quat* **tangent** - Tangent quaternion.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

## quat getTangent ( int num , int surface = 0 , int target = 0 )

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

## int getNumColors ( int surface = 0 )

Returns the number of vertex colors for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of vertex colors.
## void addColor ( vec4 color , int surface = 0 )

Adds a single vertex color to the specified surface.
### Arguments

- *vec4* **color** - Vertex color (RGBA, 0.0 to 1.0 range).
- *int* **surface** - Surface index.

## void setColor ( int num , vec4 color , int surface = 0 )

Sets the vertex color at the specified index.
### Arguments

- *int* **num** - Color index.
- *vec4* **color** - Vertex color (RGBA, 0.0 to 1.0 range).
- *int* **surface** - Surface index.

## vec4 getColor ( int num , int surface = 0 )

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

## int getNumCIndices ( int surface = 0 )

Returns the number of coordinate indices for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of coordinate indices.
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

## int getCIndex ( int num , int surface = 0 )

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

## int getNumTIndices ( int surface = 0 )

Returns the number of triangle indices for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of triangle indices.
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

## int getTIndex ( int num , int surface = 0 )

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

## int getNumIndices ( int surface = 0 )

Returns the number of rendering indices for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of rendering indices.
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

## int getIndex ( int num , int surface = 0 )

Returns the rendering index at the specified position.
### Arguments

- *int* **num** - Position in the rendering index buffer.
- *int* **surface** - Surface index.

### Return value

Rendering index value.
## BoundBox getBoundBox ( int surface )

Returns the axis-aligned bounding box for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Bounding box for the specified surface.
## BoundSphere getBoundSphere ( int surface )

Returns the bounding sphere for the specified surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Bounding sphere for the specified surface.
## void setBoundBox ( BoundBox bb , int surface )

Sets the bounding box for the specified surface.
### Arguments

- *BoundBox* **bb** - Bounding box to set.
- *int* **surface** - Surface index.

## void setBoundBox ( BoundBox bb )

Sets the bounding box for the entire mesh.
### Arguments

- *BoundBox* **bb** - Bounding box to set.

## void setBoundSphere ( BoundSphere bs , int surface )

Sets the bounding sphere for the specified surface.
### Arguments

- *BoundSphere* **bs** - Bounding sphere to set.
- *int* **surface** - Surface index.

## void setBoundSphere ( BoundSphere bs )

Sets the bounding sphere for the entire mesh.
### Arguments

- *BoundSphere* **bs** - Bounding sphere to set.
