# Unigine::MeshRender Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


**MeshRender** represents a GPU-side mesh resourse used for rendering.


The **MeshRender** class holds a precompiled mesh geometry optimized for rendering on the GPU. Unlike the **[Mesh](../../../api/library/rendering/class.mesh_usc.md)** class, which stores editable data in RAM, **MeshRender** resides in VRAM and is not intended for modifications.


## MeshRender Class

### Members

## int isLoaded () const

Returns the current value indicating if the mesh is loaded.
### Return value

Current the mesh is loaded
## void setFlags ( int flags )

Sets a new  [set of usage flags](#USAGE_DYNAMIC_VERTEX) (*USAGE_DYNAMIC_VERTEX, USAGE_DYNAMIC_INDICES, USAGE_DYNAMIC_ALL*) that control how vertex and index data are stored and accessed during rendering.
> **Notice:** These flags are only supported with **DirectX12**. When used with **Vulkan**, they are ignored and have no effect on rendering behavior.


### Arguments

- *int* **flags** - The usage flags for vertex and index memory behavior.

## int getFlags () const

Returns the current  [set of usage flags](#USAGE_DYNAMIC_VERTEX) (*USAGE_DYNAMIC_VERTEX, USAGE_DYNAMIC_INDICES, USAGE_DYNAMIC_ALL*) that control how vertex and index data are stored and accessed during rendering.
> **Notice:** These flags are only supported with **DirectX12**. When used with **Vulkan**, they are ignored and have no effect on rendering behavior.


### Return value

Current usage flags for vertex and index memory behavior.
## bool isSupportedMultiThreadedLoad () const

Returns the current support status for multi-threaded mesh loading.
This feature is considered supported if the [GPU Upload heap](../../../code/console/index.md#d3d12_gpu_upload_heap) is available or *[USAGE_DYNAMIC_ALL](#USAGE_DYNAMIC_ALL)* is enabled.


> **Notice:** This feature is supported for **DirectX 12** only.

### Return value

**true** if multi-threaded loading is enabled ; otherwise **false**.
---

## static MeshRender ( )

Constructor. Creates an empty static mesh.
## void swap ( MeshRender mesh )

Swaps all internal data between this mesh and the specified one. This includes vertices, indices, usage flags, and other relevant mesh information.
### Arguments

- *[MeshRender](../../../api/library/rendering/class.meshrender_usc.md)* **mesh** - The mesh to swap data with.

## void clear ( )

Clears the mesh (including its surfaces and bounds).
## void bind ( )

Binds the mesh data (index and vertex buffers) to the input assembler stage.
## void unbind ( )

Unbinds the mesh data (index and vertex buffers).
## int renderSurface ( int mode , int surface , int target = 0 )

Renders the surface.
### Arguments

- *int* **mode** - Rendering mode. One of the [MODE_*](#MODE_TRIANGLES) variables.
- *int* **surface** - Surface number.
- *int* **target** - Surface target number. The default value is 0.

### Return value

Number of primitives rendered. Primitive type is determined by the rendering mode.
## int renderInstancedSurface ( int mode , int num , int surface , int target = 0 )

Renders the specified number of instances of the surface.
### Arguments

- *int* **mode** - Rendering mode. One of the [MODE_*](#MODE_TRIANGLES) variables.
- *int* **num** - Number of instances to be rendered.
- *int* **surface** - Surface number.
- *int* **target** - Surface target number. The default value is 0.

### Return value

Number of primitives rendered. Primitive type is determined by the rendering mode.
## int render ( int mode , int surface = -1 , int target = 0 )

Renders the static mesh with the specified settings and mode.
### Arguments

- *int* **mode** - Rendering mode. One of the [MODE_*](#MODE_TRIANGLES) variables.
- *int* **surface** - Surface number (use -1 for all surfaces).
- *int* **target** - Surface target number. The default value is 0.

### Return value

Number of primitives rendered. Primitive type is determined by the rendering mode.
## int renderInstanced ( int mode , int num , int surface = -1 , int target = 0 )

Renders the specified number of instances of the surface.
### Arguments

- *int* **mode** - Rendering mode. One of the [MODE_*](#MODE_TRIANGLES) variables.
- *int* **num** - Number of instances to be rendered.
- *int* **surface** - Surface number (use -1 for all surfaces).
- *int* **target** - Surface target number. The default value is 0.

### Return value

Number of primitives rendered. Primitive type is determined by the rendering mode.
## int getSystemMemoryUsage ( )

Returns the current amount of system memory used by the static mesh, in bytes.
### Return value

System memory amount used by the static mesh, in bytes.
## int getVideoMemoryUsage ( )

Returns the current amount of video memory used by the static mesh.
### Return value

Video memory amount used by the static mesh, in bytes.
## void updateDebugName ( )

Updates the friendly name for GPU debugging (RenderDoc, NVIDIA Nsight).
## void setDebugName ( string name )

Sets a friendly name for GPU debugging (RenderDoc, NVIDIA Nsight). It can be used to help you determine if the corresponding object interface pointer caused the leak. Memory leaks are reported by the [debug software layer](https://docs.microsoft.com/en-us/windows/desktop/direct3d11/overviews-direct3d-11-devices-layers#debug-layer) by outputting a list of object interface pointers along with their friendly names.
### Arguments

- *string* **name** - Friendly debug name to be set.

## string getDebugName ( )

Returns the currently used friendly name for GPU debugging (RenderDoc, NVIDIA Nsight). It can be used to help you determine if the corresponding object interface pointer caused the leak. Memory leaks are reported by the [debug software layer](https://docs.microsoft.com/en-us/windows/desktop/direct3d11/overviews-direct3d-11-devices-layers#debug-layer) by outputting a list of object interface pointers along with their friendly names.
### Return value

Friendly debug name.
