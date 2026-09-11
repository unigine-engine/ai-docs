# Unigine.Ffp Class (CS)

> **Notice:** This class is a singleton.


Interface for fixed function pipeline.


Ffp class in Unigine differs from the classic OpenGL FFP implementation. For example, Unigine [Visualizer](../../../code/console/index.md#visualizer) and [Texture Buffers for Debugging](../../../code/console/index.md#render_show_textures) are implemented by using FFP. FFP uses already implemented D3D12 and Vulkan shader programs (without creating materials, etc.) to render.


This interface enables to render basic geometric primitives. For example, it can be used to draw a project watermark.


#### Usage Example


Here is an example how to render 2D texture:


```csharp
/* ... */
// begin triangles rendering
Ffp.beginTriangles();
	// add single triangle quad
	// this method creates indices
	Ffp.addTriangleQuads(1);
	// add 4 vertices and texcoords
	Ffp.addVertex(x0,y0);
	Ffp.setTexCoord(0.0f,0.0f);
	Ffp.addVertex(x1,y0);
	Ffp.setTexCoord(1.0f,0.0f);
	Ffp.addVertex(x1,y1);
	Ffp.setTexCoord(1.0f,1.0f);
	Ffp.addVertex(x0,y1);
	Ffp.setTexCoord(0.0f,1.0f);
// end of triangles rendering
Ffp.endTriangles();

```


### See Also


- C++ API sample located in the folder **<UnigineSDK>/source/samples/Api/Systems/Ffp**
- C# API sample located in the folder **<UnigineSDK>/source/csharp/samples/Api/Systems/Ffp**


## Ffp Class

### Properties

## 🔒︎ int NumIndices

The number of indices in the current primitive batch.
## 🔒︎ int NumVertex

The number of vertices in the current primitive batch.
## mat4 Transform

The Transformation matrix of the rendered primitive.
## 🔒︎ bool IsEnabled

The a value indicating if the FFP is enabled.
## int Mode

The FFP mode.
## int TextureSample

The texture sample flag.
### Members

---

## void SetColor ( uint color )


Sets rendering color for the last added vertex.


You can use [COLOR_*](#COLOR_BLACK) variables to set the color.


### Arguments

- *uint* **color** - Color in ARGB8 format: (a << 24) | (r << 16) | (g << 8) | (b << 0).

## void SetColor ( float r , float g , float b , float a )

Sets rendering color for the last added vertex.
### Arguments

- *float* **r** - Red color component.
- *float* **g** - Green color component.
- *float* **b** - Blue color component.
- *float* **a** - Alpha color component.

## void SetOrtho ( int width , int height )


Sets orthographic projection to render the primitive.


For example, the [`render_show_textures`](../../../code/console/index.md#render_show_textures) console command renders textures via FFP by using orthographic projection.


### Arguments

- *int* **width** - Primitive width.
- *int* **height** - Primitive height.

## void SetTexCoord ( float x , float y , float z = 0.0f , float w = 1.0f )

Sets texture coordinates for the last added vertex.
### Arguments

- *float* **x** - X texture coordinate.
- *float* **y** - Y texture coordinate.
- *float* **z** - Z texture coordinate.
- *float* **w** - W texture coordinate.

## void AddIndex ( int index )

Adds given index to FFP.
### Arguments

- *int* **index** - Index of a vertex.

## void AddIndices ( int i0 , int i1 )

Adds two given indices to FFP.
### Arguments

- *int* **i0** - The first index.
- *int* **i1** - The second index.

## void AddIndices ( ushort[] OUT_indices , int vertex_offset )

Adds the specified array of indices to FFP with the specified vertex offset.
### Arguments

- *ushort[]* **OUT_indices** - Array of indices to be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **vertex_offset** - Vertex offset.

## void AddIndices ( ushort[] OUT_indices )

Adds the specified array of indices to FFP.
### Arguments

- *ushort[]* **OUT_indices** - Array of indices to be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void AddIndices ( int i0 , int i1 , int i2 , int i3 )

Adds four given indices to FFP.
### Arguments

- *int* **i0** - The first index.
- *int* **i1** - The second index.
- *int* **i2** - The third index.
- *int* **i3** - The fourth index.

## void AddIndices ( int i0 , int i1 , int i2 )

Adds three given indices to FFP.
### Arguments

- *int* **i0** - The first index.
- *int* **i1** - The second index.
- *int* **i2** - The third index.

## void AddLines ( int num )

Adds a specified number of lines. This method does not add vertices; instead, it allocates indices, for which vertices should be then created with *addVertex()*. Indices will point to vertices starting from the last added vertex.
### Arguments

- *int* **num** - The number of lines.

## void AddTriangleQuads ( int num )

Adds a specified number of quads. This method does not add vertices; instead, it allocates indices, for which vertices should be then created with *addVertex()*. Indices will point to vertices starting from the last added vertex.
### Arguments

- *int* **num** - The number of quads.

## void AddTriangles ( int num )

Adds a specified number of triangles. This method does not add vertices; instead, it allocates indices, for which vertices should be then created with *addVertex()*. Indices will point to vertices starting from the last added vertex.
### Arguments

- *int* **num** - The number of triangles.

## void AddVertex ( Vertex[] OUT_vertex )

Adds the specified vertex array to FFP.
### Arguments

- *Vertex[]* **OUT_vertex** - Array of vertices to be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void AddVertex ( Vertex vertex )

Adds given vertex to FFP.
### Arguments

- *Vertex* **vertex** - Vertex.

## void AddVertex ( float x , float y , float z = 0.0f )

Adds a vertex with given coordinates to FFP.
### Arguments

- *float* **x** - X coordinate of the vertex.
- *float* **y** - Y coordinate of the vertex.
- *float* **z** - Z coordinate of the vertex.

## void BeginLines ( )

Begins rendering of lines. Specify a list of vertex or index data between *beginLines()* and *endLines()*.
## void BeginTriangles ( )

Begins rendering of triangles. Specify a list of primitives and vertex data between *beginTriangles()* and *endTriangles()*.
## void Disable ( )

Disables FFP rendering.
## void Enable ( int mode = MODE_DEFAULT , int texture_sample = 0 )

Enables FFP rendering.
### Arguments

- *int* **mode** - FFP mode.
- *int* **texture_sample** - Texture sampler flag to be set. One of the *[TEXTURE_SAMPLE_*](#TEXTURE_SAMPLE_2D)* values.

## void EndLines ( )

Ends rendering of lines (i.e. draws the specified lines).
## void EndTriangles ( )

Ends rendering of triangles (i.e. draws the specified triangles).
## void RenderScreen ( )

Renderers a full screen quad. It should be used when rendering post effects.
