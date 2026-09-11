# Unigine.MeshDynamic Class (CS)


This class is used to procedurally create dynamic meshes (i.e. triangles, lines or points) and modify them at run time.


## MeshDynamic Class

### Enums

## BUFFER

| Name | Description |
|---|---|
| **USAGE_IMMUTABLE_VERTEX** = 1 << 0 | Vertex buffer will be created in GPU memory as an unmodifiable resource. |
| **USAGE_IMMUTABLE_INDICES** = 1 << 1 | Index buffer will be created in GPU memory as an unmodifiable resource. |
| **USAGE_IMMUTABLE_ALL** = (USAGE_IMMUTABLE_VERTEX \| USAGE_IMMUTABLE_INDICES) | Vertex and index buffers will be created in GPU memory as unmodifiable resources. |
| **USAGE_DYNAMIC_VERTEX** = 1 << 2 | Vertex buffer will be created in GPU memory as a dynamic resource. |
| **USAGE_DYNAMIC_INDICES** = 1 << 3 | Index buffer will be created in GPU memory as a dynamic resource. |
| **USAGE_DYNAMIC_ALL** = (USAGE_DYNAMIC_VERTEX \| USAGE_DYNAMIC_INDICES) | Vertex and index buffers will be created in GPU memory as dynamic resources. |
| **USAGE_FLUSH_VERTEX** = 1 << 4 | Data on updated vertices will be sent from CPU to GPU. |
| **USAGE_FLUSH_INDICES** = 1 << 5 | Data on updated indices will be sent from CPU to GPU. |
| **USAGE_FLUSH_ALL** = (USAGE_FLUSH_VERTEX \| USAGE_FLUSH_INDICES) | Data on updated vertices and indices will be sent from CPU to GPU. |
| **USAGE_MISC_SHARED** = 1 << 6 | Data is accessible by an external graphics API (applicable for DX12 and Vulkan only). |

## TYPE

| Name | Description |
|---|---|
| **TYPE_HALF** = 0 | Half-precision floating-point data type. |
| **TYPE_FLOAT** = 1 | Floating-point data type. |
| **TYPE_UCHAR** = 2 | Unsigned character data type. |
| **TYPE_USHORT** = 3 | Unsigned short data type. |
| **NUM_TYPES** = 4 | Number of data types. |

## MODE

| Name | Description |
|---|---|
| **MODE_POINTS** = 0 | Mode to render the points. |
| **MODE_LINES** = 1 | Mode to render the lines. |
| **MODE_TRIANGLES** = 2 | Mode to render the triangles. |
| **MODE_TRIANGLE_PATCHES** = 3 | Mode to render the triangle patches. |
| **MODE_QUAD_PATCHES** = 4 | Mode to render the quad patches. |
| **NUM_MODES** = 5 | Number of rendering modes. |

### Properties

## int Flags

The set of flags of the dynamic mesh.
> **Notice:** The [USAGE_IMMUTABLE_VERTEX](#USAGE_IMMUTABLE_VERTEX) flag cannot be used together with [USAGE_DYNAMIC_VERTEX](#USAGE_DYNAMIC_VERTEX) flag.
>
>
> The [USAGE_IMMUTABLE_INDICES](#USAGE_IMMUTABLE_INDICES) flag cannot be used together with [USAGE_DYNAMIC_INDICES](#USAGE_DYNAMIC_INDICES) flag.
>
>
> [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) can be used only together with [USAGE_IMMUTABLE_ALL](#USAGE_IMMUTABLE_ALL).


## 🔒︎ bool IsUsageShared

The value indicating if Mesh Dynamic has the [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) flag enabled.
### Members

---

## MeshDynamic ( int flags )


Creates a new dynamic mesh in accordance with the specified flags.


> **Notice:** The [USAGE_IMMUTABLE_VERTEX](#USAGE_IMMUTABLE_VERTEX) flag cannot be used together with [USAGE_DYNAMIC_VERTEX](#USAGE_DYNAMIC_VERTEX) flag.
>
>
> The [USAGE_IMMUTABLE_INDICES](#USAGE_IMMUTABLE_INDICES) flag cannot be used together with [USAGE_DYNAMIC_INDICES](#USAGE_DYNAMIC_INDICES) flag.
>
>
> [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) can be used only together with [USAGE_IMMUTABLE_ALL](#USAGE_IMMUTABLE_ALL).


### Arguments

- *int* **flags** - Creation flags. A combination of [USAGE_IMMUTABLE_*](#USAGE_IMMUTABLE_VERTEX), [USAGE_DYNAMIC_*](#USAGE_DYNAMIC_VERTEX) and [USAGE_FLUSH_*](#USAGE_FLUSH_VERTEX) flags.

## MeshDynamic Create ( int flags )


Creates a new dynamic mesh instance in accordance with the specified flags.


> **Notice:** The [USAGE_IMMUTABLE_VERTEX](#USAGE_IMMUTABLE_VERTEX) flag cannot be used together with [USAGE_DYNAMIC_VERTEX](#USAGE_DYNAMIC_VERTEX) flag.
>
>
> The [USAGE_IMMUTABLE_INDICES](#USAGE_IMMUTABLE_INDICES) flag cannot be used together with [USAGE_DYNAMIC_INDICES](#USAGE_DYNAMIC_INDICES) flag.
>
>
> [USAGE_MISC_SHARED](#USAGE_MISC_SHARED) can be used only together with [USAGE_IMMUTABLE_ALL](#USAGE_IMMUTABLE_ALL).


### Arguments

- *int* **flags** - Creation flags. A combination of [USAGE_IMMUTABLE_*](#USAGE_IMMUTABLE_VERTEX), [USAGE_DYNAMIC_*](#USAGE_DYNAMIC_VERTEX) and [USAGE_FLUSH_*](#USAGE_FLUSH_VERTEX) flags.

### Return value

New MeshDynamic instance.
## bool Copy ( MeshDynamic dest )

Copies the dynamic mesh to the specified target.
### Arguments

- *[MeshDynamic](../../../api/library/rendering/class.meshdynamic_cs.md)* **dest** - Target dynamic mesh to which the mesh is to be copied.

### Return value

true if the dynamic mesh is copied successfully to the specified target; otherwise, false.
## void Bind ( )

Binds dynamic mesh data (index and vertex buffers) to the input assembler stage.
## void Unbind ( )

Unbinds dynamic mesh data (index and vertex buffers).
## void FlushVertex ( )

Flushes the vertex buffer and sends all data to GPU. This method is called automatically, if the length of the vertex buffer changes. If you change the contents of the vertex buffer, you should call this method.
## void FlushIndices ( )

Flushes the index buffer and sends all data to GPU. This method is called automatically, if the length of the index buffer changes. If you change the contents of the index buffers, you should call this method.
## int RenderSurface ( int mode )

Renders the surface.
### Arguments

- *int* **mode** - Rendering mode. One of the [MODE](#MODE) values.

### Return value

Number of primitives rendered. Primitive type is determined by the rendering mode.
## int RenderInstancedSurface ( int mode , int num )

Renders the specified number of instances of the surface.
### Arguments

- *int* **mode** - Rendering mode. One of the [MODE](#MODE) values.
- *int* **num** - Number of instances to be rendered.

### Return value

Number of primitives rendered. Primitive type is determined by the rendering mode.
## int RenderSurface ( int mode , int base , int begin , int end )

Renders the surface specified by begin and end indices.
### Arguments

- *int* **mode** - Rendering mode. One of the [MODE](#MODE) values.
- *int* **base** - A value added to each index before reading a vertex from the vertex buffer.
- *int* **begin** - First index of the surface to be read by the GPU from the index buffer.
- *int* **end** - Last index of the surface to be read by the GPU from the index buffer.

### Return value

Number of primitives rendered. Primitive type is determined by the rendering mode.
## int RenderInstancedSurface ( int mode , int base , int begin , int end , int num )

Renders the specified number of instances of the surface specified by begin and end indices.
### Arguments

- *int* **mode** - Rendering mode. One of the [MODE](#MODE) values.
- *int* **base** - A value added to each index before reading a vertex from the vertex buffer.
- *int* **begin** - First index of the surface to be read by the GPU from the index buffer.
- *int* **end** - Last index of the surface to be read by the GPU from the index buffer.
- *int* **num** - Number of instances to be rendered.

### Return value

Number of primitives rendered. Primitive type is determined by the rendering mode.
## int Render ( int mode , int flush )

Renders the dynamic mesh with the specified flags and mode.
### Arguments

- *int* **mode** - Rendering mode. One of the [MODE](#MODE) values.
- *int* **flush** - Flush flag. One of the [USAGE_FLUSH_*](#USAGE_FLUSH_VERTEX) variables.

### Return value

Number of triangles rendered.
## ulong GetSystemMemoryUsage ( )

Returns the current amount of system memory used by the dynamic mesh, in bytes.
### Return value

System memory amount used by the dynamic mesh, in bytes.
## ulong GetVideoMemoryUsage ( )

Returns the current amount of video memory used by the dynamic mesh.
### Return value

Video memory amount used by the dynamic mesh, in bytes.
## void SetVertexFormat ( Attribute[] attributes )

Sets vertex format to be used by the dynamic mesh.
### Arguments

- *Attribute[]* **attributes** - Array of attributes to be used for vertex format, can be up to 16 attributes for one vertex. The numeration starts from **0**. Each attribute consists of:

  - An offset of the vertex in bytes, depends on the vertex type and size.
  - Type of the vertex: one of the [TYPE_*](#TYPE) values
  - Size of the vertex: can be **1,2,3,4** for *float* type; **2,4** for *half* type; **4** for *UChar* type > **Notice:** When it goes to shader, **0** -attribute always comes with the size of **4**, no matter what size is specified in the method. All the other attributes come with the specified sizes.

## int GetVertexSize ( )

Returns vertex size of the dynamic mesh.
### Return value

Vertex size.
## int GetNumAttributes ( )

Returns the number of vertex attributes of the dynamic mesh.
## void ClearVertex ( )

Removes all dynamic mesh vertices.
## void AllocateVertex ( int num )

Allocates a given number of vertices in the vertex buffer. With this function, memory can be allocated once rather than in chunks, making the creation faster.
### Arguments

- *int* **num** - Number of vertices for which memory is to be allocated.

## void RemoveVertex ( int num , int size )

Removes the specified number of elements starting from the specified one from the vertex buffer of the dynamic mesh.
### Arguments

- *int* **num** - Number of the first vertex to be removed.
- *int* **size** - Number of vertices to be removed.

## void SetNumVertex ( int num )

Sets the total number of vertices for the dynamic mesh.
### Arguments

- *int* **num** - New number of vertices.

## int GetNumVertex ( )

Returns the total number of vertices for the dynamic mesh.
## void AddVertexArray ( IntPtr vertex , int num_vertex )

Adds a set of new elements to the vertex buffer of the dynamic mesh at once.
### Arguments

- *IntPtr* **vertex** - Array of vertices to be added.
- *int* **num_vertex** - Number of vertices to add.

## void SetVertexArray ( IntPtr vertex , int num_vertex )

Replaces the current vertex buffer of the dynamic mesh with the specified array of vertices.
### Arguments

- *IntPtr* **vertex** - Array of vertices to be added.
- *int* **num_vertex** - Number of vertices to add.

## void AddVertexHalf1 ( int attribute , float x )

Adds a new vertex with a single half coordinate to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.

## void AddVertexHalf2 ( int attribute , float x , float y )

Adds a new vertex with 2 half coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.

## void AddVertexHalf3 ( int attribute , float x , float y , float z )

Adds a new vertex with 3 half coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.

## void AddVertexHalf4 ( int attribute , float x , float y , float z , float w )

Adds a new vertex with 4 half coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.
- *float* **w** - W coordinate of the vertex.

## void AddVertexFloat ( int attribute , float[] OUT_value )

Adds a new vertex with *float* coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float[]* **OUT_value** - Array of *float*-type coordinates of the vertex to be set. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void AddVertexFloat1 ( int attribute , float x )

Adds a new vertex with a single float coordinate to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.

## void AddVertexFloat2 ( int attribute , float x , float y )

Adds a new vertex with 2 float coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.

## void AddVertexFloat3 ( int attribute , float x , float y , float z )

Adds a new vertex with 3 float coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.

## void AddVertexFloat4 ( int attribute , float x , float y , float z , float w )

Adds a new vertex with 4 float coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.
- *float* **w** - W coordinate of the vertex.

## void AddVertexUChar ( int attribute , uchar[] OUT_value )

Adds a new vertex with *unsigned char* coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *uchar[]* **OUT_value** - Array of *uchar*-type coordinates of the vertex to be set. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void AddVertexUChar1 ( int attribute , byte x )

Adds a new vertex with a single unsigned char coordinate to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *byte* **x** - X coordinate of the vertex.

## void AddVertexUChar2 ( int attribute , byte x , byte y )

Adds a new vertex with 2 unsigned char coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *byte* **x** - X coordinate of the vertex.
- *byte* **y** - Y coordinate of the vertex.

## void AddVertexUChar3 ( int attribute , byte x , byte y , byte z )

Adds a new vertex with 3 unsigned char coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *byte* **x** - X coordinate of the vertex.
- *byte* **y** - Y coordinate of the vertex.
- *byte* **z** - Z coordinate of the vertex.

## void AddVertexUChar4 ( int attribute , byte x , byte y , byte z , byte w )

Adds a new vertex with 4 unsigned char coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *byte* **x** - X coordinate of the vertex.
- *byte* **y** - Y coordinate of the vertex.
- *byte* **z** - Z coordinate of the vertex.
- *byte* **w** - W coordinate of the vertex.

## void AddVertexUShort ( int attribute , ushort[] OUT_value )

Adds a new vertex with *unsigned short* coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *ushort[]* **OUT_value** - Array of *ushort*-type coordinates of the vertex to be set. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void AddVertexUShort1 ( int attribute , ushort x )

Adds a new vertex with a single unsigned short coordinate to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *ushort* **x** - X coordinate of the vertex.

## void AddVertexUShort2 ( int attribute , ushort x , ushort y )

Adds a new vertex with 2 unsigned short coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *ushort* **x** - X coordinate of the vertex.
- *ushort* **y** - Y coordinate of the vertex.

## void AddVertexUShort3 ( int attribute , ushort x , ushort y , ushort z )

Adds a new vertex with 3 unsigned short coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *ushort* **x** - X coordinate of the vertex.
- *ushort* **y** - Y coordinate of the vertex.
- *ushort* **z** - Z coordinate of the vertex.

## void AddVertexUShort4 ( int attribute , ushort x , ushort y , ushort z , ushort w )

Adds a new vertex with 4 unsigned short coordinates to the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *ushort* **x** - X coordinate of the vertex.
- *ushort* **y** - Y coordinate of the vertex.
- *ushort* **z** - Z coordinate of the vertex.
- *ushort* **w** - W coordinate of the vertex.

## void SetVertexHalf1 ( int attribute , float x )

Sets half-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.

## void SetVertexHalf2 ( int attribute , float x , float y )

Sets half-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.

## void SetVertexHalf3 ( int attribute , float x , float y , float z )

Sets half-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.

## void SetVertexHalf4 ( int attribute , float x , float y , float z , float w )

Sets half-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.
- *float* **w** - W coordinate of the vertex.

## void SetVertexFloat ( int attribute , float[] OUT_value )

Sets *float*-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float[]* **OUT_value** - Array of *float*-type coordinates to be set. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetVertexFloat1 ( int attribute , float x )

Sets float-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.

## void SetVertexFloat2 ( int attribute , float x , float y )

Sets float-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.

## void SetVertexFloat3 ( int attribute , float x , float y , float z )

Sets float-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.

## void SetVertexFloat4 ( int attribute , float x , float y , float z , float w )

Sets float-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.
- *float* **w** - W coordinate of the vertex.

## void SetVertexUChar ( int attribute , uchar[] OUT_value )

Sets *uchar*-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *uchar[]* **OUT_value** - Array of *uchar*-type coordinates to be set. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetVertexUChar1 ( int attribute , byte x )

Sets uchar-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *byte* **x** - X coordinate of the vertex.

## void SetVertexUChar2 ( int attribute , byte x , byte y )

Sets uchar-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *byte* **x** - X coordinate of the vertex.
- *byte* **y** - Y coordinate of the vertex.

## void SetVertexUChar3 ( int attribute , byte x , byte y , byte z )

Sets uchar-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *byte* **x** - X coordinate of the vertex.
- *byte* **y** - Y coordinate of the vertex.
- *byte* **z** - Z coordinate of the vertex.

## void SetVertexUChar4 ( int attribute , byte x , byte y , byte z , byte w )

Sets uchar-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *byte* **x** - X coordinate of the vertex.
- *byte* **y** - Y coordinate of the vertex.
- *byte* **z** - Z coordinate of the vertex.
- *byte* **w** - W coordinate of the vertex.

## void SetVertexUShort ( int attribute , ushort[] OUT_value )

Sets *ushort*-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *ushort[]* **OUT_value** - Array of *ushort*-type coordinates to be set. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetVertexUShort1 ( int attribute , ushort x )

Sets ushort-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *ushort* **x** - X coordinate of the vertex.

## void SetVertexUShort2 ( int attribute , ushort x , ushort y )

Sets ushort-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *ushort* **x** - X coordinate of the vertex.
- *ushort* **y** - Y coordinate of the vertex.

## void SetVertexUShort3 ( int attribute , ushort x , ushort y , ushort z )

Sets ushort-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *ushort* **x** - X coordinate of the vertex.
- *ushort* **y** - Y coordinate of the vertex.
- *ushort* **z** - Z coordinate of the vertex.

## void SetVertexUShort4 ( int attribute , ushort x , ushort y , ushort z , ushort w )

Sets ushort-type coordinates and specified attribute for the last vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **attribute** - Attribute to be set.
- *ushort* **x** - X coordinate of the vertex.
- *ushort* **y** - Y coordinate of the vertex.
- *ushort* **z** - Z coordinate of the vertex.
- *ushort* **w** - W coordinate of the vertex.

## void SetVertexHalf1 ( int vertex , int attribute , float x )

Sets half-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.

## void SetVertexHalf2 ( int vertex , int attribute , float x , float y )

Sets half-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.

## void SetVertexHalf3 ( int vertex , int attribute , float x , float y , float z )

Sets half-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.

## void SetVertexHalf4 ( int vertex , int attribute , float x , float y , float z , float w )

Sets half-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.
- *float* **w** - W coordinate of the vertex.

## void SetVertexFloat ( int vertex , int attribute , float[] OUT_value )

Sets *float*-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *float[]* **OUT_value** - Array of *float*-type coordinates to be set. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetVertexFloat1 ( int vertex , int attribute , float x )

Sets float-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.

## void SetVertexFloat2 ( int vertex , int attribute , float x , float y )

Sets float-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.

## void SetVertexFloat3 ( int vertex , int attribute , float x , float y , float z )

Sets float-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.

## void SetVertexFloat4 ( int vertex , int attribute , float x , float y , float z , float w )

Sets float-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.
- *float* **w** - W coordinate of the vertex.

## void SetVertexUChar ( int vertex , int attribute , uchar[] OUT_value )

Sets *uchar*-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *uchar[]* **OUT_value** - Array of *uchar*-type coordinates to be set. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetVertexUChar1 ( int vertex , int attribute , byte x )

Sets uchar-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *byte* **x** - X coordinate of the vertex.

## void SetVertexUChar2 ( int vertex , int attribute , byte x , byte y )

Sets uchar-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *byte* **x** - X coordinate of the vertex.
- *byte* **y** - Y coordinate of the vertex.

## void SetVertexUChar3 ( int vertex , int attribute , byte x , byte y , byte z )

Sets uchar-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *byte* **x** - X coordinate of the vertex.
- *byte* **y** - Y coordinate of the vertex.
- *byte* **z** - Z coordinate of the vertex.

## void SetVertexUChar4 ( int vertex , int attribute , byte x , byte y , byte z , byte w )

Sets uchar-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *byte* **x** - X coordinate of the vertex.
- *byte* **y** - Y coordinate of the vertex.
- *byte* **z** - Z coordinate of the vertex.
- *byte* **w** - W coordinate of the vertex.

## void SetVertexUShort ( int vertex , int attribute , ushort[] OUT_value )

Sets *ushort*-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *ushort[]* **OUT_value** - Array of *ushort*-type coordinates to be set. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetVertexUShort1 ( int vertex , int attribute , ushort x )

Sets ushort-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *ushort* **x** - X coordinate of the vertex.

## void SetVertexUShort2 ( int vertex , int attribute , ushort x , ushort y )

Sets ushort-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *ushort* **x** - X coordinate of the vertex.
- *ushort* **y** - Y coordinate of the vertex.

## void SetVertexUShort3 ( int vertex , int attribute , ushort x , ushort y , ushort z )

Sets ushort-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *ushort* **x** - X coordinate of the vertex.
- *ushort* **y** - Y coordinate of the vertex.
- *ushort* **z** - Z coordinate of the vertex.

## void SetVertexUShort4 ( int vertex , int attribute , ushort x , ushort y , ushort z , ushort w )

Sets ushort-type coordinates and specified attribute for the specified vertex in the vertex buffer of the dynamic mesh.
### Arguments

- *int* **vertex** - Vertex number.
- *int* **attribute** - Attribute to be set.
- *ushort* **x** - X coordinate of the vertex.
- *ushort* **y** - Y coordinate of the vertex.
- *ushort* **z** - Z coordinate of the vertex.
- *ushort* **w** - W coordinate of the vertex.

## void ClearIndices ( )

Removes all indices of the dynamic mesh.
## void AllocateIndices ( int num )

Allocates a given number of vertex indices in the index buffer. With this function, memory can be allocated once rather than in chunks, making the creation faster.
### Arguments

- *int* **num** - Number of indices for which memory is to be allocated.

## void RemoveIndices ( int num , int size )

Removes the specified number of indices starting from the specified one from the index buffer of the dynamic mesh.
### Arguments

- *int* **num** - Number of the first index to be removed.
- *int* **size** - Number of indices to be removed.

## void SetNumIndices ( int num )

Sets the total number of indices for the dynamic mesh.
### Arguments

- *int* **num** - New number of indices.

## int GetNumIndices ( )

Returns the total number of indices for the dynamic mesh.
### Return value

Number of indices.
## void AddIndex ( int index )

Adds a new index to the index buffer of the dynamic mesh.
### Arguments

- *int* **index** - Index to be added.

## void AddIndexFast ( int index )

Adds a new index to the index buffer of the dynamic mesh.
### Arguments

- *int* **index** - Index to be added.

## void AddIndices ( int i0 , int i1 )

Adds two new indices to the index buffer of the dynamic mesh at once. This method can be used to add indices for a line strips via a single function call.
### Arguments

- *int* **i0** - First index to be added.
- *int* **i1** - Second index to be added.

## void AddIndices ( int i0 , int i1 , int i2 )

Adds three new indices to the index buffer of the dynamic mesh at once. This method can be used to add indices for a triangle via a single function call.
### Arguments

- *int* **i0** - First index to be added.
- *int* **i1** - Second index to be added.
- *int* **i2** - Third index to be added.

## void AddIndices ( int i0 , int i1 , int i2 , int i3 )

Adds four new indices to the index buffer of the dynamic mesh at once. This method can be used to add indices for a quad via a single function call.
### Arguments

- *int* **i0** - First index to be added.
- *int* **i1** - Second index to be added.
- *int* **i2** - Third index to be added.
- *int* **i3** - Fourth index to be added.

## void AddIndicesArray ( int[] indices )

Adds a set of new elements to the index buffer of the dynamic mesh at once.
### Arguments

- *int[]* **indices** - Array of indices to be added.

## void SetIndicesArray ( int[] indices )

Replaces the current index buffer of the dynamic mesh with the specified array of indices.
### Arguments

- *int[]* **indices** - Array of indices to be set.

## void AddPoints ( int num_points )

Adds the specified number of points to the dynamic mesh.
### Arguments

- *int* **num_points** - Number of points to be added.

## void AddLineStrip ( int num_vertex )

Adds a line strip to the dynamic mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with one of the [*addVertex*()*](#addVertexHalf1_int_float_void) methods. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_vertex** - Number of vertices comprising the strip.

## void AddTriangles ( int num_triangles )

Adds the specified number of triangles to the dynamic mesh.
### Arguments

- *int* **num_triangles** - Number of triangles to be added.

## void AddTriangleFan ( int num_vertex )

Adds a triangle fan to the dynamic mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with one of the [*addVertex*()*](#addVertexHalf1_int_float_void) methods. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_vertex** - Number of vertices comprising the fan.

## void AddTriangleStrip ( int num_vertex )

Adds a triangle strip to the dynamic mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with one of the [*addVertex*()*](#addVertexHalf1_int_float_void) methods. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_vertex** - Number of vertices comprising the strip.

## void AddTriangleQuads ( int num_quads )

Adds a given number of quadrilaterals to the dynamic mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with one of the [*addVertex*()*](#addVertexHalf1_int_float_void) methods. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_quads** - Number of quadrilaterals to be added.

## int SaveState ( Stream stream )


Saves the current state of the dynamic mesh (vertices, indices, etc.) to the specified stream.


Saving into the stream requires creating a blob to save into. To restore the saved state the [RestoreState()](#restoreState_Stream_int) method is used:


```csharp
// initialize a mesh and set its state
//...//

// save state
Blob blob_state = new Blob();
dynamicMesh.SaveState(blob_state);

// change the state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
dynamicMesh.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream to which the state of the dynamic mesh is to be saved.

### Return value

true if the current state of the dynamic mesh is saved successfully; otherwise, false.
## int RestoreState ( Stream stream )


Restores a previously saved state of the dynamic mesh (vertices, indices, etc.) from the specified stream.


Restoring from the stream requires creating a blob to save into and saving the state using the [SaveState()](#saveState_Stream_int) method:


```csharp
// initialize a mesh and set its state
//...//

// save state
Blob blob_state = new Blob();
dynamicMesh.SaveState(blob_state);

// change the state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
dynamicMesh.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream from which the previously saved state of the dynamic mesh is to be loaded.

### Return value

true if a previously saved state of the dynamic mesh is restored successfully; otherwise, false.
