# Unigine.RenderState Class (CS)

> **Notice:** This class is a singleton.


RenderState is a low-level GPU pipeline state abstraction that controls how rendering is performed. It manages all the settings the GPU needs before drawing: blending, depth testing, stencil operations, polygon rasterization, write masks, scissor clipping, and resource bindings (textures, structured buffers, shaders, materials).


State changes are deferred - they accumulate on the CPU side and are only sent to the GPU when explicitly flushed. The class also provides a save/restore mechanism to isolate rendering code segments from each other.


In addition to managing pipeline state, RenderState is used to submit draw calls and compute shader dispatches to the GPU.


### Usage Example


The following example illustrates the common usage of the [saveState()](#saveState_void), [clearStates()](#clearStates_int_void), [flushStates()](#flushStates_void), and [restoreState()](#restoreState_void) methods


```csharp
/* ... */

// saving the current render state
RenderState.SaveState();

// clearing the current render state to prevent our rendering code from being affected by the previous settings
RenderState.ClearStates();

/* ... */

// changing current render state
RenderState.SetBlendFunc(RenderState.BLEND_SRC_ALPHA, RenderState.BLEND_ONE_MINUS_SRC_ALPHA );

// flushing the current render state to GPU
RenderState.FlushStates();

/*	rendering code begin

...

rendering code end */

// clearing the current render state (if necessary)
RenderState.ClearStates();

// changing current render state again
RenderState.SetPolygonFront(1);

// flushing the current render state to GPU
RenderState.FlushStates();

/*	rendering code begin

...

rendering code end */

// restoring the previously saved render state
RenderState.RestoreState();

/* ... */

```


## RenderState Class

### Enums

## RENDER_MODE

| Name | Description |
|---|---|
| **POINTS** = 0 | Mode to render points. |
| **LINES** = 1 | Mode to render lines. |
| **TRIANGLES** = 2 | Mode to render triangles. |
| **TRIANGLE_PATCHES** = 3 | Mode to render triangle patches. |
| **QUAD_PATCHES** = 4 | Mode to render quad patches. |
| **NUM_RENDER_MODES** = 5 | Number of rendering modes. |

### Properties

## Material Material

The material to be used.
## Shader Shader

The shader to be used.
## int Anisotropy

The
texture anisotropy level (degree of anisotropic filtering). Available values:


- **0** - anisotropy level 1.
- **1** - anisotropy level 2.
- **2** - anisotropy level 4.
- **3** - anisotropy level 8.
- **4** - anisotropy level 16.


## int PolygonFill

The polygon fill mode.
## int PolygonCull

The polygon cull mode (one of the [CULL_*](#CULL_NONE) variables).
## bool PolygonFront

The value indicating if the polygon front mode is set.
## int DepthFunc

The depth function (one of the [DEPTH_*](#DEPTH_NONE) variables).
## bool DepthWrite

The value indicating if writing to the depth buffer is enabled.
## 🔒︎ int Height

The viewport height, in pixels.
## 🔒︎ int Width

The viewport width, in pixels.
## 🔒︎ int CoordX

The X-coordinate of the viewport.
## 🔒︎ int CoordY

The Y-coordinate of the viewport.
## 🔒︎ Texture ScreenColorTexture

The screen color texture.
## 🔒︎ Texture ScreenDepthTexture

The screen depth texture.
## float PolygonSlope

The polygon slope offset.
## float PolygonBias

The polygon bias offset.
## int BlendOperation

The blending operation to be used. One of the [BLEND_OP_*](#BLEND_OP_ADD) variables.
## int BlendDestFunc

The destination blending function to be used. One of the [BLEND_*](#BLEND_NONE) variables.
## int BlendSrcFunc

The source blending function to be used. One of the [BLEND_*](#BLEND_NONE) variables.
## int BlendAlphaSrcFunc

The source blending function for the alpha channel to be used. One of the [BLEND_*](#BLEND_NONE) variables.
## int StencilRef

The stencil reference value to be used.
## int StencilPass

The stencil mode to be used. One of the [STENCIL_*](#STENCIL_NONE) variables.
## int StencilFunc

The stencil function.
## bool ConservativeRasterizationEnabled

The value indicating if conservative rasterization is enabled. Conservative rasterization (alternative to normal rasterization) is a graphics rendering technique used in GPUs where a triangle (or other primitive) is rasterized in a way that guarantees any pixel even slightly touched by the primitive is considered covered. This technique is useful in a number of situations, including for certainty in collision detection, occlusion culling, and tiled rendering.
### Members

---

## int GetBlendDestFuncBuffer ( int num )

Returns the destination blending function for the specified buffer.
### Arguments

- *int* **num** - Buffer number.

### Return value

Destination blending function. One of the [BLEND_*](#BLEND_NONE) variables.
## void SetBlendFunc ( int src , int dest , int blend_op = 0 )

Sets the blending function for the primary render target. The final pixel color is computed by combining the source (incoming fragment) and destination (existing framebuffer) colors using the specified blend factors and operation.
### Arguments

- *int* **src** - Source blending function. One of the [BLEND_*](#BLEND_NONE) variables.
- *int* **dest** - Destination blending function. One of the [BLEND_*](#BLEND_NONE) variables.
- *int* **blend_op** - Blending operation to be used. One of the [BLEND_OP_*](#BLEND_OP_ADD) variables. [BLEND_OP_ADD](#BLEND_OP_ADD) is used by default.

## void SetBlendAlphaSrcFuncBuffer ( int num , int src )

Sets the alpha-channel source blending function for the specified buffer.
### Arguments

- *int* **num** - Buffer number.
- *int* **src** - Source blending function for the alpha channel. One of the [BLEND_*](#BLEND_NONE) variables.

## int GetBlendAlphaSrcFuncBuffer ( int num )

Returns the alpha-channel source blending function for the specified buffer.
### Arguments

- *int* **num** - Buffer number.

### Return value

Source blending function for the alpha channel. One of the [BLEND_*](#BLEND_NONE) variables.
## void SetBlendFuncBuffer ( int num , int src , int dest , int blend_op = 0 )

Sets the blending function for a specific render target buffer. Use this method when rendering to multiple render targets (MRT) and each target requires its own blending mode.
### Arguments

- *int* **num** - Render target index.
- *int* **src** - Source blending function. One of the [BLEND_*](#BLEND_NONE) variables.
- *int* **dest** - Destination blending function. One of the [BLEND_*](#BLEND_NONE) variables.
- *int* **blend_op** - Blending operation to be used. One of the [BLEND_OP_*](#BLEND_OP_ADD) variables. [BLEND_OP_ADD](#BLEND_OP_ADD) is used by default.

## int GetBlendSrcFuncBuffer ( int num )

Returns the source blending function for the specified buffer.
### Arguments

- *int* **num** - Buffer number.

### Return value

Source blending function. One of the [BLEND_*](#BLEND_NONE) variables.
## int GetBlendOperationBuffer ( int num )

Returns the current blending operation for the given buffer.
### Arguments

- *int* **num** - Buffer number.

### Return value

Current blending operation for the given buffer. One of the [BLEND_OP_*](#BLEND_OP_ADD) variables.
## void SetBufferMask ( int num , int mask )

Sets the write mask for the specified render target, controlling which color channels (R, G, B, A) and depth/stencil buffers can be written to.
### Arguments

- *int* **num** - Render target index.
- *int* **mask** - Combination of [BUFFER_*](#BUFFER_ALL) flags defining which channels are enabled for writing.

## int GetBufferMask ( int num )

Returns the current write mask for the specified render target.
### Arguments

- *int* **num** - Render target index.

### Return value

Combination of [BUFFER_*](#BUFFER_ALL) flags.
## void SetMaterial ( Render.PASS pass , Material material )

Sets the specified material to be used for the specified rendering pass.
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass for which the material is to be set.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Material to be used.

## void SetPolygonOffset ( float bias , float offset )

Sets the polygon offset (depth bias). Used to prevent z-fighting when rendering coplanar geometry, such as decals or shadow maps.
### Arguments

- *float* **bias** - Constant depth offset added to each fragment, in units of the minimum resolvable depth buffer value.
- *float* **offset** - Slope-scaled depth offset, multiplied by the maximum depth slope of the polygon.

## void SetScissorTest ( float x , float y , float width , float height )

Enables the scissor test and sets the clipping rectangle. Fragments outside this rectangle are discarded. Pass zero size to disable.
### Arguments

- *float* **x** - X coordinate of the scissor rectangle's top-left corner, in pixels.
- *float* **y** - Y coordinate of the scissor rectangle's top-left corner, in pixels.
- *float* **width** - Width of the scissor rectangle, in pixels.
- *float* **height** - Height of the scissor rectangle, in pixels.

## void SetScissorTest ( ivec4 rectangle )

Enables the scissor test and sets the clipping rectangle. Fragments outside this rectangle are discarded. Pass zero size to disable.
### Arguments

- *ivec4* **rectangle** - Scissor rectangle as (x, y, width, height) in pixels.

## void SetScissorTest ( vec4 rectangle )

Enables the scissor test and sets the clipping rectangle. Fragments outside this rectangle are discarded. Pass zero size to disable.
### Arguments

- *vec4* **rectangle** - Scissor rectangle as (x, y, width, height) in pixels.

## int GetScissorTest ( )

Returns the current scissor test status.
### Return value

1 if scissor test is enabled; otherwise, 0.
## void SetStructuredBuffer ( int slot , StructuredBuffer buffer )

Binds a *[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cs.md)* to the specified slot in the render state, making it accessible from shaders.
### Arguments

- *int* **slot** - Buffer slot index to bind to. Each slot corresponds to a buffer register in the shader.
- *[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cs.md)* **buffer** - [StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cs.md) to bind. Pass nullptr to unbind.

## void SetTexture ( int binding , int slot , Texture texture )

Binds a texture to the specified slot in the render state. Sampler flags are taken from the texture itself.
### Arguments

- *int* **binding** - Shader stages that will read the texture: *[BIND_ALL](#BIND_ALL)* for all stages (*vertex, fragment, compute*), [BIND_FRAGMENT](#BIND_FRAGMENT) for the fragment shader only. Use *BIND_FRAGMENT* when the texture is only needed in the fragment shader, as it may be more efficient.
- *int* **slot** - Texture slot index to bind the texture to. Each slot corresponds to a texture register in the shader.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Texture to bind. Pass nullptr to unbind the texture from the slot.

## void SetTexture ( int binding , int slot , Texture texture , int sampler_flags )

Binds a texture to the specified slot in the render state with custom sampler flags that override the texture's own sampler settings.
### Arguments

- *int* **binding** - Shader stages that will read the texture: *[BIND_ALL](#BIND_ALL)* for all stages (*vertex, fragment, compute*), *[BIND_FRAGMENT](#BIND_FRAGMENT)* for the fragment shader only. Use *BIND_FRAGMENT* when the texture is only needed in the fragment shader, as it may be more efficient.
- *int* **slot** - Texture slot index to bind the texture to. Each slot corresponds to a texture register in the shader.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Texture to bind. Pass nullptr to unbind the texture from the slot.
- *int* **sampler_flags** - Sampler flags to use instead of the texture's own sampler settings. This lets you override filtering, wrapping, and other [sampler parameters](../../../api/library/rendering/class.texture_cs.md#sampler_flags) without modifying the texture.

## Texture GetTexture ( int slot )

Returns the texture currently bound to the given slot in the render state.
### Arguments

- *int* **slot** - Texture slot index.

### Return value

Texture currently bound to the given slot, or nullptr if the slot is empty.
## void SetViewport ( int x , int y , int width , int height )

Sets the viewport size and position.
### Arguments

- *int* **x** - The X coordinate.
- *int* **y** - The Y coordinate.
- *int* **width** - The width.
- *int* **height** - The height.

## void ClearBuffer ( int buffer , vec4 color , float depth = 0.0f , int stencil = 0 )

Clears the specified buffer.
### Arguments

- *int* **buffer** - Buffer mask determines which buffers are to be cleared. One or combination of [BUFFER_*](#BUFFER_ALL) variables. ```text clearBuffer(BUFFER_COLOR); // clears color buffer clearBuffer(BUFFER_DEPTH); // clears depth buffer clearBuffer(BUFFER_STENCIL); // clears stencil buffer //masks can be combined: clearBuffer(BUFFER_COLOR | BUFFER_STENCIL); // clears color and stencil buffer //there is a separate BUFFER_DEPTH_STENCIL mask for convenience clearBuffer(BUFFER_DEPTH_STENCIL); ```
- *vec4* **color** - Color value to be used.
- *float* **depth** - Depth value to be used.
- *int* **stencil** - Stencil value to be used.

## void ClearStates ( bool clear_all = true )

Clears all current render states. This method is used to prevent certain rendering code segment from being affected by other segments. See the [usage example](#usage), that illustrates the typical use case.
### Arguments

- *bool* **clear_all** - Clear flag: true - to clear current shader, material, textures, and structured buffers as well, or false to clear render states only.

## void ClearStructuredBuffer ( StructuredBuffer buffer )

Unbinds the specified structured buffer from all slots in the render state.
### Arguments

- *[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cs.md)* **buffer** - *[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cs.md)* to unbind.

## void ClearStructuredBuffers ( )

Unbinds all structured buffers from the render state.
## void ClearTexture ( Texture texture )

Unbinds the specified texture from all slots in the render state.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Texture to unbind.

## void ClearTextures ( )

Unbinds all textures from the render state.
## void FlushRender ( )

Forces a full CPU-GPU synchronization, blocking until all previously submitted GPU commands have completed. This is an expensive operation - use *[FlushStates()](../../...md#flushStates_void)* to just apply state changes without waiting.
## void FlushStates ( )

Flushes the current render state to GPU. See the [usage example](#usage), that illustrates the typical use case.
## void SaveState ( )

Saves the current render state. This method is to be used together with the *[restoreState()](#restoreState_void)* method to enclose a segment of code, that changes the render state. See the [usage example](#usage), that illustrates the typical use case.
## void RestoreState ( )

Restores the current render state, that was saved by calling the *[saveState()](#saveState_void)* method. These two methods are used together to enclose a segment of code, that changes the render state. See the [usage example](#usage), that illustrates the typical use case.
## void Dispatch ( int group_threads_x , int group_threads_y , int group_threads_z )

Executes commands in a compute shader (similar to *[ID3D12GraphicsCommandList::Dispatch](https://learn.microsoft.com/en-us/windows/win32/api/d3d12/nf-d3d12-id3d12graphicscommandlist-dispatch)* or *[vkCmdDispatch](https://registry.khronos.org/vulkan/specs/latest/man/html/vkCmdDispatch.html)* method). A compute shader can be run on many threads in parallel, within a thread group. Index a particular thread, within a thread group using a 3D vector given by (x,y,z).
### Arguments

- *int* **group_threads_x** - Local X work-group size of the compute shader.
- *int* **group_threads_y** - Local Y work-group size of the compute shader.
- *int* **group_threads_z** - Local Z work-group size of the compute shader.

## int Render ( RenderState.RENDER_MODE mode , int base , int begin , int end , int num )


Renders the specified number of instances of the surface defined by the begin and end indices.


> **Notice:** The **pass, material, and shader must be set** via *[Renderer.SetShaderParameters()](../../../api/library/rendering/class.renderer_cs.md#setShaderParameters_int_Shader_Material_int_void)* and/or *[Renderer.SetMaterial()](../../../api/library/rendering/class.renderer_cs.md#setMaterial_int_Material_void)* **before calling this function**. Otherwise, there won't be sufficient shader parameters for rendering.


### Arguments

- *[RenderState.RENDER_MODE](../../../api/library/rendering/class.renderstate_cs.md#RENDER_MODE)* **mode** - Rendering mode. One of the [RENDER_MODE](#RENDER_MODE) values.
- *int* **base** - A value added to each index before reading a vertex from the vertex buffer.
- *int* **begin** - First index of the surface to be read by the GPU from the index buffer.
- *int* **end** - Last index of the surface to be read by the GPU from the index buffer.
- *int* **num** - Number of instances to be rendered.

### Return value

Number of primitives rendered. The primitive type is determined by the specified rendering mode.
## void SetVertexBuffer ( int num , StructuredBuffer buffer , int offset = 0 , int num_vertex = -1 )

Sets a structured buffer to be used as a vertex buffer for subsequent rendering calls.
### Arguments

- *int* **num** - Buffer slot index.
- *[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cs.md)* **buffer** - Structured buffer to be bound as a vertex buffer.
- *int* **offset** - Offset position in the buffer from which vertices are read and passed to the vertex shader.
- *int* **num_vertex** - Number of vertices to read from the buffer. If -1, the entire buffer is used.

## void SetIndexBuffer ( StructuredBuffer buffer , int offset = 0 , int num_indices = -1 )

Sets a structured buffer to be used as an index buffer for subsequent rendering calls.
### Arguments

- *[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cs.md)* **buffer** - Structured buffer to be bound as an index buffer.
- *int* **offset** - Offset position in the buffer from which indices are read.
- *int* **num_indices** - Number of indices to read from the buffer. If -1, the entire buffer is used.

## StructuredBuffer GetStructuredBuffer ( int slot )

Returns the [StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cs.md) currently bound to the given slot in the render state.
### Arguments

- *int* **slot** - StructuredBuffer unit number.

### Return value

StructuredBuffer.
