# Unigine::MeshRender Class (CPP)

**Header:** #include <UnigineMeshRender.h>


**MeshRender** represents a GPU-side mesh resourse used for rendering.


The **MeshRender** class holds a precompiled mesh geometry optimized for rendering on the GPU. Unlike the **[Mesh](../../../api/library/rendering/class.mesh_cpp.md)** class, which stores editable data in RAM, **MeshRender** resides in VRAM and is not intended for modifications.


## MeshRender Class

### Members

## bool isLoaded () const

Returns the current value indicating if the mesh is loaded.
### Return value

**true** if the mesh is loaded; otherwise **false**.
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

## static MeshRenderPtr create ( )

Constructor. Creates an empty static mesh.
## bool load ( const char * path )

Loads the mesh using the specified path.
### Arguments

- *const char ** **path** - Path to the mesh.

### Return value

true if the mesh is loaded successfully; otherwise false.
## bool load ( const Ptr <ConstMesh> & mesh )

Loads the specified mesh.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<ConstMesh> &* **mesh** - The mesh to be loaded.

### Return value

true if the mesh is loaded successfully; otherwise false.
## void swap ( const Ptr < MeshRender > & mesh )

Swaps all internal data between this mesh and the specified one. This includes vertices, indices, usage flags, and other relevant mesh information.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[MeshRender](../../../api/library/rendering/class.meshrender_cpp.md)> &* **mesh** - The mesh to swap data with.

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
## size_t getSystemMemoryUsage ( ) const

Returns the current amount of system memory used by the static mesh, in bytes.
### Return value

System memory amount used by the static mesh, in bytes.
## size_t getVideoMemoryUsage ( ) const

Returns the current amount of video memory used by the static mesh.
### Return value

Video memory amount used by the static mesh, in bytes.
## void updateDebugName ( )

Updates the friendly name for GPU debugging (RenderDoc, NVIDIA Nsight).
## void setDebugName ( const char * name )

Sets a friendly name for GPU debugging (RenderDoc, NVIDIA Nsight). It can be used to help you determine if the corresponding object interface pointer caused the leak. Memory leaks are reported by the [debug software layer](https://docs.microsoft.com/en-us/windows/desktop/direct3d11/overviews-direct3d-11-devices-layers#debug-layer) by outputting a list of object interface pointers along with their friendly names.
### Arguments

- *const char ** **name** - Friendly debug name to be set.

## const char * getDebugName ( ) const

Returns the currently used friendly name for GPU debugging (RenderDoc, NVIDIA Nsight). It can be used to help you determine if the corresponding object interface pointer caused the leak. Memory leaks are reported by the [debug software layer](https://docs.microsoft.com/en-us/windows/desktop/direct3d11/overviews-direct3d-11-devices-layers#debug-layer) by outputting a list of object interface pointers along with their friendly names.
### Return value

Friendly debug name.
