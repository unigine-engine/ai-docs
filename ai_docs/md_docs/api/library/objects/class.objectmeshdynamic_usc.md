# ObjectMeshDynamic Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


This class is used to procedurally create dynamic meshes (i.e. triangles), lines, or points and modify them in runtime. You can also load an existing mesh as a dynamic one to modify it.


#### See Also


- Article on [ObjectMeshDynamic class usage examples](../../../code/usage/dynamic_meshes/index_usc.md)
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
## void setMeshName ( string name )

Sets a new mesh name.
### Arguments

- *string* **name** - The mesh name.

## const char * getMeshName () const

Returns the current mesh name.
### Return value

Current mesh name.
## void setUpdateDistanceLimit ( float limit )

Sets a new distance from the camera within which the object should be updated. The default value is infinity.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_usc.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_usc.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_usc.md#BODY_WATER) assigned.


### Arguments

- *float* **limit** - The distance from the camera within which the object should be updated.

## float getUpdateDistanceLimit () const

Returns the current distance from the camera within which the object should be updated. The default value is infinity.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_usc.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_usc.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_usc.md#BODY_WATER) assigned.


### Return value

Current distance from the camera within which the object should be updated.
## void setFPSInvisible ( int fpsinvisible )

Sets a new update rate value when the object is not rendered at all. The default value is 0 fps.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_usc.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_usc.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_usc.md#BODY_WATER) assigned.


### Arguments

- *int* **fpsinvisible** - The update rate value when the object is not rendered at all.

## int getFPSInvisible () const

Returns the current update rate value when the object is not rendered at all. The default value is 0 fps.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_usc.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_usc.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_usc.md#BODY_WATER) assigned.


### Return value

Current update rate value when the object is not rendered at all.
## void setFPSVisibleShadow ( int shadow )

Sets a new update rate value when only object shadows are rendered. The default value is 30 fps.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_usc.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_usc.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_usc.md#BODY_WATER) assigned.


### Arguments

- *int* **shadow** - The update rate value when only object shadows are rendered.

## int getFPSVisibleShadow () const

Returns the current update rate value when only object shadows are rendered. The default value is 30 fps.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_usc.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_usc.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_usc.md#BODY_WATER) assigned.


### Return value

Current update rate value when only object shadows are rendered.
## void setFPSVisibleCamera ( int camera )

Sets a new update rate value when the object is rendered to the viewport.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_usc.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_usc.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_usc.md#BODY_WATER) assigned.


### Arguments

- *int* **camera** - The update rate value when the object is rendered to the viewport.

## int getFPSVisibleCamera () const

Returns the current update rate value when the object is rendered to the viewport.
> **Notice:** This method is effective when the object has [BODY_ROPE](../../../api/library/physics/class.body_usc.md#BODY_ROPE), [BODY_CLOTH](../../../api/library/physics/class.body_usc.md#BODY_CLOTH), or [BODY_WATER](../../../api/library/physics/class.body_usc.md#BODY_WATER) assigned.


### Return value

Current update rate value when the object is rendered to the viewport.
## bool isUniqueMesh () const

Returns the current value indicating if the mesh used by the object is unique (different from the one shared by other dynamic mesh objects in the world by default).
### Return value

**true** if the object uses a unique mesh; otherwise **false**.
## int isUsageShared () const

Returns the current value indicating if the dynamic mesh object has the [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) flag enabled.
### Return value

Current the dynamic mesh object has the [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) flag enabled
---

## static ObjectMeshDynamic ( Mesh mesh , int flags = 0 )

ObjectMeshDynamic constructor.
> **Notice:** A default surface named "`dynamic`" is created automatically, allowing geometry to be added to the object immediately after creation without explicitly specifying a surface index.
>
>
> To add more surfaces, use *[addSurface()()](../../../api/library/objects/class.objectmeshdynamic_usc.md#addSurface_cstr_void)*. The first call simply assigns a user-defined name to the existing internal surface and does not change the total number of surfaces (any geometry created before the call, if any, is preserved). Subsequent calls create additional surfaces as needed.


> **Notice:** The [USAGE_IMMUTABLE_VERTEX](#USAGE_IMMUTABLE_VERTEX) flag cannot be used together with [USAGE_DYNAMIC_VERTEX](#USAGE_DYNAMIC_VERTEX) flag.
>
>
> The [USAGE_IMMUTABLE_INDICES](#USAGE_IMMUTABLE_INDICES) flag cannot be used together with [USAGE_DYNAMIC_INDICES](#USAGE_DYNAMIC_INDICES) flag.
>
>
> [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) can be used only together with [USAGE_IMMUTABLE_ALL](#USAGE_IMMUTABLE_ALL).


### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **mesh** - [Mesh](../../../api/library/rendering/class.mesh_usc.md) instance.
- *int* **flags** - Dynamic flag: one of the [OBJECT_MESH_DYNAMIC_USAGE_DYNAMIC_*](#USAGE_DYNAMIC_ALL) or [OBJECT_MESH_DYNAMIC_USAGE_IMMUTABLE_*](#USAGE_IMMUTABLE_ALL).

## void setBoundBox ( BoundBox bb )

Sets a bounding box of a specified size for a given dynamic mesh surface.
### Arguments

- *BoundBox* **bb** - Bounding box.

## void setBoundBox ( BoundBox bb , int surface )

Sets a bounding box of a specified size for a given dynamic mesh surface.
### Arguments

- *BoundBox* **bb** - Bounding box.
- *int* **surface** - Surface number in range from 0 to the total number of dynamic mesh surfaces.

## void setColor ( int num , vec4 color )

Updates the color of a given vertex.
### Arguments

- *int* **num** - Vertex number in range from 0 to the total number of mesh vertices.
- *vec4* **color** - Color.

## vec4 getColor ( int num )

Returns the color of a given vertex.
### Arguments

- *int* **num** - Vertex number in range from 0 to the total number of mesh vertices.

### Return value

Vertex color.
## void setIndex ( int num , int index )

Updates a given index in the index buffer (replaces the index with the given number with the specified index of the vertex).
### Arguments

- *int* **num** - Index number in the index buffer.
- *int* **index** - Vertex index in the index buffer to set.

## int getIndex ( int num )

Returns the index of the vertex by the index number.
### Arguments

- *int* **num** - Index number in the index buffer.

### Return value

Vertex index in the index buffer.
## int setMesh ( Mesh mesh )

Allows for reinitialization of the ObjectMeshDynamic: it copies a given mesh into the current dynamic mesh. For example, you can copy a mesh into another one as follows:
```cpp
// create ObjectMeshDynamic instances
ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic();
ObjectMeshDynamic dynamicMesh_2 = new ObjectMeshDynamic();

// create a Mesh instance
Mesh firstMesh = new Mesh();

// get the mesh of the ObjectMeshDynamic and copy it to the Mesh class instance
dynamicMesh.getMesh(firstMesh);

// put the firstMesh mesh to the dynamicMesh_2 instance
dynamicMesh_2.setMesh(firstMesh);

```


### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **mesh** - Mesh.

### Return value

**1** if the mesh is copied successfully; otherwise, **0**.
## int getMesh ( Mesh mesh )

Copies the current dynamic mesh into the received mesh. For example, you can obtain geometry of the dynamic mesh and then change it:
```cpp
// a dynamic mesh from which geometry will be obtained
Mesh mesh_0 = new Mesh("box.mesh");
ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic(mesh_0);
// create a new mesh
Mesh mesh_1 = new Mesh();
// copy geometry to the Mesh instance
if(dynamicMesh.getMesh(mesh_1)) {
	// do something with the obtained mesh
} else {
	log.error("Failed to copy a mesh\n");
}

```


### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **mesh** - Mesh.

### Return value

**1** if the mesh is copied successfully; otherwise, **0**.
## vec3 getNormal ( int num )

Returns a normal vector of a given vertex.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.

### Return value

The vertex normal vector.
## void setSurfaceBegin ( int begin , int surface )

Sets the begin index to the specified surface of the dynamic object mesh. It means that the surface will be rendered the first.
### Arguments

- *int* **begin** - Begin index.
- *int* **surface** - Number of the target surface.

## int getSurfaceBegin ( int surface )

Returns the begin index of the specified mesh surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Begin index of the surface.
## void setSurfaceEnd ( int end , int surface )

Sets the end index to the specified surface of the dynamic object mesh. It means that the surface will be rendered the last.
### Arguments

- *int* **end** - End index.
- *int* **surface** - Number of the target surface.

## int getSurfaceEnd ( int surface )

Returns the end index of the specified mesh surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Returns the end index of the surface.
## void setSurfaceName ( string name , int surface )

Sets the name for the specified surface.
> **Notice:** The name will be set only if the specified surface was added via the *[addSurface()()](../../../api/library/objects/class.objectmeshdynamic_usc.md#addSurface_cstr_void)* method.


### Arguments

- *string* **name** - New name of the surface.
- *int* **surface** - Number of a target surface in range from **0** to the total number of surfaces.

## void setTangent ( int num , quat tangent )

Sets the new tangent vector for the given vertex.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.
- *quat* **tangent** - Tangent vector to be set.

## quat getTangent ( int num )

Returns the tangent vector of the given vertex.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.

### Return value

Tangent vector.
## void setTexCoord ( int num , vec4 texcoord )

Updates texture coordinates of a given vertex.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.
- *vec4* **texcoord** - New coordinate pairs for both texture channels.

## vec4 getTexCoord ( int num )

Returns texture coordinates of a given vertex.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.

### Return value

Coordinate pairs for both texture channels.
## void setVertex ( int num , vec3 xyz )

Updates coordinates of a given vertex.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.
- *vec3* **xyz** - New coordinates in the mesh system of coordinates.

## vec3 getVertex ( int num )

Returns coordinates of a given vertex.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.

### Return value

Coordinates in the mesh system of coordinates.
## void setVertexArray ( )

Updates the vertex array of the dynamic mesh.
### Arguments

## int isFlushed ( )

Returns a value indicating if vertex data of the mesh was flushed (create/upload operation) to video memory.
### Return value

**1** if vertex data of the mesh was flushed (create/upload operation) to video memory; otherwise, **0**.
## void addColor ( vec4 color )

Adds a color to the last added vertex.
### Arguments

- *vec4* **color** - Color.

## void addIndex ( int index )

Adds an index to the index buffer.
### Arguments

- *int* **index** - Index to add.

## void addSurface ( string name )

Adds all the last listed and unsigned vertices and triangles to a new surface with a specified name.
> **Notice:** For your convenience, *[ObjectMeshDynamic()()](../../../api/library/objects/class.objectmeshdynamic_usc.md#ObjectMeshDynamic_constPtrMesh_int)* initializes the object with one internal surface named "`dynamic`". The first call to *[addSurface()()](../../../api/library/objects/class.objectmeshdynamic_usc.md#addSurface_cstr_void)* simply assigns a user-defined name to this surface and does not change the total number of surfaces (any geometry created before the call, if any, is preserved). Subsequent calls create additional surfaces as needed.


### Arguments

- *string* **name** - Name of the new surface.

## void addTangent ( quat tangent )

Appends the given tangent to the last added vertex.
### Arguments

- *quat* **tangent** - Tangent to add.

## void addTexCoord ( vec4 texcoord )

Adds texture coordinates to the last added vertex.
### Arguments

- *vec4* **texcoord** - Coordinate pairs for both texture channels.

## void addTriangleFan ( int num_vertex )

Adds a triangle fan to the mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with [*addVertex()*](#addVertex_vec3_void). Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_vertex** - Number of vertices comprising the fan.

## void addTriangleQuads ( int num_quads )

Adds a given number of quadrilaterals to the mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with the [addVertex()](#addVertex_vec3_void) function. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_quads** - Number of quadrilaterals to add.

## void addTriangles ( int num_triangles )

Adds a given number of triangles to the mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with [*addVertex()*](#addVertex_vec3_void).Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_triangles** - Number of triangles.

## void addTriangleStrip ( int num_vertex )

Adds a triangle strip to the mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with [*addVertex()*](#addVertex_vec3_void). Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_vertex** - Number of vertices comprising the strip.

## void addVertex ( vec3 xyz )

Adds a vertex with given coordinates to the mesh.
### Arguments

- *vec3* **xyz** - Vertex coordinates in the mesh system of coordinates.

## void addVertexArray ( )

Adds an array of vertices to the dynamic mesh.
### Arguments

## void allocateIndices ( int num )

Allocate an index buffer for a given number of indices that will be used for a mesh. With this function, memory can be allocated once rather than in chunks, making the creation faster.
### Arguments

- *int* **num** - The number of indices that will be stored in a buffer.

## void allocateVertex ( int num )

Allocate a vertex buffer for a given number of vertices that will be used for a mesh. With this function, memory can be allocated once rather than in chunks, making the creation faster.
### Arguments

- *int* **num** - The number of vertices that will be stored in a buffer.

## void clearIndices ( )

Clears all vertex indices used by the mesh.
## void clearSurfaces ( )

Clears all the surface settings.
## void clearVertex ( )

Clears all vertices comprising the mesh.
## void flushIndices ( )

 Flushes the index buffer and sends data to the GPU. This function is called automatically, if the length of the index buffer changes. If you change the content of the index buffer, you should call this method.
## void flushVertex ( )

 Flushes the vertex buffer and sends data to the GPU. This function is called automatically, if the length of the vertex buffer changes. If you change the content of the vertex buffer, you should call this method.
## int loadMesh ( string path )

Loads a mesh for the current mesh from the file. This function doesn't change the mesh name.
### Arguments

- *string* **path** - Mesh file name.

### Return value

**1** if the mesh is loaded successfully; otherwise, **0**.
## void removeIndices ( int num , int size )

Removes the specified number of indices starting from the given index.
### Arguments

- *int* **num** - Number of the index in the index buffer.
- *int* **size** - Number of indices to remove.

## void removeSurface ( int surface )

Removes the surface with the given index.
### Arguments

- *int* **surface** - Surface index.

## void removeSurfaces ( string name )

Removes surfaces with the given name.
### Arguments

- *string* **name** - Surface name.

## void removeVertex ( int num , int size , int indices )

Removes the specified number of vertices starting from the given vertex. To fix the index buffer after removal of vertices, pass true as the 3rd argument.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.
- *int* **size** - Number of vertices to remove.
- *int* **indices** - 1 to fix the index buffer after removal of vertices; otherwise, 0.

## int saveMesh ( string path )

Saves the dynamic mesh into `.mesh` or `.anim` format.
### Arguments

- *string* **path** - Mesh file name.

### Return value

**1** if the mesh is saved successfully; otherwise, **0**.
## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_usc.md) type identifier.
## int updateBounds ( )

Calculates a bounding box and a bounding sphere for the current mesh.
### Return value

**1** if the bounds are calculated successfully; otherwise, **0**.
## int updateIndices ( )

Updates vertex and index buffers by removing duplicated vertices and rearranging the indices of the created mesh to optimize it for faster rendering.
### Return value

**1** if the indices are updated successfully; otherwise, **0**.
## void updateSurfaceBegin ( int surface )

Synchronizes surface begin index.
### Arguments

- *int* **surface** - ID of a target surface.

## void updateSurfaceEnd ( int surface )

Synchronizes surface end index.
### Arguments

- *int* **surface** - ID of a target surface.

## int updateTangents ( )

Updates tangent vectors of the mesh vertices.
### Return value

**1** if the tangents are updated successfully; otherwise, **0**.
## void putUniqueMesh ( )

Makes the mesh used by the object unique (different from the one shared by other Dynamic Mesh objects in the world by default).
