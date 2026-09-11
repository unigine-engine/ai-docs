# ObjectDynamic Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


The following sample demonstrates the *ObjectDynamic* class usage:

- [dynamic_05](../../../code/uniginescript/samples/objects/dynamic_05.md)


#### Creating a Dynamic Object


An example of creating a dynamic object - square:


> **Notice:** Do not forget to create **.mat** file with all the materials for the new dynamic object and add a reference to it in the **.world** file.


```cpp
#include <core/unigine.h>

/*
 */

// create a new dynamic object
ObjectDynamic dynamic;

/*
 */
int init() {

	// add a free-flying camera and set position to it
	Player player = new PlayerSpectator();
	player.setPosition(Vec3(4.0f,4.0f,4.0f));
	player.setDirection(vec3(-1.0f));
	engine.game.setPlayer(player);

	// add new dynamic object
	dynamic = new ObjectDynamic(1);
	// set a node type to determine materials that can be applied to the dynamic object
	dynamic.setMaterialNodeType(NODE_OBJECT_MESH_STATIC);
	// set a material (dynamic_mesh_base is inherited from mesh_base)
	dynamic.setMaterialPath("materials/dynamic_mesh_base.mat","*");

	// set vertex format
	dynamic.setVertexFormat((
		ivec3( 0, OBJECT_DYNAMIC_TYPE_FLOAT, 2),
		ivec3( 8, OBJECT_DYNAMIC_TYPE_HALF, 4),
		ivec3( 16, OBJECT_DYNAMIC_TYPE_HALF, 4),
		ivec3( 24, OBJECT_DYNAMIC_TYPE_HALF, 4),
	));

	// set vertex adding parameters
	void add_vertex(vec3 vertex,vec4 texcoord,vec3 normal,vec4 tangent) {
		dynamic.addVertexFloat(0,vertex,2);
		dynamic.setVertexHalf(1,texcoord,4);
		dynamic.setVertexHalf(2,vec4(normal,vertex.z),4);
		dynamic.setVertexHalf(3,tangent,4);
	}

	// add four vertices of a square
	add_vertex(vec3(-1.0f,-1.0f,0.0f),vec4(0.0f,0.0f,0.0f,0.0f),vec3(0.0f,0.0f,1.0f),vec4(1.0f,0.0f,0.0f,1.0f));
	add_vertex(vec3( 1.0f,-1.0f,0.0f),vec4(1.0f,0.0f,0.0f,0.0f),vec3(0.0f,0.0f,1.0f),vec4(1.0f,0.0f,0.0f,1.0f));
	add_vertex(vec3( 1.0f, 1.0f,0.0f),vec4(1.0f,1.0f,0.0f,0.0f),vec3(0.0f,0.0f,1.0f),vec4(1.0f,0.0f,0.0f,1.0f));
	add_vertex(vec3(-1.0f, 1.0f,0.0f),vec4(0.0f,1.0f,0.0f,0.0f),vec3(0.0f,0.0f,1.0f),vec4(1.0f,0.0f,0.0f,1.0f));

	// add the indices for the vertices
	dynamic.addIndex(0);
	dynamic.addIndex(1);
	dynamic.addIndex(2);

	dynamic.addIndex(2);
	dynamic.addIndex(3);
	dynamic.addIndex(0);

	// set a bounding box for the object
	BoundBox bb = new BoundBox(vec3(-1.0f),vec3(1.0f));
	dynamic.setBoundBox(bb);

	return 1;
}

/*
 */
int update() {

	// add a rotation to the object (if needed)
	dynamic.setWorldTransform(Mat4(rotateZ(engine.game.getTime() * 32.0f)));

	return 1;
}

```


## ObjectDynamic Class

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
## void setInstancing ( int instancing )

Sets a new value indicating if the hardware [instancing](../../../editor2/instancing_nodes/index.md) flag is enabled.
### Arguments

- *int* **instancing** - The hardware instancing

## int getInstancing () const

Returns the current value indicating if the hardware [instancing](../../../editor2/instancing_nodes/index.md) flag is enabled.
### Return value

Current hardware instancing
## void setMaterialNodeType ( int type )

Sets a new [node type](../../../api/library/nodes/class.node_usc.md) to be used by the renderer to determine which materials can be applied to the object. One of the [node type identifiers](../../../api/library/nodes/class.node_usc.md#DECAL_BEGIN).
> **Notice:** As ObjectDynamic is a custom user-defined object, so the user should determine the node type for the renderer to treat this object properly. Setting inappropriate node type may lead to system crashes.


### Arguments

- *int* **type** - The node type to be used by the renderer to determine which materials can be applied to the object

## int getMaterialNodeType () const

Returns the current [node type](../../../api/library/nodes/class.node_usc.md) to be used by the renderer to determine which materials can be applied to the object. One of the [node type identifiers](../../../api/library/nodes/class.node_usc.md#DECAL_BEGIN).
> **Notice:** As ObjectDynamic is a custom user-defined object, so the user should determine the node type for the renderer to treat this object properly. Setting inappropriate node type may lead to system crashes.


### Return value

Current node type to be used by the renderer to determine which materials can be applied to the object
---

## static ObjectDynamic ( int flags = 0 )

Constructor. Creates a new dynamic object. By default, no flags are used.
### Arguments

- *int* **flags** - Dynamic flags: one of the [*OBJECT_DYNAMIC_**](#DYNAMIC_ALL) or [*OBJECT_IMMUTABLE_**](#IMMUTABLE_ALL) flags.

## Attribute * getAttributes ( )

Returns an array of vertex attributes.
### Return value

Array of vertex attributes.
## void setBoundBox ( BoundBox bb )

Sets a bounding box of a specified size for a given dynamic object surface.
### Arguments

- *BoundBox* **bb** - Bounding box.

## void setBoundBox ( BoundBox bb , int surface )

Sets a bounding box of a specified size for a given dynamic object surface.
### Arguments

- *BoundBox* **bb** - Bounding box.
- *int* **surface** - Surface number in range from 0 to the total number of dynamic mesh surfaces.

## void setIndex ( int num , int index )

Updates the index in the index buffer (replaces the index with the given number with the specified index of the vertex).
### Arguments

- *int* **num** - Index number in the index buffer.
- *int* **index** - Vertex index in the index buffer to set.

## int getIndex ( int num )

Returns the index of the vertex by the index number.
### Arguments

- *int* **num** - Index number.

### Return value

Vertex index in the index buffer.
## void setParameterBool ( string name , int value )

Sets boolean shader parameter of the specified value.
### Arguments

- *string* **name** - Shader parameter name.
- *int* **value** - Parameter value.

## void setParameterFloat ( )

Sets float shader parameter of the specified value.
### Arguments

## void setParameterInt ( string name )

Sets integer shader parameter of the specified value.
### Arguments

- *string* **name** - Name of the parameter.

## void setSurfaceBegin ( int begin , int surface )

Sets the begin index for the specified object surface.
### Arguments

- *int* **begin** - The index to be set as the begin one for the surface.
- *int* **surface** - Number of the target surface.

## int getSurfaceBegin ( int surface )

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

## int getSurfaceEnd ( int surface )

Returns the end index of the specified object surface.
### Arguments

- *int* **surface** - The number of the target surface in range from 0 to the total number of surfaces.

### Return value

The end index.
## void setSurfaceMode ( int mode , int surface )

Sets primitives to render an object surface with: triangles (by default), lines or points.
### Arguments

- *int* **mode** - Surface rendering mode:

  - [OBJECT_DYNAMIC_MODE_TRIANGLES](#MODE_TRIANGLES)
  - [OBJECT_DYNAMIC_MODE_LINES](#MODE_LINES)
  - [OBJECT_DYNAMIC_MODE_POINTS](#MODE_POINTS)
- *int* **surface** - Surface number.

## int getSurfaceMode ( int surface )

Returns primitives used to render the object surface with: triangles (by default), lines or points.
### Arguments

- *int* **surface** - Number of a target surface.

### Return value

Surface rendering mode:
- OBJECT_DYNAMIC_MODE_POINTS = 0
- OBJECT_DYNAMIC_MODE_LINES
- OBJECT_DYNAMIC_MODE_TRIANGLES


## void setSurfaceName ( string name , int surface )

Sets the name for the specified surface.
> **Notice:** The name will be set only if the specified surface was added via the *[addSurface()](#addSurface_cstr_void)* method.


### Arguments

- *string* **name** - Surface name.
- *int* **surface** - Number of a target surface in range from 0 to the total number of surfaces.

## void setVertexFloat ( int attribute )

Updates the last added vertex to the vertex of the float type with the given parameters.
### Arguments

- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.

## void setVertexFloat ( int vertex , int attribute )

Updates the given vertex to the vertex of the float type with the given parameters
### Arguments

- *int* **vertex** - Vertex index.
- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.

## void setVertexFormat ( )

Sets the number of the vertex attributes.
> **Notice:** This method does not create vertices, but their attributes. Vertices should be created with [addVertexFloat()](#addVertexFloat_int_float_int_void), [addVertexHalf()](#addVertexHalf_int_float_int_void) or [addVertexUChar()](#addVertexUChar_int_uchar_int_void) methods accordingly to the type specified in this method.


The example of setting 3 different vertices attributes:


```cpp
// vertex format
dynamic.setVertexFormat((
	ivec3( 0, OBJECT_DYNAMIC_TYPE_FLOAT, 1),
	ivec3( 12, OBJECT_DYNAMIC_TYPE_HALF, 2),
	ivec3( 24, OBJECT_DYNAMIC_TYPE_UCHAR, 4),
));

```


### Arguments

## void setVertexHalf ( int attribute )

Updates the last added vertex to the vertex of the half-float type with the given parameters.
### Arguments

- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.

## void setVertexHalf ( int vertex , int attribute )

Updates the last added vertex to the vertex of the half-float type with the given parameters.
### Arguments

- *int* **vertex** - Vertex index.
- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.

## void addIndex ( int index )

Adds an index to the index buffer.
### Arguments

- *int* **index** - Index to add.

## void addLineStrip ( int num_vertex )

Adds a line strip to the object.
> **Notice:** This method does not add the new vertices, but allocates their indices. Vertices should be created with [addVertexFloat()](#addVertexFloat_int_float_int_void), [addVertexHalf()](#addVertexHalf_int_float_int_void) or [addVertexUChar()](#addVertexUChar_int_uchar_int_void) methods accordingly to the required vertex type.


### Arguments

- *int* **num_vertex** - Number of vertices composing the strip.

## void addPoints ( int num_points )

Adds the points to the object.
> **Notice:** This method does not add the new vertices, but allocates their indices. Vertices should be created with [addVertexFloat()](#addVertexFloat_int_float_int_void), [addVertexHalf()](#addVertexHalf_int_float_int_void) or [addVertexUChar()](#addVertexUChar_int_uchar_int_void) methods accordingly to the required vertex type.


### Arguments

- *int* **num_points** - Number of points.

## void addSurface ( string name )

Adds all the last listed and unsigned vertices and triangles to a new surface with a specified name.
### Arguments

- *string* **name** - Name of the new surface.

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

## void addVertexFloat ( int attribute )

Adds a vertex of a float type with the given attribute, coordinates and size to the object.
> **Notice:** Before adding a vertex, make sure that you set all the attributes for it with the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.


### Arguments

- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.

## void addVertexHalf ( int attribute )

Adds a vertex of the half-float type with the given attribute, coordinates and size to the object.
> **Notice:** Before adding a vertex, make sure that you set all the attributes for it with the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.


### Arguments

- *int* **attribute** - The number of the attribute, set in the [setVertexFormat()](#setVertexFormat_Attribute_int_void) method.

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

## void updateSurfaceBegin ( int surface )

Synchronizes surface begin index.
### Arguments

- *int* **surface** - The number of the target surface in range from 0 to the total number of surfaces.

## void updateSurfaceEnd ( int surface )

Synchronizes surface end index.
### Arguments

- *int* **surface** - The number of the target surface in range from 0 to the total number of surfaces.
