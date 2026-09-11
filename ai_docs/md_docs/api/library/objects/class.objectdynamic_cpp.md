# ObjectDynamic Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


ObjectDynamic class allows to create a dynamic object, which can be rendered by means of any type of geometry (vertex format for an object is changeable). The class supports instancing as well as point/line/triangle rendering modes. ObjectDynamic class requires a custom shader for rendering, no built-in shaders are available.


## ObjectDynamic Class

### Enums

## MODE

| Name | Description |
|---|---|
| **MODE_POINTS** = 0 | Mode to render the points. |
| **MODE_LINES** = 1 | Mode to render the lines. |
| **MODE_TRIANGLES** = 2 | Mode to render the triangles. |
| **MODE_TRIANGLE_PATCHES** = 3 | Mode to render the triangle patches. |
| **MODE_QUAD_PATCHES** = 4 | Mode to render the quad patches. |

### Members

## void setNumIndices ( int indices )

Sets a new number of vertex indices used by the object.
### Arguments

- *int* **indices** - The number of vertex indices used by the object

## int getNumIndices () const

Returns the current number of vertex indices used by the object.
### Return value

Current number of vertex indices used by the object
## void setNumVertex ( int vertex )

Sets a new number of vertices composing the object.
### Arguments

- *int* **vertex** - The number of vertices composing the object

## int getNumVertex () const

Returns the current number of vertices composing the object.
### Return value

Current number of vertices composing the object
## int getNumAttributes () const

Returns the current number of vertex attributes.
### Return value

Current number of vertex attributes
## int getVertexSize () const

Returns the current size of the current vertex, bytes.
### Return value

Current size of the current vertex, in bytes
## void setInstancing ( bool instancing )

Sets a new value indicating if the hardware [instancing](../../../editor2/instancing_nodes/index.md) flag is enabled.
### Arguments

- *bool* **instancing** - Set **true** to enable hardware instancing; **false** - to disable it.

## bool getInstancing () const

Returns the current value indicating if the hardware [instancing](../../../editor2/instancing_nodes/index.md) flag is enabled.
### Return value

**true** if hardware instancing is enabled ; otherwise **false**.
## void setMaterialNodeType ( Node::TYPE type )

Sets a new [node type](../../../api/library/nodes/class.node_cpp.md) to be used by the renderer to determine which materials can be applied to the object. One of the [node type identifiers](../../../api/library/nodes/class.node_cpp.md#DECAL_BEGIN).
> **Notice:** As ObjectDynamic is a custom user-defined object, so the user should determine the node type for the renderer to treat this object properly. Setting inappropriate node type may lead to system crashes.


### Arguments

- *[Node::TYPE](../../../api/library/nodes/class.node_cpp.md#TYPE)* **type** - The node type to be used by the renderer to determine which materials can be applied to the object

## Node::TYPE getMaterialNodeType () const

Returns the current [node type](../../../api/library/nodes/class.node_cpp.md) to be used by the renderer to determine which materials can be applied to the object. One of the [node type identifiers](../../../api/library/nodes/class.node_cpp.md#DECAL_BEGIN).
> **Notice:** As ObjectDynamic is a custom user-defined object, so the user should determine the node type for the renderer to treat this object properly. Setting inappropriate node type may lead to system crashes.


### Return value

Current node type to be used by the renderer to determine which materials can be applied to the object
---

## static ObjectDynamicPtr create ( int flags = 0 )

Constructor. Creates a new dynamic object. By default, no flags are used.
### Arguments

- *int* **flags** - Dynamic flags: one of the [*OBJECT_DYNAMIC_**](#DYNAMIC_ALL) or [*OBJECT_IMMUTABLE_**](#IMMUTABLE_ALL) flags.

## const ObjectDynamic::Attribute * getAttributes ( ) const

Returns an array of vertex attributes.
### Return value

Array of vertex attributes.
## void setBoundBox ( const Math:: BoundBox & bb )

Sets a bounding box of a specified size for a given dynamic object surface.
### Arguments

- *const  Math::[BoundBox](../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

## void setBoundBox ( const Math:: BoundBox & bb , int surface )

Sets a bounding box of a specified size for a given dynamic object surface.
### Arguments

- *const  Math::[BoundBox](../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.
- *int* **surface** - Surface number in range from 0 to the total number of dynamic mesh surfaces.

## void setIndex ( int num , int index )

Updates the index in the index buffer (replaces the index with the given number with the specified index of the vertex).
### Arguments

- *int* **num** - Index number in the index buffer.
- *int* **index** - Vertex index in the index buffer to set.

## int getIndex ( int num ) const

Returns the index of the vertex by the index number.
### Arguments

- *int* **num** - Index number.

### Return value

Vertex index in the index buffer.
## void setIndicesArray ( const int * indices , int indices_size )

Updates the specified indices array.
> **Notice:** To apply changes you should call the [*flushIndices()*](#flushIndices_void) method after updating the indices array.


### Arguments

- *const int ** **indices** - Array of indices to be set.
- *int* **indices_size** - Number of indices to be set.

## void setParameterBool ( const char * name , bool value )

Sets boolean shader parameter of the specified value.
### Arguments

- *const char ** **name** - Shader parameter name.
- *bool* **value** - Parameter value.

## void setParameterFloat ( const char * name , const float * value , int value_size )

Sets float shader parameter of the specified value.
### Arguments

- *const char ** **name** - Name of the parameter.
- *const float ** **value** - Parameter value.
- *int* **value_size** - Number of values to be set.

## void setParameterFloatArray ( const char * name , const float * value , int value_size , int num )

Sets an array of the specified number of float shader parameters.
### Arguments

- *const char ** **name** - Name of the parameter.
- *const float ** **value** - Parameter value.
- *int* **value_size** - Number of values to be set.
- *int* **num** - Number of shader parameters.

## void setParameterInt ( const char * name , const int * value , int value_size )

Sets integer shader parameter of the specified value.
### Arguments

- *const char ** **name** - Name of the parameter.
- *const int ** **value** - Parameter value.
- *int* **value_size** - Number of values to be set.

## void setSurfaceBegin ( int begin , int surface )

Sets the begin index for the specified object surface.
### Arguments

- *int* **begin** - The index to be set as the begin one for the surface.
- *int* **surface** - Number of the target surface.

## int getSurfaceBegin ( int surface ) const

Returns the begin index of the specified object surface.
### Arguments

- *int* **surface** - The number of the target surface in range from 0 to the total number of surfaces.

### Return value

The begin index.
## void setSurfaceEnd ( int end , int surface )

Sets the end index for the specified object surface.
### Arguments

- *int* **end** - The index to be set as the end one for the surface.
- *int* **surface** - Number of the target surface.

## int getSurfaceEnd ( int surface ) const

Returns the end index of the specified object surface.
### Arguments

- *int* **surface** - The number of the target surface in range from 0 to the total number of surfaces.

### Return value

The end index.
## void setSurfaceMode ( ObjectDynamic::MODE mode , int surface )

Sets primitives to render an object surface with: triangles (by default), lines or points.
### Arguments

- *[ObjectDynamic::MODE](../../../api/library/objects/class.objectdynamic_cpp.md#MODE)* **mode** - Surface rendering mode.
- *int* **surface** - Number of a target surface.

## ObjectDynamic::MODE getSurfaceMode ( int surface ) const

Returns primitives used to render the object surface with: triangles (by default), lines or points.
### Arguments

- *int* **surface** - Number of a target surface.

### Return value

Surface rendering mode:
- OBJECT_DYNAMIC_MODE_POINTS = 0
- OBJECT_DYNAMIC_MODE_LINES
- OBJECT_DYNAMIC_MODE_TRIANGLES


## void setSurfaceName ( const char * name , int surface )

Sets the name for the specified surface.
> **Notice:** The name will be set only if the specified surface was added via the *[addSurface()](#addSurface_cstr_void)* method.


### Arguments

- *const char ** **name** - Surface name.
- *int* **surface** - Number of a target surface in range from 0 to the total number of surfaces.

## void setVertex ( int num , const void * vertex )

Updates a vertex in the vertices buffer.
### Arguments

- *int* **num** - Vertex number.
- *const void ** **vertex** - Vertex pointer.

## void setVertexArray ( const void * vertex , int num_vertex )

Updates the vertices array.
### Arguments

- *const void ** **vertex** - Vertices array pointer.
- *int* **num_vertex** - Number of vertices.

## void setVertexFloat ( int attribute , const float * value , int value_size )

Updates the last added vertex to the vertex of the float type with the given parameters.
### Arguments

- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *const float ** **value** - Vertex coordinates.
- *int* **value_size** - Number of values to be set.

## void setVertexFloat ( int vertex , int attribute , const float * value , int value_size )

Updates the given vertex to the vertex of the float type with the given parameters
### Arguments

- *int* **vertex** - Vertex index.
- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *const float ** **value** - Vertex coordinates.
- *int* **value_size** - Number of values to be set.

## void setVertexFormat ( const ObjectDynamic::Attribute * attributes , int attributes_size )

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

- *const [ObjectDynamic::Attribute](../../../api/library/objects/class.objectdynamic_cpp.md#Attribute) ** **attributes** - Number of the vertex attributes, can be up to 16 attributes for one vertex. The numeration starts from **0**. Each attribute consists of:

  - An offset of the vertex in bytes, depends on the vertex type and size.
  - Type of the vertex: [TYPE_FLOAT](#TYPE_FLOAT), [TYPE_HALF](#TYPE_HALF), [TYPE_UCHAR](#TYPE_UCHAR)
  - Size of the vertex: can be **1,2,3,4** for *float* type; **2,4** for *half* type; **4** for *UChar* type > **Notice:** When it goes to shader, **0** -attribute always comes with the size of **4**, no matter what size is specified in the method. All the other attributes comes with the specified sizes.
- *int* **attributes_size** - Number of attributes to be set.

## void setVertexHalf ( int attribute , const float * value , int value_size )

Updates the last added vertex to the vertex of the half-float type with the given parameters.
### Arguments

- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *const float ** **value** - Vertex coordinates.
- *int* **value_size** - Number of values to be set.

## void setVertexHalf ( int vertex , int attribute , const float * value , int value_size )

Updates the last added vertex to the vertex of the half-float type with the given parameters.
### Arguments

- *int* **vertex** - Vertex index.
- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *const float ** **value** - Vertex coordinates.
- *int* **value_size** - Number of values to be set.

## void setVertexUChar ( int attribute , const unsigned char * value , int value_size )

Updates the last added vertex with the vertex of the unsigned char type with the given parameters.
### Arguments

- *int* **attribute** - The number of the attribute, as set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *const unsigned char ** **value** - Vertex coordinates.
- *int* **value_size** - Number of values to be set.

## void setVertexUChar ( int vertex , int attribute , const unsigned char * value , int value_size )

Updates the last added vertex with the vertex of the unsigned char type with the given parameters.
### Arguments

- *int* **vertex** - Vertex index.
- *int* **attribute** - The number of the attribute, as set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *const unsigned char ** **value** - Vertex coordinates.
- *int* **value_size** - Number of values to be set.

## void setVertexUShort ( int attribute , const unsigned short * value , int value_size )

Updates the last added vertex to the vertex of the unsigned short type with the given parameters.
### Arguments

- *int* **attribute** - The number of the attribute, as set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *const unsigned short ** **value** - Vertex coordinates.
- *int* **value_size** - Number of values to be set.

## void setVertexUShort ( int vertex , int attribute , const unsigned short * value , int value_size )

Updates the given vertex to the vertex of the unsigned short type with the given parameters.
### Arguments

- *int* **vertex** - Vertex index.
- *int* **attribute** - The number of the attribute, as set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *const unsigned short ** **value** - Vertex coordinates.
- *int* **value_size** - Number of values to be set.

## void addIndex ( int index )

Adds an index to the index buffer.
### Arguments

- *int* **index** - Index to add.

## void addIndicesArray ( const int * indices , int indices_size )

Adds an array of the specified number of indices.
### Arguments

- *const int ** **indices** - Indices array.
- *int* **indices_size** - Number of indices to be set.

## void addLineStrip ( int num_vertex )

Adds a line strip to the object.
> **Notice:** This method does not add the new vertices, but allocates their indices. Vertices should be created with [addVertexFloat()](#addVertexFloat_int_float_int_void), [addVertexHalf()](#addVertexHalf_int_float_int_void) or [addVertexUChar()](#addVertexUChar_int_uchar_int_void) methods accordingly to the required vertex type.


### Arguments

- *int* **num_vertex** - Number of vertices.

## void addPoints ( int num_points )

Adds the points to the object.
> **Notice:** This method does not add the new vertices, but allocates their indices. Vertices should be created with [addVertexFloat()](#addVertexFloat_int_float_int_void), [addVertexHalf()](#addVertexHalf_int_float_int_void) or [addVertexUChar()](#addVertexUChar_int_uchar_int_void) methods accordingly to the required vertex type.


### Arguments

- *int* **num_points** - Number of points.

## void addSurface ( const char * name )

Adds all the last listed and unsigned vertices and triangles to a new surface with a specified name.
### Arguments

- *const char ** **name** - Name of the new surface.

## void addTriangleFan ( int num_vertex )

Adds a triangle fan to the object.
> **Notice:** This method does not add the new vertices, but allocates their indices. Vertices should be created with [addVertexFloat()](#addVertexFloat_int_float_int_void), [addVertexHalf()](#addVertexHalf_int_float_int_void) or [addVertexUChar()](#addVertexUChar_int_uchar_int_void) methods accordingly to the required vertex type.


### Arguments

- *int* **num_vertex** - Number of vertices composing the fan.

## void addTriangleQuads ( int num_quads )

Adds a given number of quadrilaterals to the mesh. This method does not add vertices, rather it allocates indices, for which vertices should be then created with the [addVertex()](#addVertex_void_void) function. Indices will point to vertices starting from the current last vertex in the vertex buffer.
### Arguments

- *int* **num_quads** - Number of quadrilaterals.

## void addTriangles ( int num_triangles )

Adds a given number of triangles to the object.
> **Notice:** This method does not add the new vertices, but allocates their indices. Vertices should be created with [addVertexFloat()](#addVertexFloat_int_float_int_void), [addVertexHalf()](#addVertexHalf_int_float_int_void) or [addVertexUChar()](#addVertexUChar_int_uchar_int_void) methods accordingly to the required vertex type.


### Arguments

- *int* **num_triangles** - Number of triangles.

## void addTriangleStrip ( int num_vertex )

Adds a triangle strip to the object.
> **Notice:** This method does not add the new vertices, but allocates their indices. Vertices should be created with [addVertexFloat()](#addVertexFloat_int_float_int_void), [addVertexHalf()](#addVertexHalf_int_float_int_void) or [addVertexUChar()](#addVertexUChar_int_uchar_int_void) methods accordingly to the required vertex type.


### Arguments

- *int* **num_vertex** - Number of vertices composing the strip.

## void addVertex ( const void * vertex )

Adds a vertex to the vertices buffer.
### Arguments

- *const void ** **vertex** - Vertex pointer.

## void addVertexArray ( const void * vertex , int num_vertex )

Adds an array of the specified vertices number.
### Arguments

- *const void ** **vertex** - Vertices array pointer.
- *int* **num_vertex** - Number of vertices.

## void addVertexFloat ( int attribute , const float * value , int value_size )

Adds a vertex of a float type with the given attribute, coordinates and size to the object.
> **Notice:** Before adding a vertex, make sure that you set all the attributes for it with the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.


### Arguments

- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *const float ** **value** - Vertex coordinates.
- *int* **value_size** - Number of values to be set.

## void addVertexHalf ( int attribute , const float * value , int value_size )

Adds a vertex of the half-float type with the given attribute, coordinates and size to the object.
> **Notice:** Before adding a vertex, make sure that you set all the attributes for it with the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.


### Arguments

- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *const float ** **value** - Vertex coordinates.
- *int* **value_size** - Number of values to be set.

## void addVertexUChar ( int attribute , const unsigned char * value , int value_size )

Adds a vertex of an unsigned char value with the given attribute, coordinates and size to the object.
### Arguments

- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *const unsigned char ** **value** - Vertex coordinates.
- *int* **value_size** - Number of values to be set.

## void addVertexUShort ( int attribute , const unsigned short * value , int value_size )

Adds a vertex of an unsigned short value with the given attribute, coordinates and size to the object.
### Arguments

- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.
- *const unsigned short ** **value** - Vertex coordinates.
- *int* **value_size** - Number of values to be set.

## void allocateIndices ( int num )

Allocate an index buffer for a given number of indices that will be used for an object. With this function, memory can be allocated once rather than in chunks, making the creation faster.
### Arguments

- *int* **num** - The number of indices that will be stored in a buffer.

## void allocateVertex ( int num )

Allocate a vertex buffer for a given number of vertices that will be used for an object. With this function, memory can be allocated once rather than in chunks, making the creation faster.
### Arguments

- *int* **num** - The number of vertices that will be stored in a buffer.

## void clearIndices ( )

Clears all the vertex indices in the object.
## void clearSurfaces ( )

Clears all the surface settings.
## void clearVertex ( )

Clears all the current vertex settings.
## void flushIndices ( )

Flushes the index buffer and sends all data to GPU. If you change the contents of the index buffers, you should call this method.
## void flushVertex ( )

Flushes the vertex buffer and sends all data to GPU. This method is called automatically, if the length of the vertex buffer changes. If you change the contents of the vertex buffers, you should call this method.
## void removeIndices ( int num , int size )

Removes the specified number of indices starting from the given index.
### Arguments

- *int* **num** - Number of the index in the index buffer.
- *int* **size** - Number of indices to remove.

## void removeVertex ( int num , int size , int indices )

Removes the specified number of vertices starting from the given vertex. To fix the index buffer after removal of vertices, pass 1 as the 3rd argument.
### Arguments

- *int* **num** - Number of the vertex in the vertex buffer.
- *int* **size** - Number of vertices to remove.
- *int* **indices** - 1 to fix the index buffer after removal of vertices; otherwise, 0.

## static int type ( )

Returns the type of the object.
### Return value

[Object Dynamic](../../../api/library/nodes/class.node_cpp.md#OBJECT_DYNAMIC) type identifier.
## void updateSurfaceBegin ( int surface )

Synchronizes surface begin index.
### Arguments

- *int* **surface** - The number of the target surface in range from 0 to the total number of surfaces.

## void updateSurfaceEnd ( int surface )

Synchronizes surface end index.
### Arguments

- *int* **surface** - The number of the target surface in range from 0 to the total number of surfaces.
