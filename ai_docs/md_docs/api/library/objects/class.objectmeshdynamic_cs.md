# ObjectMeshDynamic Class (CS)

**Inherits from:** Object


This class is used to procedurally create dynamic meshes (i.e. triangles), lines, or points and modify them in runtime. You can also load an existing mesh as a dynamic one to modify it.


#### See Also


- Article on [ObjectMeshDynamic class usage examples](../../../code/usage/dynamic_meshes/index_cs.md)
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

### Properties

## int NumIndices

The number of vertex indices.
## int NumVertex

The number of mesh vertices.
## string MeshName

The mesh name.
## float UpdateDistanceLimit

The distance from the camera within which the object should be updated. The default value is infinity.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_cs.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_cs.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_cs.md#BODY_WATER) assigned.


## int FPSInvisible

The update rate value when the object is not rendered at all. The default value is 0 fps.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_cs.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_cs.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_cs.md#BODY_WATER) assigned.


## int FPSVisibleShadow

The update rate value when only object shadows are rendered. The default value is 30 fps.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_cs.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_cs.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_cs.md#BODY_WATER) assigned.


## int FPSVisibleCamera

The update rate value when the object is rendered to the viewport.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_cs.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_cs.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_cs.md#BODY_WATER) assigned.


## 🔒︎ bool IsUniqueMesh

The value indicating if the mesh used by the object is unique (different from the one shared by other dynamic mesh objects in the world by default).
## 🔒︎ bool IsUsageShared

The value indicating if the dynamic mesh object has the [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) flag enabled.
### Members

---

## ObjectMeshDynamic ( Mesh mesh , int flags = 0 )

ObjectMeshDynamic constructor.
> **Notice:** A default surface named "`dynamic`" is created automatically, allowing geometry to be added to the object immediately after creation without explicitly specifying a surface index.
>
>
> To add more surfaces, use *[AddSurface()](../../../api/library/objects/class.objectmeshdynamic_cs.md#addSurface_cstr_void)*. The first call simply assigns a user-defined name to the existing internal surface and does not change the total number of surfaces (any geometry created before the call, if any, is preserved). Subsequent calls create additional surfaces as needed.


> **Notice:** The [USAGE_IMMUTABLE_VERTEX](#USAGE_IMMUTABLE_VERTEX) flag cannot be used together with [USAGE_DYNAMIC_VERTEX](#USAGE_DYNAMIC_VERTEX) flag.
>
>
> The [USAGE_IMMUTABLE_INDICES](#USAGE_IMMUTABLE_INDICES) flag cannot be used together with [USAGE_DYNAMIC_INDICES](#USAGE_DYNAMIC_INDICES) flag.
>
>
> [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) can be used only together with [USAGE_IMMUTABLE_ALL](#USAGE_IMMUTABLE_ALL).


### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - [Mesh](../../../api/library/rendering/class.mesh_cs.md) instance.
- *int* **flags** - Dynamic flag: one of the [USAGE_DYNAMIC_*](#USAGE_DYNAMIC_ALL) or [USAGE_IMMUTABLE_*](#USAGE_IMMUTABLE_ALL).

## ObjectMeshDynamic ( int flags = 0 )

ObjectMeshDynamic constructor.
> **Notice:** A default surface named "`dynamic`" is created automatically, allowing geometry to be added to the object immediately after creation without explicitly specifying a surface index.
>
>
> To add more surfaces, use *[AddSurface()](../../../api/library/objects/class.objectmeshdynamic_cs.md#addSurface_cstr_void)*. The first call simply assigns a user-defined name to the existing internal surface and does not change the total number of surfaces (any geometry created before the call, if any, is preserved). Subsequent calls create additional surfaces as needed.


> **Notice:** The [USAGE_IMMUTABLE_VERTEX](#USAGE_IMMUTABLE_VERTEX) flag cannot be used together with [USAGE_DYNAMIC_VERTEX](#USAGE_DYNAMIC_VERTEX) flag.
>
>
> The [USAGE_IMMUTABLE_INDICES](#USAGE_IMMUTABLE_INDICES) flag cannot be used together with [USAGE_DYNAMIC_INDICES](#USAGE_DYNAMIC_INDICES) flag.
>
>
> [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) can be used only together with [USAGE_IMMUTABLE_ALL](#USAGE_IMMUTABLE_ALL).


### Arguments

- *int* **flags** - Dynamic flag: one of the [USAGE_DYNAMIC_*](#USAGE_DYNAMIC_ALL) or [USAGE_IMMUTABLE_*](#USAGE_IMMUTABLE_ALL).

## ObjectMeshDynamic ( string path , int flags = 0 )

ObjectMeshDynamic constructor.
> **Notice:** A default surface named "`dynamic`" is created automatically, allowing geometry to be added to the object immediately after creation without explicitly specifying a surface index.
>
>
> To add more surfaces, use *[AddSurface()](../../../api/library/objects/class.objectmeshdynamic_cs.md#addSurface_cstr_void)*. The first call simply assigns a user-defined name to the existing internal surface and does not change the total number of surfaces (any geometry created before the call, if any, is preserved). Subsequent calls create additional surfaces as needed.


> **Notice:** The [USAGE_IMMUTABLE_VERTEX](#USAGE_IMMUTABLE_VERTEX) flag cannot be used together with [USAGE_DYNAMIC_VERTEX](#USAGE_DYNAMIC_VERTEX) flag.
>
>
> The [USAGE_IMMUTABLE_INDICES](#USAGE_IMMUTABLE_INDICES) flag cannot be used together with [USAGE_DYNAMIC_INDICES](#USAGE_DYNAMIC_INDICES) flag.
>
>
> [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) can be used only together with [USAGE_IMMUTABLE_ALL](#USAGE_IMMUTABLE_ALL).


### Arguments

- *string* **path** - Path to the mesh file.
- *int* **flags** - Dynamic flag: one of the [USAGE_DYNAMIC_*](#USAGE_DYNAMIC_ALL) or [USAGE_IMMUTABLE_*](#USAGE_IMMUTABLE_ALL).

## void SetBoundBox ( BoundBox bb )

Sets a bounding box of a specified size for a given dynamic mesh surface.
### Arguments

- *[BoundBox](../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

## void SetBoundBox ( BoundBox bb , int surface )

Sets a bounding box of a specified size for a given dynamic mesh surface.
### Arguments

- *[BoundBox](../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.
- *int* **surface** - Surface number in range from 0 to the total number of dynamic mesh surfaces.

## void SetColor ( int num , vec4 color )

Updates the color of a given vertex.
### Arguments

- *int* **num** - Vertex number in range from 0 to the total number of mesh vertices.
- *vec4* **color** - Color.

## vec4 GetColor ( int num )

Returns the color of a given vertex.
### Arguments

- *int* **num** - Vertex number in range from 0 to the total number of mesh vertices.

### Return value

Color.
## void SetIndex ( int num , int index )

Updates an index in the index buffer (replaces the index with the given number with the specified index of the vertex).
### Arguments

- *int* **num** - Index number in the index buffer.
- *int* **index** - Vertex index in the index buffer to set.

## int GetIndex ( int num )

Returns the index of the vertex by the index number.
### Arguments

- *int* **num** - Index number in the index buffer.

### Return value

Vertex index in the index buffer.
## void SetIndicesArray ( int[] OUT_indices )

Updates the array of indices.
### Arguments

- *int[]* **OUT_indices** - Source array to be used to update indices. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## int SetMesh ( Mesh mesh )

Allows for reinitialization of the ObjectMeshDynamic: it copies a given mesh into the current dynamic mesh. For example, you can copy a mesh into another one as follows:
```csharp
// create ObjectMeshDynamic instances
ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic();
ObjectMeshDynamic dynamicMesh_2 = new ObjectMeshDynamic();

// create a Mesh instance
Mesh firstMesh = new Mesh();

// get the mesh of the ObjectMeshDynamic and copy it to the Mesh class instance
dynamicMesh.GetMesh(firstMesh);

// put the firstMesh mesh to the dynamicMesh_2 instance
dynamicMesh_2.SetMesh(firstMesh);

```


### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Mesh.

### Return value

**1** if the mesh is copied successfully; otherwise, **0**.
## int GetMesh ( Mesh mesh )

Copies the current dynamic mesh into the received mesh. For example, you can obtain geometry of the dynamic mesh and then change it:
```csharp
// a dynamic mesh from which geometry will be obtained
Mesh mesh_0 = new Mesh("box.mesh");
ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic(mesh_0);
// create a new mesh
Mesh mesh_1 = new Mesh();
// copy geometry to the Mesh instance
if(dynamicMesh.GetMesh(mesh_1) == 1) {
	// do something with the obtained mesh
} else {
	Log.Error("Failed to copy a mesh\n");
}

```


### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Mesh.

### Return value

**1** if the mesh is copied successfully; otherwise, **0**.
## vec3 GetNormal ( int num )

Returns the normal vector coordinates of a given vertex.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.

### Return value

Normal vector.
## void SetSurfaceBegin ( int begin , int surface )

Sets the begin index for the specified surface of the dynamic object mesh.
### Arguments

- *int* **begin** - Begin index.
- *int* **surface** - Number of the target surface.

## int GetSurfaceBegin ( int surface )

Returns the begin index of the specified mesh surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Returns the begin index of the surface.
## void SetSurfaceEnd ( int end , int surface )

Sets the end index for the specified surface of the dynamic object mesh.
### Arguments

- *int* **end** - End index.
- *int* **surface** - Number of the target surface.

## int GetSurfaceEnd ( int surface )

Returns the end index of the specified mesh surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Returns the end index of the surface.
## void SetSurfaceName ( string name , int surface )

Sets the name for the specified surface.
> **Notice:** The name will be set only if the specified surface was added via the *[AddSurface()](../../../api/library/objects/class.objectmeshdynamic_cs.md#addSurface_cstr_void)* method.


### Arguments

- *string* **name** - New name of the surface.
- *int* **surface** - Number of a target surface in range from **0** to the total number of surfaces.

## void SetTangent ( int num , quat tangent )

Updates the tangent vector coordinates of a given vertex.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.
- *quat* **tangent** - Tangent vector to be set.

## quat GetTangent ( int num )

Returns the tangent vector coordinates of a given vertex.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.

### Return value

Tangent vector.
## void SetTexCoord ( int num , vec4 texcoord )

Updates texture coordinates of a given vertex.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.
- *vec4* **texcoord** - New coordinate pairs for both texture channels.

## vec4 GetTexCoord ( int num )

Returns texture coordinates of a given vertex.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.

### Return value

Coordinate pairs for both texture channels.
## void SetVertex ( int num , vec3 xyz )

Updates coordinates of a given vertex.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.
- *vec3* **xyz** - New coordinates in the mesh system of coordinates.

## vec3 GetVertex ( int num )

Returns coordinates of a given vertex.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.

### Return value

Vertex coordinates in the mesh system of coordinates.
## void SetVertexArray ( ObjectMeshDynamic.Vertex [] OUT_vertex )

Updates the vertex array of the dynamic mesh.
### Arguments

- *[ObjectMeshDynamic.Vertex](../../../api/library/objects/class.objectmeshdynamic_cs.md#Vertex)[]* **OUT_vertex** - Source array to be used to update the vertex array of the dynamic mesh. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## bool IsFlushed ( )

Returns a value indicating if vertex data of the mesh was flushed (create/upload operation) to video memory.
### Return value

true if vertex data of the mesh was flushed (create/upload operation) to video memory; otherwise, false.
## void AddColor ( vec4 color )

Adds a color with given coordinates to the last added vertex.
### Arguments

- *vec4* **color** - Color.

## void AddIndex ( int index )

Adds an index to the index buffer.
### Arguments

- *int* **index** - Index to add.

## void AddIndicesArray ( int[] OUT_indices )

Adds an array of indices.
### Arguments

- *int[]* **OUT_indices** - Array of indices to be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void AddSurface ( string name )

Adds all the last listed and unsigned vertices and triangles to a new surface with a specified name.
> **Notice:** For your convenience, *[ObjectMeshDynamic()](../../../api/library/objects/class.objectmeshdynamic_cs.md#ObjectMeshDynamic_constPtrMesh_int)* initializes the object with one internal surface named "`dynamic`". The first call to *[AddSurface()](../../../api/library/objects/class.objectmeshdynamic_cs.md#addSurface_cstr_void)* simply assigns a user-defined name to this surface and does not change the total number of surfaces (any geometry created before the call, if any, is preserved). Subsequent calls create additional surfaces as needed.


### Arguments

- *string* **name** - Name of the new surface.

## void AddTangent ( quat tangent )

Adds a tangent vector with given coordinates to the last added vertex.
### Arguments

- *quat* **tangent** - Tangent to add.

## void AddTexCoord ( vec4 texcoord )

Adds texture coordinates to the last added vertex.
### Arguments

- *vec4* **texcoord** - Coordinate pairs for both texture channels.

## void AddTriangleFan ( int num_vertex )

Adds a triangle fan to the mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with the [addVertex()](#addVertex_vec3_void) function. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_vertex** - Number of vertices comprising the fan.

## void AddTriangleQuads ( int num_quads )

Adds a given number of quadrilaterals to the mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with the [addVertex()](#addVertex_vec3_void) function. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_quads** - Number of quadrilaterals to add.

## void AddTriangles ( int num_triangles )

Adds a given number of triangles to the mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with the [addVertex()](#addVertex_vec3_void) function. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_triangles** - Number of triangles.

## void AddTriangleStrip ( int num_vertex )

Adds a triangle strip to the mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with the [addVertex()](#addVertex_vec3_void) function. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_vertex** - Number of vertices comprising the strip.

## void AddVertex ( vec3 xyz )

Adds a vertex with given coordinates to the mesh.
### Arguments

- *vec3* **xyz** - Vertex coordinates in the mesh system of coordinates.

## void AddVertexArray ( Vertex[] OUT_vertex )

Adds an array of vertices to the dynamic mesh.
### Arguments

- *Vertex[]* **OUT_vertex** - Array of vertices to be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void AllocateIndices ( int num )

Allocates a given number of vertex indices in the index buffer. With this function, memory can be allocated once rather than in chunks, making the creation faster.
### Arguments

- *int* **num** - The number of indices that will be stored in a buffer.

## void AllocateVertex ( int num )

Allocates a given number of vertices in the vertex buffer. With this function, memory can be allocated once rather than in chunks, making the creation faster.
### Arguments

- *int* **num** - The number of vertices that will be stored in a buffer.

## void ClearIndices ( )

Clears all vertex indices in the mesh.
## void ClearSurfaces ( )

Clears all the surface settings.
## void ClearVertex ( )

Clears all of the mesh vertex settings.
## void FlushIndices ( )

Flushes the index buffer and sends all data to GPU. This method is called automatically, if the length of the index buffer changes. If you change the contents of the index buffers, you should call this method.
## void FlushVertex ( )

Flushes the vertex buffer and sends all data to GPU. This method is called automatically, if the length of the vertex buffer changes. If you change the contents of the vertex buffer, you should call this method.
## bool LoadMesh ( string path )

Loads a mesh for the current mesh from the file. This function doesn't change the mesh name.
### Arguments

- *string* **path** - Mesh file name.

### Return value

true if the mesh is loaded successfully; otherwise, false.
## void RemoveIndices ( int num , int size )

Removes the specified number of indices starting from the given index.
### Arguments

- *int* **num** - Number of the index in the index buffer.
- *int* **size** - Number of indices to remove.

## void RemoveSurface ( int surface )

Removes the surface with the given index.
### Arguments

- *int* **surface** - Surface index.

## void RemoveSurfaces ( string name )

Removes surfaces with the given name.
### Arguments

- *string* **name** - Surface name.

## void RemoveVertex ( int num , int size , int indices )

Removes the specified number of vertices starting from the given vertex. To fix the index buffer after removal of vertices, pass true as the 3rd argument.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.
- *int* **size** - Number of vertices to remove.
- *int* **indices** - 1 to fix the index buffer after removal of vertices; otherwise, 0.

## bool SaveMesh ( string path )

Saves the dynamic mesh into `.mesh` or `.anim` format.
### Arguments

- *string* **path** - Mesh file name.

### Return value

true if the mesh is saved successfully; otherwise, false.
## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cs.md) type identifier.
## bool UpdateBounds ( )

Calculates a bounding box and a bounding sphere for the current mesh.
### Return value

true if the bounds are calculated successfully; otherwise, false.
## bool UpdateIndices ( )

Updates vertex and index buffers by removing duplicated vertices and rearranging the indices of the created mesh to optimize it for faster rendering.
### Return value

true if the indices are updated successfully; otherwise, false.
## void UpdateSurfaceBegin ( int surface )

Synchronizes surface begin index.
### Arguments

- *int* **surface** - ID of a target surface.

## void UpdateSurfaceEnd ( int surface )

Synchronizes surface end index.
### Arguments

- *int* **surface** - ID of a target surface.

## bool UpdateTangents ( )

Updates tangent vectors of the mesh vertices.
### Return value

true if the tangents are updated successfully; otherwise, false.
## void PutUniqueMesh ( )

Makes the mesh used by the object unique (different from the one shared by other Dynamic Mesh objects in the world by default).
