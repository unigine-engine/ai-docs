# Unigine.Ffp Class (CPP)

**Header:** #include <UnigineFfp.h>

> **Notice:** This class is a singleton.


Interface for fixed function pipeline.


Ffp class in Unigine differs from the classic OpenGL FFP implementation. For example, Unigine [Visualizer](../../../code/console/index.md#visualizer) and [Texture Buffers for Debugging](../../../code/console/index.md#render_show_textures) are implemented by using Ffp. Ffp uses already implemented D3D12 and Vulkan shader programs (without creating materials, etc.) to render.


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

## bool isEnabled ( ) const

Return a value indicating if the Ffp is enabled.
### Return value

Returns **1** if the Ffp is enabled; otherwise, **0**.
## void setMode ( int mode )

Sets current Ffp mode.
### Arguments

- *int* **mode** - Current Ffp mode.

## int getMode ( ) const

Returns current Ffp mode.
### Return value

Current Ffp mode.
## int getNumIndices ( ) const

Returns the number of indices in the current primitive batch.
### Return value

The number of indices.
## int getNumVertex ( ) const

Returns the number of vertices in the current primitive batch.
### Return value

The number of vertices.
## void setOrtho ( int width , int height )

Sets orthographic projection to render the primitive.
For example, the [`render_show_textures`](../../../code/console/index.md#render_show_textures) console command renders textures via Ffp by using orthographic projection.


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

## void setTransform ( const Math:: mat4 & transform )

Sets transformation matrix for the rendered primitive.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## Math:: mat4 getTransform ( ) const

Returns transformation matrix of the rendered primitive.
### Return value

Transformation matrix.
## void addIndex ( int index )

Adds given index to Ffp.
### Arguments

- *int* **index** - Index of a vertex.

## void addIndices ( int i0 , int i1 )

Adds two given indices to Ffp.
### Arguments

- *int* **i0** - The first index.
- *int* **i1** - The second index.

## void addIndices ( ushort* OUT_indices , int indices_size , int vertex_offset )

Adds the specified array of indices to Ffp with the specified vertex offset.
### Arguments

- *ushort** **OUT_indices** - Array of indices to be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **indices_size** - Number of elements in the array.
- *int* **vertex_offset** - Vertex offset.

## void addIndices ( ushort* OUT_indices , int indices_size )

Adds the specified array of indices to Ffp.
### Arguments

- *ushort** **OUT_indices** - Array of indices to be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **indices_size** - Number of elements in the array.

## void addIndices ( int i0 , int i1 , int i2 , int i3 )

Adds four given indices to Ffp.
### Arguments

- *int* **i0** - The first index.
- *int* **i1** - The second index.
- *int* **i2** - The third index.
- *int* **i3** - The fourth index.

## void addIndices ( int i0 , int i1 , int i2 )

Adds three given indices to Ffp.
### Arguments

- *int* **i0** - The first index.
- *int* **i1** - The second index.
- *int* **i2** - The third index.

## void addLines ( int num )

Adds a specified number of lines.
This method does not add vertices; instead, it allocates indices, for which vertices should be then created with *addVertex()*. Indices will point to vertices starting from the last added vertex.


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

Adds the specified vertex array to Ffp.
### Arguments

- *Vertex** **OUT_vertex** - Array of vertices to be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **vertex_size** - Number of vertices in the array.

## void addVertex ( const Ffp::Vertex & vertex )

Adds given vertex to Ffp.
### Arguments

- *const [Ffp::Vertex](../../../api/library/rendering/class.ffp_cpp.md#Vertex) &* **vertex** - Vertex.

## void addVertex ( float x , float y , float z = 0.0f )

Adds a vertex with given coordinates to Ffp.
### Arguments

- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.

## void beginLines ( )

Begins rendering of lines. Specify a list of vertex or index data between *beginLines()* and *endLines()*.
## void beginTriangles ( )

Begins rendering of triangles. Specify a list of primitives and vertex data between *beginTriangles()* and *endTriangles()*.
## void disable ( )

Disables Ffp rendering.
## void enable ( int mode = MODE_DEFAULT , int texture_sample = 0 )

Enables Ffp rendering.
### Arguments

- *int* **mode** - Ffp mode.
- *int* **texture_sample** - Texture sampler flag to be set. One of the *[TEXTURE_SAMPLE_*](#TEXTURE_SAMPLE_2D)* values.

## void endLines ( )

Ends rendering of lines (i.e. draws the specified lines).
## void endTriangles ( )

Ends rendering of triangles (i.e. draws the specified triangles).
## void renderScreen ( )

Renderers a full screen quad. It should be used when rendering post effects.
## void setTextureSample ( int sample )

Sets a new texture sample flag.
### Arguments

- *int* **sample** - Texture sample flag to be set, one of the *[TEXTURE_SAMPLE_*](#TEXTURE_SAMPLE_2D)* values.

## int getTextureSample ( ) const

Returns the current texture sample flag.
### Return value

Current texture sample flag used, one of the *[TEXTURE_SAMPLE_*](#TEXTURE_SAMPLE_2D)* values.
