# ObjectDynamic Class (CS)

**Inherits from:** Object


ObjectDynamic class allows to create a dynamic object, which can be rendered by means of any type of geometry (vertex format for an object is changeable). The class supports instancing as well as point/line/triangle rendering modes. ObjectDynamic class requires a custom shader for rendering, no built-in shaders are available.


## ObjectDynamic Class

### Enums

## MODE

| Name | Description |
|---|---|
| **POINTS** = 0 | Mode to render the points. |
| **LINES** = 1 | Mode to render the lines. |
| **TRIANGLES** = 2 | Mode to render the triangles. |
| **TRIANGLE_PATCHES** = 3 | Mode to render the triangle patches. |
| **QUAD_PATCHES** = 4 | Mode to render the quad patches. |

### Properties

## int NumIndices

The number of vertex indices used by the object.
## int NumVertex

The number of vertices composing the object.
## 🔒︎ int NumAttributes

The number of vertex attributes.
## 🔒︎ int VertexSize

The size of the current vertex, bytes.
## bool Instancing

The value indicating if the hardware [instancing](../../../editor2/instancing_nodes/index.md) flag is enabled.
## Node.TYPE MaterialNodeType

The [node type](../../../api/library/nodes/class.node_cs.md) to be used by the renderer to determine which materials can be applied to the object. One of the [node type identifiers](../../../api/library/nodes/class.node_cs.md#DECAL_BEGIN).
> **Notice:** As ObjectDynamic is a custom user-defined object, so the user should determine the node type for the renderer to treat this object properly. Setting inappropriate node type may lead to system crashes.


### Members

---

## ObjectDynamic ( int flags = 0 )

Constructor. Creates a new dynamic object. By default, no flags are used.
### Arguments

- *int* **flags** - Dynamic flags: one of the [*OBJECT_DYNAMIC_**](#DYNAMIC_ALL) or [*OBJECT_IMMUTABLE_**](#IMMUTABLE_ALL) flags.

## ObjectDynamic.Attribute [] GetAttributes ( )

Returns an array of vertex attributes.
### Return value

Array of vertex attributes.
## void SetBoundBox ( BoundBox bb )

Sets a bounding box of a specified size for a given dynamic object surface.
### Arguments

- *[BoundBox](../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

## void SetBoundBox ( BoundBox bb , int surface )

Sets a bounding box of a specified size for a given dynamic object surface.
### Arguments

- *[BoundBox](../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.
- *int* **surface** - Surface number in range from 0 to the total number of dynamic mesh surfaces.

## void SetIndex ( int num , int index )

Updates the index in the index buffer (replaces the index with the given number with the specified index of the vertex).
### Arguments

- *int* **num** - Index number in the index buffer.
- *int* **index** - Vertex index in the index buffer to set.

## int GetIndex ( int num )

Returns the index of the vertex by the index number.
### Arguments

- *int* **num** - Index number.

### Return value

Vertex index in the index buffer.
## void SetIndicesArray ( int[] indices )

Updates the specified indices array.
> **Notice:** To apply changes you should call the [*flushIndices()*](#flushIndices_void) method after updating the indices array.


### Arguments

- *int[]* **indices** - Array of indices to be set.

## void SetParameterBool ( string name , bool value )

Sets boolean shader parameter of the specified value.
### Arguments

- *string* **name** - Shader parameter name.
- *bool* **value** - Parameter value.

## void SetParameterFloat ( string name , float[] value )

Sets float shader parameter of the specified value.
### Arguments

- *string* **name** - Name of the parameter.
- *float[]* **value** - Parameter value.

## void SetParameterFloatArray ( string name , float[] value , int num )

Sets an array of the specified number of float shader parameters.
### Arguments

- *string* **name** - Name of the parameter.
- *float[]* **value** - Parameter value.
- *int* **num** - Number of shader parameters.

## void SetParameterInt ( string name , int[] value )

Sets integer shader parameter of the specified value.
### Arguments

- *string* **name** - Name of the parameter.
- *int[]* **value** - Parameter value.

## void SetSurfaceBegin ( int begin , int surface )

Sets the begin index for the specified object surface.
### Arguments

- *int* **begin** - The index to be set as the begin one for the surface.
- *int* **surface** - Number of the target surface.

## int GetSurfaceBegin ( int surface )

Returns the begin index of the specified object surface.
### Arguments

- *int* **surface** - The number of the target surface in range from 0 to the total number of surfaces.

### Return value

The begin index.
## void SetSurfaceEnd ( int end , int surface )

Sets the end index for the specified object surface.
### Arguments

- *int* **end** - The index to be set as the end one for the surface.
- *int* **surface** - Number of the target surface.

## int GetSurfaceEnd ( int surface )

Returns the end index of the specified object surface.
### Arguments

- *int* **surface** - The number of the target surface in range from 0 to the total number of surfaces.

### Return value

The end index.
## void SetSurfaceMode ( ObjectDynamic.MODE mode , int surface )

Sets primitives to render an object surface with: triangles (by default), lines or points.
### Arguments

- *[ObjectDynamic.MODE](../../../api/library/objects/class.objectdynamic_cs.md#MODE)* **mode** - Surface rendering mode:

  - [OBJECT_DYNAMIC_MODE_TRIANGLES](#MODE_TRIANGLES)
  - [OBJECT_DYNAMIC_MODE_LINES](#MODE_LINES)
  - [OBJECT_DYNAMIC_MODE_POINTS](#MODE_POINTS)
- *int* **surface** - Surface number.

## ObjectDynamic.MODE GetSurfaceMode ( int surface )

Returns primitives used to render the object surface with: triangles (by default), lines or points.
### Arguments

- *int* **surface** - Number of a target surface.

### Return value

Surface rendering mode:
- OBJECT_DYNAMIC_MODE_POINTS = 0
- OBJECT_DYNAMIC_MODE_LINES
- OBJECT_DYNAMIC_MODE_TRIANGLES


## void SetSurfaceName ( string name , int surface )

Sets the name for the specified surface.
> **Notice:** The name will be set only if the specified surface was added via the *[addSurface()](#addSurface_cstr_void)* method.


### Arguments

- *string* **name** - Surface name.
- *int* **surface** - Number of a target surface in range from 0 to the total number of surfaces.

## void SetVertex ( int num , IntPtr vertex )

Updates a vertex in the vertices buffer.
### Arguments

- *int* **num** - Vertex number.
- *IntPtr* **vertex** - Vertex pointer.

## void SetVertexArray ( IntPtr vertex , int num_vertex )

Updates the vertices array.
### Arguments

- *IntPtr* **vertex** - Vertices array pointer.
- *int* **num_vertex** - Number of vertices.

## void SetVertexFloat ( int attribute , float[] value )

Updates the last added vertex to the vertex of the float type with the given parameters.
### Arguments

- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *float[]* **value** - Vertex coordinates.

## void SetVertexFloat ( int vertex , int attribute , float[] value )

Updates the given vertex to the vertex of the float type with the given parameters
### Arguments

- *int* **vertex** - Vertex index.
- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *float[]* **value** - Vertex coordinates.

## void SetVertexFormat ( Attribute[] attributes )

Sets the number of the vertex attributes.
The example of setting 4 different vertices attributes:


```cpp
const ObjectDynamic::Attribute attributes[] = {
	{ 0, ObjectDynamic::TYPE_FLOAT, 3 },
	{ 8, ObjectDynamic::TYPE_HALF, 4 },
	{ 16, ObjectDynamic::TYPE_HALF, 4 },
	{ 24, ObjectDynamic::TYPE_HALF, 4 }
};

// set vertex format
dynamic->setVertexFormat(attributes, 4);

```


### Arguments

- *Attribute[]* **attributes** - Number of the vertex attributes, can be up to 16 attributes for one vertex. The numeration starts from **0**. Each attribute consists of:

  - An offset of the vertex in bytes, depends on the vertex type and size.
  - Type of the vertex: [TYPE_FLOAT](#TYPE_FLOAT), [TYPE_HALF](#TYPE_HALF), [TYPE_UCHAR](#TYPE_UCHAR)
  - Size of the vertex: can be **1,2,3,4** for *float* type; **2,4** for *half* type; **4** for *UChar* type > **Notice:** When it goes to shader, **0** -attribute always comes with the size of **4**, no matter what size is specified in the method. All the other attributes comes with the specified sizes.

## void SetVertexHalf ( int attribute , float[] value )

Updates the last added vertex to the vertex of the half-float type with the given parameters.
### Arguments

- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *float[]* **value** - Vertex coordinates.

## void SetVertexHalf ( int vertex , int attribute , float[] value )

Updates the last added vertex to the vertex of the half-float type with the given parameters.
### Arguments

- *int* **vertex** - Vertex index.
- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *float[]* **value** - Vertex coordinates.

## void SetVertexUChar ( int attribute , unsigned char[] value )

Updates the last added vertex with the vertex of the unsigned char type with the given parameters.
### Arguments

- *int* **attribute** - The number of the attribute, as set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *unsigned char[]* **value** - Vertex coordinates.

## void SetVertexUChar ( int vertex , int attribute , unsigned char[] value )

Updates the last added vertex with the vertex of the unsigned char type with the given parameters.
### Arguments

- *int* **vertex** - Vertex index.
- *int* **attribute** - The number of the attribute, as set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *unsigned char[]* **value** - Vertex coordinates.

## void SetVertexUShort ( int attribute , unsigned short[] value )

Updates the last added vertex to the vertex of the unsigned short type with the given parameters.
### Arguments

- *int* **attribute** - The number of the attribute, as set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *unsigned short[]* **value** - Vertex coordinates.

## void SetVertexUShort ( int vertex , int attribute , unsigned short[] value )

Updates the given vertex to the vertex of the unsigned short type with the given parameters.
### Arguments

- *int* **vertex** - Vertex index.
- *int* **attribute** - The number of the attribute, as set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *unsigned short[]* **value** - Vertex coordinates.

## void AddIndex ( int index )

Adds an index to the index buffer.
### Arguments

- *int* **index** - Index to add.

## void AddIndicesArray ( int[] indices )

Adds an array of the specified number of indices.
### Arguments

- *int[]* **indices** - Indices array.

## void AddLineStrip ( int num_vertex )

Adds a line strip to the object.
> **Notice:** This method does not add the new vertices, but allocates their indices. Vertices should be created with [addVertexFloat()](#addVertexFloat_int_float_int_void), [addVertexHalf()](#addVertexHalf_int_float_int_void) or [addVertexUChar()](#addVertexUChar_int_uchar_int_void) methods accordingly to the required vertex type.


### Arguments

- *int* **num_vertex** - Number of vertices composing the strip.

## void AddPoints ( int num_points )

Adds the points to the object.
> **Notice:** This method does not add the new vertices, but allocates their indices. Vertices should be created with [addVertexFloat()](#addVertexFloat_int_float_int_void), [addVertexHalf()](#addVertexHalf_int_float_int_void) or [addVertexUChar()](#addVertexUChar_int_uchar_int_void) methods accordingly to the required vertex type.


### Arguments

- *int* **num_points** - Number of points.

## void AddSurface ( string name )

Adds all the last listed and unsigned vertices and triangles to a new surface with a specified name.
### Arguments

- *string* **name** - Name of the new surface.

## void AddTriangleFan ( int num_vertex )

Adds a triangle fan to the object.
> **Notice:** This method does not add the new vertices, but allocates their indices. Vertices should be created with [addVertexFloat()](#addVertexFloat_int_float_int_void), [addVertexHalf()](#addVertexHalf_int_float_int_void) or [addVertexUChar()](#addVertexUChar_int_uchar_int_void) methods accordingly to the required vertex type.


### Arguments

- *int* **num_vertex** - Number of vertices composing the fan.

## void AddTriangleQuads ( int num_quads )

Adds a given number of quadrilaterals to the mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with the [addVertex()](#addVertex_void_void) function. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_quads** - Number of quadrilaterals.

## void AddTriangles ( int num_triangles )

Adds a given number of triangles to the object.
> **Notice:** This method does not add the new vertices, but allocates their indices. Vertices should be created with [addVertexFloat()](#addVertexFloat_int_float_int_void), [addVertexHalf()](#addVertexHalf_int_float_int_void) or [addVertexUChar()](#addVertexUChar_int_uchar_int_void) methods accordingly to the required vertex type.


### Arguments

- *int* **num_triangles** - Number of triangles.

## void AddTriangleStrip ( int num_vertex )

Adds a triangle strip to the object.
> **Notice:** This method does not add the new vertices, but allocates their indices. Vertices should be created with [addVertexFloat()](#addVertexFloat_int_float_int_void), [addVertexHalf()](#addVertexHalf_int_float_int_void) or [addVertexUChar()](#addVertexUChar_int_uchar_int_void) methods accordingly to the required vertex type.


### Arguments

- *int* **num_vertex** - Number of vertices composing the strip.

## void AddVertex ( IntPtr vertex )

Adds a vertex to the vertices buffer.
### Arguments

- *IntPtr* **vertex** - Vertex pointer.

## void AddVertexArray ( IntPtr vertex , int num_vertex )

Adds an array of the specified vertices number.
### Arguments

- *IntPtr* **vertex** - Vertices array pointer.
- *int* **num_vertex** - Number of vertices.

## void AddVertexFloat ( int attribute , float[] value )

Adds a vertex of a float type with the given attribute, coordinates and size to the object.
> **Notice:** Before adding a vertex, make sure that you set all the attributes for it with the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.


### Arguments

- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *float[]* **value** - Vertex coordinates.

## void AddVertexHalf ( int attribute , float[] value )

Adds a vertex of the half-float type with the given attribute, coordinates and size to the object.
> **Notice:** Before adding a vertex, make sure that you set all the attributes for it with the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.


### Arguments

- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *float[]* **value** - Vertex coordinates.

## void AddVertexUChar ( int attribute , unsigned char[] value )

Adds a vertex of an unsigned char value with the given attribute, coordinates and size to the object.
### Arguments

- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *unsigned char[]* **value** - Vertex coordinates.

## void AddVertexUShort ( int attribute , unsigned short[] value )

Adds a vertex of an unsigned short value with the given attribute, coordinates and size to the object.
### Arguments

- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *unsigned short[]* **value** - Vertex coordinates.

## void AllocateIndices ( int num )

Allocate an index buffer for a given number of indices that will be used for an object. With this function, memory can be allocated once rather than in chunks, making the creation faster.
### Arguments

- *int* **num** - The number of indices that will be stored in a buffer.

## void AllocateVertex ( int num )

Allocate a vertex buffer for a given number of vertices that will be used for an object. With this function, memory can be allocated once rather than in chunks, making the creation faster.
### Arguments

- *int* **num** - The number of vertices that will be stored in a buffer.

## void ClearIndices ( )

Clears all the vertex indices in the object.
## void ClearSurfaces ( )

Clears all the surface settings.
## void ClearVertex ( )

Clears all the current vertex settings.
## void FlushIndices ( )

Flushes the index buffer and sends all data to GPU. If you change the contents of the index buffers, you should call this method.
## void FlushVertex ( )

Flushes the vertex buffer and sends all data to GPU. This method is called automatically, if the length of the vertex buffer changes. If you change the contents of the vertex buffers, you should call this method.
## void RemoveIndices ( int num , int size )

Removes the specified number of indices starting from the given index.
### Arguments

- *int* **num** - Number of the index in the index buffer.
- *int* **size** - Number of indices to remove.

## void RemoveVertex ( int num , int size , int indices )

Removes the specified number of vertices starting from the given vertex. To fix the index buffer after removal of vertices, pass 1 as the 3rd argument.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.
- *int* **size** - Number of vertices to remove.
- *int* **indices** - 1 to fix the index buffer after removal of vertices; otherwise, 0.

## void UpdateSurfaceBegin ( int surface )

Synchronizes surface begin index.
### Arguments

- *int* **surface** - The number of the target surface in range from 0 to the total number of surfaces.

## void UpdateSurfaceEnd ( int surface )

Synchronizes surface end index.
### Arguments

- *int* **surface** - The number of the target surface in range from 0 to the total number of surfaces.
