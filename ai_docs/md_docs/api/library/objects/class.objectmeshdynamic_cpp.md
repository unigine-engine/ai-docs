# ObjectMeshDynamic Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


This class is used to procedurally create dynamic meshes (i.e. triangles), lines, or points and modify them in runtime. You can also load an existing mesh as a dynamic one to modify it.


#### See Also


- Article on [ObjectMeshDynamic class usage examples](../../../code/usage/dynamic_meshes/index_cpp.md)
- C++ sample
- C# sample
- UnigineScript samples:

  -
  -
  -
  -
  -
  -


## ObjectMeshDynamic Class

### Members

## void setNumIndices ( int indices )

Sets a new number of vertex indices.
### Arguments

- *int* **indices** - The number of vertex indices.

## int getNumIndices () const

Returns the current number of vertex indices.
### Return value

Current number of vertex indices.
## void setNumVertex ( int vertex )

Sets a new number of mesh vertices.
### Arguments

- *int* **vertex** - The number of mesh vertices.

## int getNumVertex () const

Returns the current number of mesh vertices.
### Return value

Current number of mesh vertices.
## void setMeshName ( const char * name )

Sets a new mesh name.
### Arguments

- *const char ** **name** - The mesh name.

## const char * getMeshName () const

Returns the current mesh name.
### Return value

Current mesh name.
## void setUpdateDistanceLimit ( float limit )

Sets a new distance from the camera within which the object should be updated. The default value is infinity.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_cpp.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_cpp.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_cpp.md#BODY_WATER) assigned.


### Arguments

- *float* **limit** - The distance from the camera within which the object should be updated.

## float getUpdateDistanceLimit () const

Returns the current distance from the camera within which the object should be updated. The default value is infinity.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_cpp.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_cpp.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_cpp.md#BODY_WATER) assigned.


### Return value

Current distance from the camera within which the object should be updated.
## void setFPSInvisible ( int fpsinvisible )

Sets a new update rate value when the object is not rendered at all. The default value is 0 fps.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_cpp.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_cpp.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_cpp.md#BODY_WATER) assigned.


### Arguments

- *int* **fpsinvisible** - The update rate value when the object is not rendered at all.

## int getFPSInvisible () const

Returns the current update rate value when the object is not rendered at all. The default value is 0 fps.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_cpp.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_cpp.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_cpp.md#BODY_WATER) assigned.


### Return value

Current update rate value when the object is not rendered at all.
## void setFPSVisibleShadow ( int shadow )

Sets a new update rate value when only object shadows are rendered. The default value is 30 fps.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_cpp.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_cpp.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_cpp.md#BODY_WATER) assigned.


### Arguments

- *int* **shadow** - The update rate value when only object shadows are rendered.

## int getFPSVisibleShadow () const

Returns the current update rate value when only object shadows are rendered. The default value is 30 fps.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_cpp.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_cpp.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_cpp.md#BODY_WATER) assigned.


### Return value

Current update rate value when only object shadows are rendered.
## void setFPSVisibleCamera ( int camera )

Sets a new update rate value when the object is rendered to the viewport.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_cpp.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_cpp.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_cpp.md#BODY_WATER) assigned.


### Arguments

- *int* **camera** - The update rate value when the object is rendered to the viewport.

## int getFPSVisibleCamera () const

Returns the current update rate value when the object is rendered to the viewport.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_cpp.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_cpp.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_cpp.md#BODY_WATER) assigned.


### Return value

Current update rate value when the object is rendered to the viewport.
## bool isUniqueMesh () const

Returns the current value indicating if the mesh used by the object is unique (different from the one shared by other dynamic mesh objects in the world by default).
### Return value

**true** if the object uses a unique mesh; otherwise **false**.
## bool isUsageShared () const

Returns the current value indicating if the dynamic mesh object has the [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) flag enabled.
### Return value

**true** if the dynamic mesh object has the [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) flag enabled; otherwise **false**.
---

## static ObjectMeshDynamicPtr create ( const Ptr < Mesh > & mesh , int flags = 0 )

ObjectMeshDynamic constructor.
> **Notice:** A default surface named "`dynamic`" is created automatically, allowing geometry to be added to the object immediately after creation without explicitly specifying a surface index.
>
>
> To add more surfaces, use *[addSurface()](../../../api/library/objects/class.objectmeshdynamic_cpp.md#addSurface_cstr_void)*. The first call simply assigns a user-defined name to the existing internal surface and does not change the total number of surfaces (any geometry created before the call, if any, is preserved). Subsequent calls create additional surfaces as needed.


> **Notice:** The [USAGE_IMMUTABLE_VERTEX](#USAGE_IMMUTABLE_VERTEX) flag cannot be used together with [USAGE_DYNAMIC_VERTEX](#USAGE_DYNAMIC_VERTEX) flag.
>
>
> The [USAGE_IMMUTABLE_INDICES](#USAGE_IMMUTABLE_INDICES) flag cannot be used together with [USAGE_DYNAMIC_INDICES](#USAGE_DYNAMIC_INDICES) flag.
>
>
> [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) can be used only together with [USAGE_IMMUTABLE_ALL](#USAGE_IMMUTABLE_ALL).


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - [Mesh](../../../api/library/rendering/class.mesh_cpp.md) smart pointer.
- *int* **flags** - Dynamic flag: one of the [USAGE_DYNAMIC_*](#USAGE_DYNAMIC_ALL) or [USAGE_IMMUTABLE_*](#USAGE_IMMUTABLE_ALL).

## static ObjectMeshDynamicPtr create ( int flags = 0 )

ObjectMeshDynamic constructor.
> **Notice:** A default surface named "`dynamic`" is created automatically, allowing geometry to be added to the object immediately after creation without explicitly specifying a surface index.
>
>
> To add more surfaces, use *[addSurface()](../../../api/library/objects/class.objectmeshdynamic_cpp.md#addSurface_cstr_void)*. The first call simply assigns a user-defined name to the existing internal surface and does not change the total number of surfaces (any geometry created before the call, if any, is preserved). Subsequent calls create additional surfaces as needed.


> **Notice:** The [USAGE_IMMUTABLE_VERTEX](#USAGE_IMMUTABLE_VERTEX) flag cannot be used together with [USAGE_DYNAMIC_VERTEX](#USAGE_DYNAMIC_VERTEX) flag.
>
>
> The [USAGE_IMMUTABLE_INDICES](#USAGE_IMMUTABLE_INDICES) flag cannot be used together with [USAGE_DYNAMIC_INDICES](#USAGE_DYNAMIC_INDICES) flag.
>
>
> [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) can be used only together with [USAGE_IMMUTABLE_ALL](#USAGE_IMMUTABLE_ALL).


### Arguments

- *int* **flags** - Dynamic flag: one of the [USAGE_DYNAMIC_*](#USAGE_DYNAMIC_ALL) or [USAGE_IMMUTABLE_*](#USAGE_IMMUTABLE_ALL).

## static ObjectMeshDynamicPtr create ( const char * path , int flags = 0 )

ObjectMeshDynamic constructor.
> **Notice:** A default surface named "`dynamic`" is created automatically, allowing geometry to be added to the object immediately after creation without explicitly specifying a surface index.
>
>
> To add more surfaces, use *[addSurface()](../../../api/library/objects/class.objectmeshdynamic_cpp.md#addSurface_cstr_void)*. The first call simply assigns a user-defined name to the existing internal surface and does not change the total number of surfaces (any geometry created before the call, if any, is preserved). Subsequent calls create additional surfaces as needed.


> **Notice:** The [USAGE_IMMUTABLE_VERTEX](#USAGE_IMMUTABLE_VERTEX) flag cannot be used together with [USAGE_DYNAMIC_VERTEX](#USAGE_DYNAMIC_VERTEX) flag.
>
>
> The [USAGE_IMMUTABLE_INDICES](#USAGE_IMMUTABLE_INDICES) flag cannot be used together with [USAGE_DYNAMIC_INDICES](#USAGE_DYNAMIC_INDICES) flag.
>
>
> [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) can be used only together with [USAGE_IMMUTABLE_ALL](#USAGE_IMMUTABLE_ALL).


### Arguments

- *const char ** **path** - Path to the mesh file.
- *int* **flags** - Dynamic flag: one of the [USAGE_DYNAMIC_*](#USAGE_DYNAMIC_ALL) or [USAGE_IMMUTABLE_*](#USAGE_IMMUTABLE_ALL).

## void setBoundBox ( const Math:: BoundBox & bb )

Sets a bounding box of a specified size for a given dynamic mesh surface.
### Arguments

- *const  Math::[BoundBox](../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

## void setBoundBox ( const Math:: BoundBox & bb , int surface )

Sets a bounding box of a specified size for a given dynamic mesh surface.
### Arguments

- *const  Math::[BoundBox](../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.
- *int* **surface** - Surface number in range from 0 to the total number of dynamic mesh surfaces.

## void setColor ( int num , const Math:: vec4 & color )

Updates the color of a given vertex.
### Arguments

- *int* **num** - Vertex number in range from 0 to the total number of mesh vertices.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color.

## Math:: vec4 getColor ( int num ) const

Returns the color of a given vertex.
### Arguments

- *int* **num** - Vertex number in range from 0 to the total number of mesh vertices.

### Return value

Color.
## void setIndex ( int num , int index )

Updates an index in the index buffer (replaces the index with the given number with the specified index of the vertex).
### Arguments

- *int* **num** - Index number in range from 0 to the total number of indices in the index buffer.
- *int* **index** - Vertex index in the index buffer to set.

## int getIndex ( int num ) const

Returns the index of the vertex by the index number.
### Arguments

- *int* **num** - Index number in range from 0 to the total number of indices in the index buffer.

### Return value

Vertex index in the index buffer.
## void setIndicesArray ( int * OUT_indices , int indices_size )

Updates the array of indices.
### Arguments

- *int ** **OUT_indices** - Source array to be used to update indices. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **indices_size** - Size of the indices array.

## int setMesh ( const Ptr < Mesh > & mesh )

Allows for reinitialization of the ObjectMeshDynamic: it copies a given mesh into the current dynamic mesh. For example, you can copy a mesh into another one as follows:
```cpp
// create ObjectMeshDynamic instances
ObjectMeshDynamicPtr dynamicMesh = ObjectMeshDynamic::create();
ObjectMeshDynamicPtr dynamicMesh_2 = ObjectMeshDynamic::create();

// create a Mesh instance
MeshPtr firstMesh = Mesh::create();

// get the mesh of the ObjectMeshDynamic and copy it to the Mesh class instance
dynamicMesh->getMesh(firstMesh);

// put the firstMesh mesh to the dynamicMesh_2 instance
dynamicMesh_2->setMesh(firstMesh);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - Mesh smart pointer.

### Return value

**1** if the mesh is copied successfully; otherwise, **0**.
## int getMesh ( const Ptr < Mesh > & mesh ) const

Copies the current dynamic mesh into the received mesh. For example, you can obtain geometry of the dynamic mesh and then change it:
```cpp
// a dynamic mesh from which geometry will be obtained
MeshPtr mesh_0 = Mesh::create("box.mesh");
ObjectMeshDynamicPtr dynamicMesh = ObjectMeshDynamic::create(mesh_0);
// create a new mesh
MeshPtr mesh_1 = Mesh::create();
// copy geometry to the Mesh instance
if(dynamicMesh->getMesh(mesh_1)) {
	// do something with the obtained mesh
} else {
	Log::error("Failed to copy a mesh\n");
}

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - Mesh smart pointer.

### Return value

**1** if the mesh is copied successfully; otherwise, **0**.
## Math:: vec3 getNormal ( int num ) const

Returns the normal vector coordinates of a given vertex.
### Arguments

- *int* **num** - Vertex number in range from 0 to the total number of mesh vertices.

### Return value

Normal vector.
## void setSurfaceBegin ( int begin , int surface )

Sets the begin index for the specified surface of the dynamic object mesh.
### Arguments

- *int* **begin** - Index to be set as the begin one for the surface.
- *int* **surface** - Number of a target surface in range from 0 to the total number of mesh surfaces.

## int getSurfaceBegin ( int surface ) const

Returns the begin index of the specified mesh surface.
### Arguments

- *int* **surface** - Number of a target surface in range from 0 to the total number of mesh surfaces.

### Return value

Returns the begin index of the surface.
## void setSurfaceEnd ( int end , int surface )

Sets the end index for the specified surface of the dynamic object mesh.
### Arguments

- *int* **end** - Index to be set as the end one for the surface.
- *int* **surface** - Number of a target surface in range from 0 to the total number of mesh surfaces.

## int getSurfaceEnd ( int surface ) const

Returns the end index of the specified mesh surface.
### Arguments

- *int* **surface** - Number of a target surface in range from 0 to the total number of mesh surfaces.

### Return value

Returns the end index of the surface.
## void setSurfaceName ( const char * name , int surface )

Sets the name for the specified surface.
> **Notice:** The name will be set only if the specified surface was added via the *[addSurface()](../../../api/library/objects/class.objectmeshdynamic_cpp.md#addSurface_cstr_void)* method.


### Arguments

- *const char ** **name** - Surface name.
- *int* **surface** - Number of a target surface in range from 0 to the total number of mesh surfaces.

## void setTangent ( int num , const Math:: quat & tangent )

Updates the tangent vector coordinates of a given vertex.
### Arguments

- *int* **num** - Vertex number in range from 0 to the total number of mesh vertices.
- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **tangent** - Tangent vector coordinates.

## Math:: quat getTangent ( int num ) const

Returns the tangent vector coordinates of a given vertex.
### Arguments

- *int* **num** - Vertex number in range from 0 to the total number of mesh vertices.

### Return value

Tangent vector.
## void setTexCoord ( int num , const Math:: vec4 & texcoord )

Updates texture coordinates of a given vertex.
### Arguments

- *int* **num** - Vertex number in range from 0 to the total number of mesh vertices.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **texcoord** - New coordinate pairs for both texture channels.

## Math:: vec4 getTexCoord ( int num ) const

Returns texture coordinates of a given vertex.
### Arguments

- *int* **num** - Vertex number in range from 0 to the total number of mesh vertices.

### Return value

Coordinate pairs for both texture channels.
## void setVertex ( int num , const Math:: vec3 & xyz )

Updates coordinates of a given vertex.
### Arguments

- *int* **num** - Vertex number.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **xyz** - New vertex coordinates in the mesh system of coordinates.

## Math:: vec3 getVertex ( int num ) const

Returns coordinates of a given vertex.
### Arguments

- *int* **num** - Vertex number in range from 0 to the total number of mesh vertices.

### Return value

Vertex coordinates in the mesh system of coordinates.
## void setVertexArray ( ObjectMeshDynamic::Vertex* OUT_vertex , int vertex_size )

Updates the vertex array of the dynamic mesh.
### Arguments

- *[ObjectMeshDynamic::Vertex*](../../../api/library/objects/class.objectmeshdynamic_cpp.md#Vertex*)* **OUT_vertex** - Source array to be used to update the vertex array of the dynamic mesh. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **vertex_size** - Size of the vertex array.

## const ObjectMeshDynamic::Vertex * getVertexArray ( ) const

Returns an array of vertices of the dynamic mesh.
### Return value

Pointer to the array of vertices.
## bool isFlushed ( ) const

Returns a value indicating if vertex data of the mesh was flushed (create/upload operation) to video memory.
### Return value

true if vertex data of the mesh was flushed (create/upload operation) to video memory; otherwise, false.
## void addColor ( const Math:: vec4 & color )

Adds a color with given coordinates to the last added vertex.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color.

## void addIndex ( int index )

Adds an index to the index buffer.
### Arguments

- *int* **index** - Index to add.

## void addIndicesArray ( int* OUT_indices , int indices_size )

Adds an array of indices.
### Arguments

- *int** **OUT_indices** - Array of indices to be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **indices_size** - Size of the indices array.

## void addSurface ( const char * name )

Adds all the last listed and unsigned vertices and triangles to a new surface with a specified name.
> **Notice:** For your convenience, *[ObjectMeshDynamic::create()](../../../api/library/objects/class.objectmeshdynamic_cpp.md#ObjectMeshDynamic_constPtrMesh_int)* initializes the object with one internal surface named "`dynamic`". The first call to *[addSurface()](../../../api/library/objects/class.objectmeshdynamic_cpp.md#addSurface_cstr_void)* simply assigns a user-defined name to this surface and does not change the total number of surfaces (any geometry created before the call, if any, is preserved). Subsequent calls create additional surfaces as needed.


### Arguments

- *const char ** **name** - Name of the new surface.

## void addTangent ( const Math:: quat & tangent )

Adds a tangent vector with given coordinates to the last added vertex.
### Arguments

- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **tangent** - Tangent vector coordinates.

## void addTexCoord ( const Math:: vec4 & texcoord )

Adds texture coordinates to the last added vertex.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **texcoord** - Coordinate pairs for both texture channels.

## void addTriangleFan ( int num_vertex )

Adds a triangle fan to the mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with the [addVertex()](#addVertex_vec3_void) function. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_vertex** - Number of vertices of the fan.

## void addTriangleQuads ( int num_quads )

Adds a given number of quadrilaterals to the mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with the [addVertex()](#addVertex_vec3_void) function. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_quads** - Number of quadrilaterals.

## void addTriangles ( int num_triangles )

Adds a given number of triangles to the mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with the [addVertex()](#addVertex_vec3_void) function. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_triangles** - Number of triangles.

## void addTriangleStrip ( int num_vertex )

Adds a triangle strip to the mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with the [addVertex()](#addVertex_vec3_void) function. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_vertex** - Number of vertices of the strip.

## void addVertex ( const Math:: vec3 & xyz )

Adds a vertex with given coordinates to the mesh.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **xyz** - Vertex coordinates in the mesh system of coordinates.

## void addVertexArray ( Vertex* OUT_vertex , int vertex_size )

Adds an array of vertices to the dynamic mesh.
### Arguments

- *Vertex** **OUT_vertex** - Array of vertices to be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **vertex_size** - Size of the vertex array.

## void allocateIndices ( int num )

Allocates a given number of vertex indices in the index buffer. With this function, memory can be allocated once rather than in chunks, making the creation faster.
### Arguments

- *int* **num** - Number of vertex indices that will be stored in the buffer.

## void allocateVertex ( int num )

Allocates a given number of vertices in the vertex buffer. With this function, memory can be allocated once rather than in chunks, making the creation faster.
### Arguments

- *int* **num** - Number of vertices to allocate.

## void clearIndices ( )

Clears all vertex indices in the mesh.
## void clearSurfaces ( )

Clears all the surface settings.
## void clearVertex ( )

Clears all of the mesh vertex settings.
## void flushIndices ( )

Flushes the index buffer and sends all data to GPU. This method is called automatically, if the length of the index buffer changes. If you change the contents of the index buffers, you should call this method.
## void flushVertex ( )

Flushes the vertex buffer and sends all data to GPU. This method is called automatically, if the length of the vertex buffer changes. If you change the contents of the vertex buffer, you should call this method.
## bool loadMesh ( const char * path )

Loads a mesh for the current mesh from the file. This function doesn't change the mesh name.
### Arguments

- *const char ** **path** - Mesh file name.

### Return value

true if the mesh is loaded successfully; otherwise, false.
## void removeIndices ( int num , int size )

Removes the specified number of indices starting from the given index.
### Arguments

- *int* **num** - Index number.
- *int* **size** - Number of indices to remove.

## void removeSurface ( int surface )

Removes the surface with the given index.
### Arguments

- *int* **surface** - Surface index.

## void removeSurfaces ( const char * name )

Removes surfaces with the given name.
### Arguments

- *const char ** **name** - Surface name.

## void removeVertex ( int num , int size , int indices )

Removes the specified number of vertices starting from the given vertex. To fix the index buffer after removal of vertices, pass true as the 3rd argument.
### Arguments

- *int* **num** - Vertex number.
- *int* **size** - Number of vertices to remove.
- *int* **indices** - 1 to fix the index buffer after removal of vertices; otherwise, 0.

## bool saveMesh ( const char * path )

Saves the dynamic mesh into `.mesh` or `.anim` format.
### Arguments

- *const char ** **path** - Mesh file name.

### Return value

true if the mesh is saved successfully; otherwise, false.
## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cpp.md) type identifier.
## bool updateBounds ( )

Calculates a bounding box and a bounding sphere for the current mesh.
### Return value

true if the bounds are calculated successfully; otherwise, false.
## bool updateIndices ( )

Updates vertex and index buffers by removing duplicated vertices and rearranging the indices of the created mesh to optimize it for faster rendering.
### Return value

true if the indices are updated successfully; otherwise, false.
## void updateSurfaceBegin ( int surface )

Synchronizes surface begin index.
### Arguments

- *int* **surface** - Number of a target surface in range from 0 to the total number of mesh surfaces.

## void updateSurfaceEnd ( int surface )

Synchronizes surface end index.
### Arguments

- *int* **surface** - Number of a target surface.

## bool updateTangents ( )

Updates tangent vectors of the mesh vertices.
### Return value

true if the tangents are updated successfully; otherwise, false.
## void putUniqueMesh ( )

Makes the mesh used by the object unique (different from the one shared by other Dynamic Mesh objects in the world by default).
## Ptr < ResourceExternalMemory > getExternalMemoryVertexBuffer ( ) const

Returns the pointer to the vertex buffer of the resource in video memory. If the [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) flag is not enabled for the resource, this method returns nullptr.
### Return value

The pointer to the vertex buffer of the resource in video memory. If the [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) flag is not enabled for the resource, this method returns nullptr.
## Ptr < ResourceExternalMemory > getExternalMemoryIndexBuffer ( ) const

Returns the pointer to the index buffer of the resource in video memory. If the [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) flag is not enabled for the resource, this method returns nullptr.
### Return value

The pointer to the index buffer of the resource in video memory. If the [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) flag is not enabled for the resource, this method returns nullptr.
