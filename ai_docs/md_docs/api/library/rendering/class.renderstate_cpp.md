# Unigine.RenderState Class (CPP)

**Header:** #include <UnigineRender.h>

> **Notice:** This class is a singleton.


RenderState is a low-level GPU pipeline state abstraction that controls how rendering is performed. It manages all the settings the GPU needs before drawing: blending, depth testing, stencil operations, polygon rasterization, write masks, scissor clipping, and resource bindings (textures, structured buffers, shaders, materials).


State changes are deferred - they accumulate on the CPU side and are only sent to the GPU when explicitly flushed. The class also provides a save/restore mechanism to isolate rendering code segments from each other.


In addition to managing pipeline state, RenderState is used to submit draw calls and compute shader dispatches to the GPU.


### Usage Example


The following example illustrates the common usage of the [saveState()](#saveState_void), [clearStates()](#clearStates_int_void), [flushStates()](#flushStates_void), and [restoreState()](#restoreState_void) methods


```cpp
/* ... */

// saving the current render state
RenderState::saveState();

// clearing the current render state to prevent our rendering code from being affected by the previous settings
RenderState::clearStates();

/* ... */

// changing current render state
RenderState::setBlendFunc(RenderState::BLEND_SRC_ALPHA, RenderState::BLEND_ONE_MINUS_SRC_ALPHA );

// flushing the current render state to GPU
RenderState::flushStates();

/*	rendering code begin

...

rendering code end */

// clearing the current render state (if necessary)
RenderState::clearStates();

// changing current render state again
RenderState::setPolygonFront(1);

// flushing the current render state to GPU
RenderState::flushStates();

/*	rendering code begin

...

rendering code end */

// restoring the previously saved render state
RenderState::restoreState();

/* ... */

```


## RenderState Class

### Enums

## RENDER_MODE

| Name | Description |
|---|---|
| **RENDER_MODE_POINTS** = 0 | Mode to render points. |
| **RENDER_MODE_LINES** = 1 | Mode to render lines. |
| **RENDER_MODE_TRIANGLES** = 2 | Mode to render triangles. |
| **RENDER_MODE_TRIANGLE_PATCHES** = 3 | Mode to render triangle patches. |
| **RENDER_MODE_QUAD_PATCHES** = 4 | Mode to render quad patches. |
| **NUM_RENDER_MODES** = 5 | Number of rendering modes. |

### Members

## void setMaterial ( )

Sets a new material to be used.
### Arguments

- **material** - The material to be used.

## getMaterial () const

Returns the current material to be used.
### Return value

Current material to be used.
## void setShader ( )

Sets a new shader to be used.
### Arguments

- **shader** - The shader to be used.

## getShader () const

Returns the current shader to be used.
### Return value

Current shader to be used.
## void setAnisotropy ( )

Sets a new
texture anisotropy level (degree of anisotropic filtering). Available values:


- **0** - anisotropy level 1.
- **1** - anisotropy level 2.
- **2** - anisotropy level 4.
- **3** - anisotropy level 8.
- **4** - anisotropy level 16.


### Arguments

- **anisotropy** - The texture anisotropy level.

## getAnisotropy () const

Returns the current
texture anisotropy level (degree of anisotropic filtering). Available values:


- **0** - anisotropy level 1.
- **1** - anisotropy level 2.
- **2** - anisotropy level 4.
- **3** - anisotropy level 8.
- **4** - anisotropy level 16.


### Return value

Current texture anisotropy level.
## void setPolygonFill ( )

Sets a new polygon fill mode.
### Arguments

- **fill** - The polygon fill mode (one of the [FILL_*](#FILL_SOLID) variables).

## getPolygonFill () const

Returns the current polygon fill mode.
### Return value

Current polygon fill mode (one of the [FILL_*](#FILL_SOLID) variables).
## void setPolygonCull ( )

Sets a new polygon cull mode (one of the [CULL_*](#CULL_NONE) variables).
### Arguments

- **cull** - The polygon cull mode.

## getPolygonCull () const

Returns the current polygon cull mode (one of the [CULL_*](#CULL_NONE) variables).
### Return value

Current polygon cull mode.
## void setPolygonFront ( bool front )

Sets a new value indicating if the polygon front mode is set.
### Arguments

- *bool* **front** - Set **true** to enable polygon front mode; **false** - to disable it.

## bool getPolygonFront () const

Returns the current value indicating if the polygon front mode is set.
### Return value

**true** if polygon front mode is enabled ; otherwise **false**.
## void setDepthFunc ( )

Sets a new depth function (one of the [DEPTH_*](#DEPTH_NONE) variables).
### Arguments

- **func** - The depth function.

## getDepthFunc () const

Returns the current depth function (one of the [DEPTH_*](#DEPTH_NONE) variables).
### Return value

Current depth function.
## void setDepthWrite ( bool write )

Sets a new value indicating if writing to the depth buffer is enabled.
### Arguments

- *bool* **write** - Set **true** to enable writing to the depth buffer; **false** - to disable it.

## bool isDepthWrite () const

Returns the current value indicating if writing to the depth buffer is enabled.
### Return value

**true** if writing to the depth buffer is enabled ; otherwise **false**.
## getHeight () const

Returns the current viewport height, in pixels.
### Return value

Current viewport height, in pixels.
## getWidth () const

Returns the current viewport width, in pixels.
### Return value

Current viewport width, in pixels.
## getCoordX () const

Returns the current X-coordinate of the viewport.
### Return value

Current X-coordinate of the viewport.
## getCoordY () const

Returns the current Y-coordinate of the viewport.
### Return value

Current Y-coordinate of the viewport.
## getScreenColorTexture () const

Returns the current screen color texture.
### Return value

Current screen color texture.
## getScreenDepthTexture () const

Returns the current screen depth texture.
### Return value

Current screen depth texture.
## void setPolygonSlope ( )

Sets a new polygon slope offset.
### Arguments

- **slope** - The polygon slope offset.

## getPolygonSlope () const

Returns the current polygon slope offset.
### Return value

Current polygon slope offset.
## void setPolygonBias ( )

Sets a new polygon bias offset.
### Arguments

- **bias** - The polygon bias offset.

## getPolygonBias () const

Returns the current polygon bias offset.
### Return value

Current polygon bias offset.
## void setBlendOperation ( )

Sets a new blending operation to be used. One of the [BLEND_OP_*](#BLEND_OP_ADD) variables.
### Arguments

- **operation** - The blending operation.

## getBlendOperation () const

Returns the current blending operation to be used. One of the [BLEND_OP_*](#BLEND_OP_ADD) variables.
### Return value

Current blending operation.
## void setBlendDestFunc ( )

Sets a new destination blending function to be used. One of the [BLEND_*](#BLEND_NONE) variables.
### Arguments

- **func** - The destination blending function.

## getBlendDestFunc () const

Returns the current destination blending function to be used. One of the [BLEND_*](#BLEND_NONE) variables.
### Return value

Current destination blending function.
## void setBlendSrcFunc ( )

Sets a new source blending function to be used. One of the [BLEND_*](#BLEND_NONE) variables.
### Arguments

- **func** - The source blending function.

## getBlendSrcFunc () const

Returns the current source blending function to be used. One of the [BLEND_*](#BLEND_NONE) variables.
### Return value

Current source blending function.
## void setBlendAlphaSrcFunc ( int func )

Sets a new source blending function for the alpha channel to be used. One of the [BLEND_*](#BLEND_NONE) variables.
### Arguments

- *int* **func** - The source blending function for the alpha channel.

## int getBlendAlphaSrcFunc () const

Returns the current source blending function for the alpha channel to be used. One of the [BLEND_*](#BLEND_NONE) variables.
### Return value

Current source blending function for the alpha channel.
## void setStencilRef ( )

Sets a new stencil reference value to be used.
### Arguments

- **ref** - The stencil reference value.

## getStencilRef () const

Returns the current stencil reference value to be used.
### Return value

Current stencil reference value.
## void setStencilPass ( )

Sets a new stencil mode to be used. One of the [STENCIL_*](#STENCIL_NONE) variables.
### Arguments

- **pass** - The stencil mode.

## getStencilPass () const

Returns the current stencil mode to be used. One of the [STENCIL_*](#STENCIL_NONE) variables.
### Return value

Current stencil mode.
## void setStencilFunc ( )

Sets a new stencil function.
### Arguments

- **func** - The stencil function.

## getStencilFunc () const

Returns the current stencil function.
### Return value

Current stencil function.
## void setConservativeRasterizationEnabled ( bool enabled )

Sets a new value indicating if conservative rasterization is enabled. Conservative rasterization (alternative to normal rasterization) is a graphics rendering technique used in GPUs where a triangle (or other primitive) is rasterized in a way that guarantees any pixel even slightly touched by the primitive is considered covered. This technique is useful in a number of situations, including for certainty in collision detection, occlusion culling, and tiled rendering.
### Arguments

- *bool* **enabled** - Set **true** to enable conservative rasterization; **false** - to disable it.

## bool isConservativeRasterizationEnabled () const

Returns the current value indicating if conservative rasterization is enabled. Conservative rasterization (alternative to normal rasterization) is a graphics rendering technique used in GPUs where a triangle (or other primitive) is rasterized in a way that guarantees any pixel even slightly touched by the primitive is considered covered. This technique is useful in a number of situations, including for certainty in collision detection, occlusion culling, and tiled rendering.
### Return value

**true** if conservative rasterization is enabled ; otherwise **false**.
---

## int getBlendDestFuncBuffer ( int num ) const

Returns the destination blending function for the specified buffer.
### Arguments

- *int* **num** - Buffer number.

### Return value

Destination blending function. One of the [BLEND_*](#BLEND_NONE) variables.
## void setBlendFunc ( int src , int dest , int blend_op = 0 )

Sets the blending function for the primary render target. The final pixel color is computed by combining the source (incoming fragment) and destination (existing framebuffer) colors using the specified blend factors and operation.
### Arguments

- *int* **src** - Source blending function. One of the [BLEND_*](#BLEND_NONE) variables.
- *int* **dest** - Destination blending function. One of the [BLEND_*](#BLEND_NONE) variables.
- *int* **blend_op** - Blending operation to be used. One of the [BLEND_OP_*](#BLEND_OP_ADD) variables. [BLEND_OP_ADD](#BLEND_OP_ADD) is used by default.

## void setBlendAlphaSrcFuncBuffer ( int num , int src ) const

Sets the alpha-channel source blending function for the specified buffer.
### Arguments

- *int* **num** - Buffer number.
- *int* **src** - Source blending function for the alpha channel. One of the [BLEND_*](#BLEND_NONE) variables.

## int getBlendAlphaSrcFuncBuffer ( int num ) const

Returns the alpha-channel source blending function for the specified buffer.
### Arguments

- *int* **num** - Buffer number.

### Return value

Source blending function for the alpha channel. One of the [BLEND_*](#BLEND_NONE) variables.
## void setBlendFuncBuffer ( int num , int src , int dest , int blend_op = 0 )

Sets the blending function for a specific render target buffer. Use this method when rendering to multiple render targets (MRT) and each target requires its own blending mode.
### Arguments

- *int* **num** - Render target index.
- *int* **src** - Source blending function. One of the [BLEND_*](#BLEND_NONE) variables.
- *int* **dest** - Destination blending function. One of the [BLEND_*](#BLEND_NONE) variables.
- *int* **blend_op** - Blending operation to be used. One of the [BLEND_OP_*](#BLEND_OP_ADD) variables. [BLEND_OP_ADD](#BLEND_OP_ADD) is used by default.

## int getBlendSrcFuncBuffer ( int num ) const

Returns the source blending function for the specified buffer.
### Arguments

- *int* **num** - Buffer number.

### Return value

Source blending function. One of the [BLEND_*](#BLEND_NONE) variables.
## int getBlendOperationBuffer ( int num ) const

Returns the current blending operation for the given buffer.
### Arguments

- *int* **num** - Buffer number.

### Return value

Current blending operation for the given buffer. One of the [BLEND_OP_*](#BLEND_OP_ADD) variables.
## void setBufferMask ( int num , int mask )

Sets the write mask for the specified render target, controlling which color channels (R, G, B, A) and depth/stencil buffers can be written to.
### Arguments

- *int* **num** - Render target index.
- *int* **mask** - Combination of [BUFFER_*](#BUFFER_ALL) flags defining which channels are enabled for writing.

## int getBufferMask ( int num ) const

Returns the current write mask for the specified render target.
### Arguments

- *int* **num** - Render target index.

### Return value

Combination of [BUFFER_*](#BUFFER_ALL) flags.
## void setMaterial ( Render::PASS pass , const Ptr < Material > & material )

Sets the specified material to be used for the specified rendering pass.
### Arguments

- *[Render::PASS](../../../api/library/rendering/class.render_cpp.md#PASS)* **pass** - Rendering pass for which the material is to be set.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Material to be used.

## void setPolygonOffset ( float bias , float offset )

Sets the polygon offset (depth bias). Used to prevent z-fighting when rendering coplanar geometry, such as decals or shadow maps.
### Arguments

- *float* **bias** - Constant depth offset added to each fragment, in units of the minimum resolvable depth buffer value.
- *float* **offset** - Slope-scaled depth offset, multiplied by the maximum depth slope of the polygon.

## void setScissorTest ( float x , float y , float width , float height )

Enables the scissor test and sets the clipping rectangle. Fragments outside this rectangle are discarded. Pass zero size to disable.
### Arguments

- *float* **x** - X coordinate of the scissor rectangle's top-left corner, in pixels.
- *float* **y** - Y coordinate of the scissor rectangle's top-left corner, in pixels.
- *float* **width** - Width of the scissor rectangle, in pixels.
- *float* **height** - Height of the scissor rectangle, in pixels.

## void setScissorTest ( const Math:: ivec4 & rectangle )

Enables the scissor test and sets the clipping rectangle. Fragments outside this rectangle are discarded. Pass zero size to disable.
### Arguments

- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **rectangle** - Scissor rectangle as (x, y, width, height) in pixels.

## void setScissorTest ( const Math:: vec4 & rectangle )

Enables the scissor test and sets the clipping rectangle. Fragments outside this rectangle are discarded. Pass zero size to disable.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **rectangle** - Scissor rectangle as (x, y, width, height) in pixels.

## int getScissorTest ( ) const

Returns the current scissor test status.
### Return value

1 if scissor test is enabled; otherwise, 0.
## void setStructuredBuffer ( int slot , const Ptr < StructuredBuffer > & buffer )

Binds a *[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cpp.md)* to the specified slot in the render state, making it accessible from shaders.
### Arguments

- *int* **slot** - Buffer slot index to bind to. Each slot corresponds to a buffer register in the shader.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cpp.md)> &* **buffer** - [StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cpp.md) to bind. Pass nullptr to unbind.

## void setTexture ( int binding , int slot , const Ptr < Texture > & texture )

Binds a texture to the specified slot in the render state. Sampler flags are taken from the texture itself.
### Arguments

- *int* **binding** - Shader stages that will read the texture: *[BIND_ALL](#BIND_ALL)* for all stages (*vertex, fragment, compute*), [BIND_FRAGMENT](#BIND_FRAGMENT) for the fragment shader only. Use *BIND_FRAGMENT* when the texture is only needed in the fragment shader, as it may be more efficient.
- *int* **slot** - Texture slot index to bind the texture to. Each slot corresponds to a texture register in the shader.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Texture to bind. Pass nullptr to unbind the texture from the slot.

## void setTexture ( int binding , int slot , const Ptr < Texture > & texture , int sampler_flags )

Binds a texture to the specified slot in the render state with custom sampler flags that override the texture's own sampler settings.
### Arguments

- *int* **binding** - Shader stages that will read the texture: *[BIND_ALL](#BIND_ALL)* for all stages (*vertex, fragment, compute*), *[BIND_FRAGMENT](#BIND_FRAGMENT)* for the fragment shader only. Use *BIND_FRAGMENT* when the texture is only needed in the fragment shader, as it may be more efficient.
- *int* **slot** - Texture slot index to bind the texture to. Each slot corresponds to a texture register in the shader.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Texture to bind. Pass nullptr to unbind the texture from the slot.
- *int* **sampler_flags** - Sampler flags to use instead of the texture's own sampler settings. This lets you override filtering, wrapping, and other [sampler parameters](../../../api/library/rendering/class.texture_cpp.md#sampler_flags) without modifying the texture.

## Ptr < Texture > getTexture ( int slot ) const

Returns the texture currently bound to the given slot in the render state.
### Arguments

- *int* **slot** - Texture slot index.

### Return value

Texture currently bound to the given slot, or nullptr if the slot is empty.
## void setViewport ( int x , int y , int width , int height )

Sets the viewport size and position.
### Arguments

- *int* **x** - The X coordinate.
- *int* **y** - The Y coordinate.
- *int* **width** - The width.
- *int* **height** - The height.

## void clearBuffer ( int buffer , const Math:: vec4 & color , float depth = 0.0f , int stencil = 0 )

Clears the specified buffer.
### Arguments

- *int* **buffer** - Buffer mask determines which buffers are to be cleared. One or combination of [BUFFER_*](#BUFFER_ALL) variables. ```text clearBuffer(BUFFER_COLOR); // clears color buffer clearBuffer(BUFFER_DEPTH); // clears depth buffer clearBuffer(BUFFER_STENCIL); // clears stencil buffer //masks can be combined: clearBuffer(BUFFER_COLOR | BUFFER_STENCIL); // clears color and stencil buffer //there is a separate BUFFER_DEPTH_STENCIL mask for convenience clearBuffer(BUFFER_DEPTH_STENCIL); ```
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color value to be used.
- *float* **depth** - Depth value to be used.
- *int* **stencil** - Stencil value to be used.

## void clearStates ( bool clear_all = true )

Clears all current render states. This method is used to prevent certain rendering code segment from being affected by other segments. See the [usage example](#usage), that illustrates the typical use case.
### Arguments

- *bool* **clear_all** - Clear flag: true - to clear current shader, material, textures, and structured buffers as well, or false to clear render states only.

## void clearStructuredBuffer ( const Ptr < StructuredBuffer > & buffer )

Unbinds the specified structured buffer from all slots in the render state.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cpp.md)> &* **buffer** - *[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cpp.md)* to unbind.

## void clearStructuredBuffers ( )

Unbinds all structured buffers from the render state.
## void clearTexture ( const Ptr < Texture > & texture )

Unbinds the specified texture from all slots in the render state.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Texture to unbind.

## void clearTextures ( )

Unbinds all textures from the render state.
## void flushRender ( )

Forces a full CPU-GPU synchronization, blocking until all previously submitted GPU commands have completed. This is an expensive operation - use *[flushStates()](../../...md#flushStates_void)* to just apply state changes without waiting.
## void flushStates ( )

Flushes the current render state to GPU. See the [usage example](#usage), that illustrates the typical use case.
## void saveState ( )

Saves the current render state. This method is to be used together with the *[restoreState()](#restoreState_void)* method to enclose a segment of code, that changes the render state. See the [usage example](#usage), that illustrates the typical use case.
## void restoreState ( )

Restores the current render state, that was saved by calling the *[saveState()](#saveState_void)* method. These two methods are used together to enclose a segment of code, that changes the render state. See the [usage example](#usage), that illustrates the typical use case.
## void dispatch ( int group_threads_x , int group_threads_y , int group_threads_z )

Executes commands in a compute shader (similar to *[ID3D12GraphicsCommandList::Dispatch](https://learn.microsoft.com/en-us/windows/win32/api/d3d12/nf-d3d12-id3d12graphicscommandlist-dispatch)* or *[vkCmdDispatch](https://registry.khronos.org/vulkan/specs/latest/man/html/vkCmdDispatch.html)* method). A compute shader can be run on many threads in parallel, within a thread group. Index a particular thread, within a thread group using a 3D vector given by (x,y,z).
### Arguments

- *int* **group_threads_x** - Local X work-group size of the compute shader.
- *int* **group_threads_y** - Local Y work-group size of the compute shader.
- *int* **group_threads_z** - Local Z work-group size of the compute shader.

## int render ( RenderState::RENDER_MODE mode , int base , int begin , int end , int num )


Renders the specified number of instances of the surface defined by the begin and end indices.


> **Notice:** The **pass, material, and shader must be set** via *[Renderer::setShaderParameters()](../../../api/library/rendering/class.renderer_cpp.md#setShaderParameters_int_Shader_Material_int_void)* and/or *[Renderer::setMaterial()](../../../api/library/rendering/class.renderer_cpp.md#setMaterial_int_Material_void)* **before calling this function**. Otherwise, there won't be sufficient shader parameters for rendering.


### Arguments

- *[RenderState::RENDER_MODE](../../../api/library/rendering/class.renderstate_cpp.md#RENDER_MODE)* **mode** - Rendering mode. One of the [RENDER_MODE](#RENDER_MODE) values.
- *int* **base** - A value added to each index before reading a vertex from the vertex buffer.
- *int* **begin** - First index of the surface to be read by the GPU from the index buffer.
- *int* **end** - Last index of the surface to be read by the GPU from the index buffer.
- *int* **num** - Number of instances to be rendered.

### Return value

Number of primitives rendered. The primitive type is determined by the specified rendering mode.
## void setVertexBuffer ( int num , const Ptr < StructuredBuffer > & buffer , int offset = 0 , int num_vertex = -1 )

Sets a structured buffer to be used as a vertex buffer for subsequent rendering calls.
### Arguments

- *int* **num** - Buffer slot index.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cpp.md)> &* **buffer** - Structured buffer to be bound as a vertex buffer.
- *int* **offset** - Offset position in the buffer from which vertices are read and passed to the vertex shader.
- *int* **num_vertex** - Number of vertices to read from the buffer. If -1, the entire buffer is used.

## void setIndexBuffer ( const Ptr < StructuredBuffer > & buffer , int offset = 0 , int num_indices = -1 )

Sets a structured buffer to be used as an index buffer for subsequent rendering calls.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cpp.md)> &* **buffer** - Structured buffer to be bound as an index buffer.
- *int* **offset** - Offset position in the buffer from which indices are read.
- *int* **num_indices** - Number of indices to read from the buffer. If -1, the entire buffer is used.

## Ptr < StructuredBuffer > getStructuredBuffer ( int slot ) const

Returns the [StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cpp.md) currently bound to the given slot in the render state.
### Arguments

- *int* **slot** - StructuredBuffer unit number.

### Return value

StructuredBuffer smart pointer.
