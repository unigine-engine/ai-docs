# Unigine.MeshDynamic Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to procedurally create dynamic meshes (i.e. triangles, lines or points) and modify them at run time.


## MeshDynamic Class

### Members

## void setFlags ( int flags )

Sets a new set of flags of the dynamic mesh.
> **Notice:** The [USAGE_IMMUTABLE_VERTEX](#USAGE_IMMUTABLE_VERTEX) flag cannot be used together with [USAGE_DYNAMIC_VERTEX](#USAGE_DYNAMIC_VERTEX) flag.
>
>
> The [USAGE_IMMUTABLE_INDICES](#USAGE_IMMUTABLE_INDICES) flag cannot be used together with [USAGE_DYNAMIC_INDICES](#USAGE_DYNAMIC_INDICES) flag.
>
>
> [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) can be used only together with [USAGE_IMMUTABLE_ALL](#USAGE_IMMUTABLE_ALL).


### Arguments

- *int* **flags** - The creation flags. A combination of [MESH_DYNAMIC_USAGE_IMMUTABLE_*](#USAGE_IMMUTABLE_VERTEX), [MESH_DYNAMIC_USAGE_DYNAMIC_*](#USAGE_DYNAMIC_VERTEX) and [MESH_DYNAMIC_USAGE_FLUSH_*](#USAGE_FLUSH_VERTEX) flags.

## int getFlags () const

Returns the current set of flags of the dynamic mesh.
> **Notice:** The [USAGE_IMMUTABLE_VERTEX](#USAGE_IMMUTABLE_VERTEX) flag cannot be used together with [USAGE_DYNAMIC_VERTEX](#USAGE_DYNAMIC_VERTEX) flag.
>
>
> The [USAGE_IMMUTABLE_INDICES](#USAGE_IMMUTABLE_INDICES) flag cannot be used together with [USAGE_DYNAMIC_INDICES](#USAGE_DYNAMIC_INDICES) flag.
>
>
> [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) can be used only together with [USAGE_IMMUTABLE_ALL](#USAGE_IMMUTABLE_ALL).


### Return value

Current creation flags. A combination of [MESH_DYNAMIC_USAGE_IMMUTABLE_*](#USAGE_IMMUTABLE_VERTEX), [MESH_DYNAMIC_USAGE_DYNAMIC_*](#USAGE_DYNAMIC_VERTEX) and [MESH_DYNAMIC_USAGE_FLUSH_*](#USAGE_FLUSH_VERTEX) flags.
## bool isUsageShared () const

Returns the current value indicating if Mesh Dynamic has the [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) flag enabled.
### Return value

**true** if the [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) flag for Mesh Dynamic is enabled ; otherwise **false**.
---

## static MeshDynamic ( int flags )


Creates a new dynamic mesh in accordance with the specified flags.


> **Notice:** The [USAGE_IMMUTABLE_VERTEX](#USAGE_IMMUTABLE_VERTEX) flag cannot be used together with [USAGE_DYNAMIC_VERTEX](#USAGE_DYNAMIC_VERTEX) flag.
>
>
> The [USAGE_IMMUTABLE_INDICES](#USAGE_IMMUTABLE_INDICES) flag cannot be used together with [USAGE_DYNAMIC_INDICES](#USAGE_DYNAMIC_INDICES) flag.
>
>
> [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) can be used only together with [USAGE_IMMUTABLE_ALL](#USAGE_IMMUTABLE_ALL).


### Arguments

- *int* **flags** - Creation flags. A combination of [MESH_DYNAMIC_USAGE_IMMUTABLE_*](#USAGE_IMMUTABLE_VERTEX), [MESH_DYNAMIC_USAGE_DYNAMIC_*](#USAGE_DYNAMIC_VERTEX) and [MESH_DYNAMIC_USAGE_FLUSH_*](#USAGE_FLUSH_VERTEX) flags.

## MeshDynamic create ( int flags )


Creates a new dynamic mesh instance in accordance with the specified flags.


> **Notice:** The [USAGE_IMMUTABLE_VERTEX](#USAGE_IMMUTABLE_VERTEX) flag cannot be used together with [USAGE_DYNAMIC_VERTEX](#USAGE_DYNAMIC_VERTEX) flag.
>
>
> The [USAGE_IMMUTABLE_INDICES](#USAGE_IMMUTABLE_INDICES) flag cannot be used together with [USAGE_DYNAMIC_INDICES](#USAGE_DYNAMIC_INDICES) flag.
>
>
> [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) can be used only together with [USAGE_IMMUTABLE_ALL](#USAGE_IMMUTABLE_ALL).


### Arguments

- *int* **flags** - Creation flags. A combination of [MESH_DYNAMIC_USAGE_IMMUTABLE_*](#USAGE_IMMUTABLE_VERTEX), [MESH_DYNAMIC_USAGE_DYNAMIC_*](#USAGE_DYNAMIC_VERTEX) and [MESH_DYNAMIC_USAGE_FLUSH_*](#USAGE_FLUSH_VERTEX) flags.

### Return value

New MeshDynamic instance.
## int copy ( MeshDynamic dest )

Copies the dynamic mesh to the specified target.
### Arguments

- *[MeshDynamic](../../../api/library/rendering/class.meshdynamic_usc.md)* **dest** - Target dynamic mesh to which the mesh is to be copied.

### Return value

**1** if the dynamic mesh is copied successfully to the specified target; otherwise, **0**.
## void bind ( )

Binds dynamic mesh data (index and vertex buffers) to the input assembler stage.
## void unbind ( )

Unbinds dynamic mesh data (index and vertex buffers).
## void flushVertex ( )

Flushes the vertex buffer and sends all data to GPU. This method is called automatically, if the length of the vertex buffer changes. If you change the contents of the vertex buffer, you should call this method.
## void flushIndices ( )

Flushes the index buffer and sends all data to GPU. This method is called automatically, if the length of the index buffer changes. If you change the contents of the index buffers, you should call this method.
## int renderSurface ( int mode )

Renders the surface.
### Arguments

- *int* **mode** - Rendering mode. One of the [MESH_DYNAMIC_MODE_*](#MODE_POINTS) values.

### Return value

Number of primitives rendered. Primitive type is determined by the rendering mode.
## int renderInstancedSurface ( int mode , int num )

Renders the specified number of instances of the surface.
### Arguments

- *int* **mode** - Rendering mode. One of the [MESH_DYNAMIC_MODE_*](#MODE_POINTS) values.
- *int* **num** - Number of instances to be rendered.

### Return value

Number of primitives rendered. Primitive type is determined by the rendering mode.
## int renderSurface ( int mode , int base , int begin , int end )

Renders the surface specified by begin and end indices.
### Arguments

- *int* **mode** - Rendering mode. One of the [MESH_DYNAMIC_MODE_*](#MODE_POINTS) values.
- *int* **base** - A value added to each index before reading a vertex from the vertex buffer.
- *int* **begin** - First index of the surface to be read by the GPU from the index buffer.
- *int* **end** - Last index of the surface to be read by the GPU from the index buffer.

### Return value

Number of primitives rendered. Primitive type is determined by the rendering mode.
## int renderInstancedSurface ( int mode , int base , int begin , int end , int num )

Renders the specified number of instances of the surface specified by begin and end indices.
### Arguments

- *int* **mode** - Rendering mode. One of the [MESH_DYNAMIC_MODE_*](#MODE_POINTS) values.
- *int* **base** - A value added to each index before reading a vertex from the vertex buffer.
- *int* **begin** - First index of the surface to be read by the GPU from the index buffer.
- *int* **end** - Last index of the surface to be read by the GPU from the index buffer.
- *int* **num** - Number of instances to be rendered.

### Return value

Number of primitives rendered. Primitive type is determined by the rendering mode.
## int render ( int mode , int flush )

Renders the dynamic mesh with the specified flags and mode.
### Arguments

- *int* **mode** - Rendering mode. One of the [MESH_DYNAMIC_MODE_*](#MODE_POINTS) values.
- *int* **flush** - Flush flag. One of the [MESH_DYNAMIC_USAGE_FLUSH_*](#USAGE_FLUSH_VERTEX) variables.

### Return value

Number of triangles rendered.
## int getSystemMemoryUsage ( )

Returns the current amount of system memory used by the dynamic mesh, in bytes.
### Return value

System memory amount used by the dynamic mesh, in bytes.
## int getVideoMemoryUsage ( )

Returns the current amount of video memory used by the dynamic mesh.
### Return value

Video memory amount used by the dynamic mesh, in bytes.
## void setVertexFormat ( Attribute[] attributes )

Sets vertex format to be used by the dynamic mesh.
### Arguments

- *Attribute[]* **attributes** - Array of attributes to be used for vertex format, can be up to 16 attributes for one vertex. The numeration starts from **0**. Each attribute consists of:

  - An offset of the vertex in bytes, depends on the vertex type and size.
  - Type of the vertex: [MESH_DYNAMIC_TYPE_FLOAT](#TYPE_FLOAT), [MESH_DYNAMIC_TYPE_HALF](#TYPE_HALF), [MESH_DYNAMIC_TYPE_UCHAR](#TYPE_UCHAR), [MESH_DYNAMIC_TYPE_USHORT](#TYPE_USHORT)
  - Size of the vertex: can be **1,2,3,4** for *float* type; **2,4** for *half* type; **4** for *UChar* type > **Notice:** When it goes to shader, **0** -attribute always comes with the size of **4**, no matter what size is specified in the method. All the other attributes come with the specified sizes.

## int getVertexSize ( )

Returns vertex size of the dynamic mesh.
### Return value

Vertex size.
## int getNumAttributes ( )

Returns the number of vertex attributes of the dynamic mesh.
## void clearVertex ( )

Removes all dynamic mesh vertices.
## void allocateVertex ( int num )

Allocates a given number of vertices in the vertex buffer. With this function, memory can be allocated once rather than in chunks, making the creation faster.
### Arguments

- *int* **num** - Number of vertices for which memory is to be allocated.

## void removeVertex ( int num , int size )

Removes the specified number of elements starting from the specified one from the vertex buffer of the dynamic mesh.
### Arguments

- *int* **num** - Number of the first vertex to be removed.
- *int* **size** - Number of vertices to be removed.

## void setNumVertex ( int num )

Sets the total number of vertices for the dynamic mesh.
### Arguments

- *int* **num** - New number of vertices.

## int getNumVertex ( )

Returns the total number of vertices for the dynamic mesh.
## void addVertexHalf1 ( int attribute , float x )

Adds a new vertex with a single half coordinate to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.

## void addVertexHalf2 ( int attribute , float x , float y )

Adds a new vertex with 2 half coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.

## void addVertexHalf3 ( int attribute , float x , float y , float z )

Adds a new vertex with 3 half coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.

## void addVertexHalf4 ( int attribute , float x , float y , float z , float w )

Adds a new vertex with 4 half coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.
- *float* **w** - W coordinate of the vertex.

## void addVertexFloat1 ( int attribute , float x )

Adds a new vertex with a single float coordinate to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.

## void addVertexFloat2 ( int attribute , float x , float y )

Adds a new vertex with 2 float coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.

## void addVertexFloat3 ( int attribute , float x , float y , float z )

Adds a new vertex with 3 float coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.

## void addVertexFloat4 ( int attribute , float x , float y , float z , float w )

Adds a new vertex with 4 float coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.
- *float* **w** - W coordinate of the vertex.

## void addVertexUChar1 ( int attribute , int x )

Adds a new vertex with a single unsigned char coordinate to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.

## void addVertexUChar2 ( int attribute , int x , int y )

Adds a new vertex with 2 unsigned char coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.

## void addVertexUChar3 ( int attribute , int x , int y , int z )

Adds a new vertex with 3 unsigned char coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.
- *int* **z** - Z coordinate of the vertex.

## void addVertexUChar4 ( int attribute , int x , int y , int z , int w )

Adds a new vertex with 4 unsigned char coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.
- *int* **z** - Z coordinate of the vertex.
- *int* **w** - W coordinate of the vertex.

## void addVertexUShort1 ( int attribute , int x )

Adds a new vertex with a single unsigned short coordinate to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.

## void addVertexUShort2 ( int attribute , int x , int y )

Adds a new vertex with 2 unsigned short coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.

## void addVertexUShort3 ( int attribute , int x , int y , int z )

Adds a new vertex with 3 unsigned short coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.
- *int* **z** - Z coordinate of the vertex.

## void addVertexUShort4 ( int attribute , int x , int y , int z , int w )

Adds a new vertex with 4 unsigned short coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.
- *int* **z** - Z coordinate of the vertex.
- *int* **w** - W coordinate of the vertex.

## void setVertexHalf1 ( int attribute , float x )

Sets half-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.

## void setVertexHalf2 ( int attribute , float x , float y )

Sets half-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.

## void setVertexHalf3 ( int attribute , float x , float y , float z )

Sets half-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.

## void setVertexHalf4 ( int attribute , float x , float y , float z , float w )

Sets half-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.
- *float* **w** - W coordinate of the vertex.

## void setVertexFloat1 ( int attribute , float x )

Sets float-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.

## void setVertexFloat2 ( int attribute , float x , float y )

Sets float-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.

## void setVertexFloat3 ( int attribute , float x , float y , float z )

Sets float-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.

## void setVertexFloat4 ( int attribute , float x , float y , float z , float w )

Sets float-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.
- *float* **w** - W coordinate of the vertex.

## void setVertexUChar1 ( int attribute , int x )

Sets uchar-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.

## void setVertexUChar2 ( int attribute , int x , int y )

Sets uchar-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.

## void setVertexUChar3 ( int attribute , int x , int y , int z )

Sets uchar-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.
- *int* **z** - Z coordinate of the vertex.

## void setVertexUChar4 ( int attribute , int x , int y , int z , int w )

Sets uchar-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.
- *int* **z** - Z coordinate of the vertex.
- *int* **w** - W coordinate of the vertex.

## void setVertexUShort1 ( int attribute , int x )

Sets ushort-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.

## void setVertexUShort2 ( int attribute , int x , int y )

Sets ushort-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.

## void setVertexUShort3 ( int attribute , int x , int y , int z )

Sets ushort-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.
- *int* **z** - Z coordinate of the vertex.

## void setVertexUShort4 ( int attribute , int x , int y , int z , int w )

Sets ushort-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.
- *int* **z** - Z coordinate of the vertex.
- *int* **w** - W coordinate of the vertex.

## void setVertexHalf1 ( int vertex , int attribute , float x )

Sets half-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.

## void setVertexHalf2 ( int vertex , int attribute , float x , float y )

Sets half-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.

## void setVertexHalf3 ( int vertex , int attribute , float x , float y , float z )

Sets half-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.

## void setVertexHalf4 ( int vertex , int attribute , float x , float y , float z , float w )

Sets half-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.
- *float* **w** - W coordinate of the vertex.

## void setVertexFloat1 ( int vertex , int attribute , float x )

Sets float-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.

## void setVertexFloat2 ( int vertex , int attribute , float x , float y )

Sets float-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.

## void setVertexFloat3 ( int vertex , int attribute , float x , float y , float z )

Sets float-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.

## void setVertexFloat4 ( int vertex , int attribute , float x , float y , float z , float w )

Sets float-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.
- *float* **w** - W coordinate of the vertex.

## void setVertexUChar1 ( int vertex , int attribute , int x )

Sets uchar-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.

## void setVertexUChar2 ( int vertex , int attribute , int x , int y )

Sets uchar-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.

## void setVertexUChar3 ( int vertex , int attribute , int x , int y , int z )

Sets uchar-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.
- *int* **z** - Z coordinate of the vertex.

## void setVertexUChar4 ( int vertex , int attribute , int x , int y , int z , int w )

Sets uchar-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.
- *int* **z** - Z coordinate of the vertex.
- *int* **w** - W coordinate of the vertex.

## void setVertexUShort1 ( int vertex , int attribute , int x )

Sets ushort-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.

## void setVertexUShort2 ( int vertex , int attribute , int x , int y )

Sets ushort-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.

## void setVertexUShort3 ( int vertex , int attribute , int x , int y , int z )

Sets ushort-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.
- *int* **z** - Z coordinate of the vertex.

## void setVertexUShort4 ( int vertex , int attribute , int x , int y , int z , int w )

Sets ushort-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *int* **x** - X coordinate of the vertex.
- *int* **y** - Y coordinate of the vertex.
- *int* **z** - Z coordinate of the vertex.
- *int* **w** - W coordinate of the vertex.

## void clearIndices ( )

Removes all indices of the dynamic mesh.
## void allocateIndices ( int num )

Allocates a given number of vertex indices in the index buffer. With this function, memory can be allocated once rather than in chunks, making the creation faster.
### Arguments

- *int* **num** - Number of indices for which memory is to be allocated.

## void removeIndices ( int num , int size )

Removes the specified number of indices starting from the specified one from the index buffer of the dynamic mesh.
### Arguments

- *int* **num** - Number of the first index to be removed.
- *int* **size** - Number of indices to be removed.

## void setNumIndices ( int num )

Sets the total number of indices for the dynamic mesh.
### Arguments

- *int* **num** - New number of indices.

## int getNumIndices ( )

Returns the total number of indices for the dynamic mesh.
### Return value

Number of indices.
## void addIndex ( int index )

Adds a new index to the index buffer of the dynamic mesh.
### Arguments

- *int* **index** - Index to be added.

## void addIndexFast ( int index )

Adds a new index to the index buffer of the dynamic mesh.
### Arguments

- *int* **index** - Index to be added.

## void addIndices ( int i0 , int i1 )

Adds two new indices to the index buffer of the dynamic mesh at once. This method can be used to add indices for a line strips via a single function call.
### Arguments

- *int* **i0** - First index to be added.
- *int* **i1** - Second index to be added.

## void addIndices ( int i0 , int i1 , int i2 )

Adds three new indices to the index buffer of the dynamic mesh at once. This method can be used to add indices for a triangle via a single function call.
### Arguments

- *int* **i0** - First index to be added.
- *int* **i1** - Second index to be added.
- *int* **i2** - Third index to be added.

## void addIndices ( int i0 , int i1 , int i2 , int i3 )

Adds four new indices to the index buffer of the dynamic mesh at once. This method can be used to add indices for a quad via a single function call.
### Arguments

- *int* **i0** - First index to be added.
- *int* **i1** - Second index to be added.
- *int* **i2** - Third index to be added.
- *int* **i3** - Fourth index to be added.

## void addPoints ( int num_points )

Adds the specified number of points to the dynamic mesh.
### Arguments

- *int* **num_points** - Number of points to be added.

## void addLineStrip ( int num_vertex )

Adds a line strip to the dynamic mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with one of the [*addVertex*()*](#addVertexHalf1_int_float_void) methods. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_vertex** - Number of vertices comprising the strip.

## void addTriangles ( int num_triangles )

Adds the specified number of triangles to the dynamic mesh.
### Arguments

- *int* **num_triangles** - Number of triangles to be added.

## void addTriangleFan ( int num_vertex )

Adds a triangle fan to the dynamic mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with one of the [*addVertex*()*](#addVertexHalf1_int_float_void) methods. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_vertex** - Number of vertices comprising the fan.

## void addTriangleStrip ( int num_vertex )

Adds a triangle strip to the dynamic mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with one of the [*addVertex*()*](#addVertexHalf1_int_float_void) methods. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_vertex** - Number of vertices comprising the strip.

## void addTriangleQuads ( int num_quads )

Adds a given number of quadrilaterals to the dynamic mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with one of the [*addVertex*()*](#addVertexHalf1_int_float_void) methods. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_quads** - Number of quadrilaterals to be added.

## int saveState ( Stream stream )


Saves the current state of the dynamic mesh (vertices, indices, etc.) to the specified stream.


Saving into the stream requires creating a blob to save into. To restore the saved state the [restoreState()](#restoreState_Stream_int) method is used:


```cpp
// initialize a mesh and set its state
//...//

// save state
Blob blob_state = new Blob();
dynamicMesh.saveState(blob_state);

// change state
//...//

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
dynamicMesh.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream to which the state of the dynamic mesh is to be saved.

### Return value

**1** if the current state of the dynamic mesh is saved successfully; otherwise, **0**.
## int restoreState ( Stream stream )


Restores a previously saved state of the dynamic mesh (vertices, indices, etc.) from the specified stream.


Restoring from the stream requires creating a blob to save into and saving the state using the [saveState()](#saveState_Stream_int) method:


```cpp
// initialize a mesh and set its state
//...//

// save state
Blob blob_state = new Blob();
dynamicMesh.saveState(blob_state);

// change state
//...//

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
dynamicMesh.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream from which the previously saved state of the dynamic mesh is to be loaded.

### Return value

**1** if a previously saved state of the dynamic mesh is restored successfully; otherwise, **0**.
