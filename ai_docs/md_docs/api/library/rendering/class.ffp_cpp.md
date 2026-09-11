# Unigine.Ffp Class (CPP)

**Header:** #include <UnigineFfp.h>

> **Notice:** This class is a singleton.


Interface for fixed function pipeline.


Ffp class in Unigine differs from the classic OpenGL FFP implementation. For example, Unigine [Visualizer](../../../code/console/index.md#visualizer) and [Texture Buffers for Debugging](../../../code/console/index.md#render_show_textures) are implemented by using FFP. FFP uses already implemented D3D12 and Vulkan shader programs (without creating materials, etc.) to render.


This interface enables to render basic geometric primitives. For example, it can be used to draw a project watermark.


#### Usage Example


Here is an example how to render 2D texture:


```cpp
/* ... */
// begin triangles rendering
Ffp::beginTriangles();
	// add single triangle quad
	// this method creates indices
	Ffp::addTriangleQuads(1);
	// add 4 vertices and texcoords
	Ffp::addVertex(x0,y0);
	Ffp::setTexCoord(0.0f,0.0f);
	Ffp::addVertex(x1,y0);
	Ffp::setTexCoord(1.0f,0.0f);
	Ffp::addVertex(x1,y1);
	Ffp::setTexCoord(1.0f,1.0f);
	Ffp::addVertex(x0,y1);
	Ffp::setTexCoord(0.0f,1.0f);
// end of triangles rendering
Ffp::endTriangles();

```


### See Also


- C++ API sample located in the folder **<UnigineSDK>/source/samples/Api/Systems/Ffp**
- C# API sample located in the folder **<UnigineSDK>/source/csharp/samples/Api/Systems/Ffp**


## Ffp Class

### Members

## int getNumIndices () const

Returns the current number of indices in the current primitive batch.
### Return value

Current number of indices in the current primitive batch.
## int getNumVertex () const

Returns the current number of vertices in the current primitive batch.
### Return value

Current number of vertices in the current primitive batch.
## void setTransform ( const Math:: mat4 & transform )

Sets a new Transformation matrix of the rendered primitive.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md)&* **transform** - The Transformation matrix of the rendered primitive.

## Math:: mat4 getTransform () const

Returns the current Transformation matrix of the rendered primitive.
### Return value

Current Transformation matrix of the rendered primitive.
## bool isEnabled () const

Returns the current a value indicating if the FFP is enabled.
### Return value

**true** if FFP is enabled is enabled ; otherwise **false**.
## void setMode ( int mode )

Sets a new FFP mode.
### Arguments

- *int* **mode** - The FFP mode.

## int getMode () const

Returns the current FFP mode.
### Return value

Current FFP mode.
## void setTextureSample ( int sample )

Sets a new texture sample flag.
### Arguments

- *int* **sample** - The texture sample flag, one of the *[TEXTURE_SAMPLE_*](#TEXTURE_SAMPLE_2D)* values.

## int getTextureSample () const

Returns the current texture sample flag.
### Return value

Current texture sample flag, one of the *[TEXTURE_SAMPLE_*](#TEXTURE_SAMPLE_2D)* values.
---

## void setColor ( unsigned int color )


Sets rendering color for the last added vertex.


You can use [COLOR_*](#COLOR_BLACK) variables to set the color.


### Arguments

- *unsigned int* **color** - Color in ARGB8 format: (a << 24) | (r << 16) | (g << 8) | (b << 0).

## void setColor ( float r , float g , float b , float a )

Sets rendering color for the last added vertex.
### Arguments

- *float* **r** - Red color component.
- *float* **g** - Green color component.
- *float* **b** - Blue color component.
- *float* **a** - Alpha color component.

## void setOrtho ( int width , int height )


Sets orthographic projection to render the primitive.


For example, the [`render_show_textures`](../../../code/console/index.md#render_show_textures) console command renders textures via FFP by using orthographic projection.


### Arguments

- *int* **width** - Primitive width.
- *int* **height** - Primitive height.

## void setTexCoord ( float x , float y , float z = 0.0f , float w = 1.0f )

Sets texture coordinates for the last added vertex.
### Arguments

- *float* **x** - X texture coordinate.
- *float* **y** - Y texture coordinate.
- *float* **z** - Z texture coordinate.
- *float* **w** - W texture coordinate.

## void addIndex ( int index )

Adds given index to FFP.
### Arguments

- *int* **index** - Index of a vertex.

## void addIndices ( int i0 , int i1 )

Adds two given indices to FFP.
### Arguments

- *int* **i0** - The first index.
- *int* **i1** - The second index.

## void addIndices ( ushort* OUT_indices , int indices_size , int vertex_offset )

Adds the specified array of indices to FFP with the specified vertex offset.
### Arguments

- *ushort** **OUT_indices** - Array of indices to be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **indices_size** - Number of elements in the array.
- *int* **vertex_offset** - Vertex offset.

## void addIndices ( ushort* OUT_indices , int indices_size )

Adds the specified array of indices to FFP.
### Arguments

- *ushort** **OUT_indices** - Array of indices to be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **indices_size** - Number of elements in the array.

## void addIndices ( int i0 , int i1 , int i2 , int i3 )

Adds four given indices to FFP.
### Arguments

- *int* **i0** - The first index.
- *int* **i1** - The second index.
- *int* **i2** - The third index.
- *int* **i3** - The fourth index.

## void addIndices ( int i0 , int i1 , int i2 )

Adds three given indices to FFP.
### Arguments

- *int* **i0** - The first index.
- *int* **i1** - The second index.
- *int* **i2** - The third index.

## void addLines ( int num )

Adds a specified number of lines. This method does not add vertices; instead, it allocates indices, for which vertices should be then created with *addVertex()*. Indices will point to vertices starting from the last added vertex.
### Arguments

- *int* **num** - The number of lines.

## void addTriangleQuads ( int num )

Adds a specified number of quads. This method does not add vertices; instead, it allocates indices, for which vertices should be then created with *addVertex()*. Indices will point to vertices starting from the last added vertex.
### Arguments

- *int* **num** - The number of quads.

## void addTriangles ( int num )

Adds a specified number of triangles. This method does not add vertices; instead, it allocates indices, for which vertices should be then created with *addVertex()*. Indices will point to vertices starting from the last added vertex.
### Arguments

- *int* **num** - The number of triangles.

## void addVertex ( Vertex* OUT_vertex , int vertex_size )

Adds the specified vertex array to FFP.
### Arguments

- *Vertex** **OUT_vertex** - Array of vertices to be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **vertex_size** - Number of vertices in the array.

## void addVertex ( const Ffp::Vertex & vertex )

Adds given vertex to FFP.
### Arguments

- *const [Ffp::Vertex](../../../api/library/rendering/class.ffp_cpp.md#Vertex) &* **vertex** - Vertex.

## void addVertex ( float x , float y , float z = 0.0f )

Adds a vertex with given coordinates to FFP.
### Arguments

- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.

## void beginLines ( )

Begins rendering of lines. Specify a list of vertex or index data between *beginLines()* and *endLines()*.
## void beginTriangles ( )

Begins rendering of triangles. Specify a list of primitives and vertex data between *beginTriangles()* and *endTriangles()*.
## void disable ( )

Disables FFP rendering.
## void enable ( int mode = MODE_DEFAULT , int texture_sample = 0 )

Enables FFP rendering.
### Arguments

- *int* **mode** - FFP mode.
- *int* **texture_sample** - Texture sampler flag to be set. One of the *[TEXTURE_SAMPLE_*](#TEXTURE_SAMPLE_2D)* values.

## void endLines ( )

Ends rendering of lines (i.e. draws the specified lines).
## void endTriangles ( )

Ends rendering of triangles (i.e. draws the specified triangles).
## void renderScreen ( )

Renderers a full screen quad. It should be used when rendering post effects.
