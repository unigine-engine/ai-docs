# Unigine::MeshRender Class (CS)


**MeshRender** represents a GPU-side mesh resourse used for rendering.


The **MeshRender** class holds a precompiled mesh geometry optimized for rendering on the GPU. Unlike the **[Mesh](../../../api/library/rendering/class.mesh_cs.md)** class, which stores editable data in RAM, **MeshRender** resides in VRAM and is not intended for modifications.


## MeshRender Class

### Properties

## 🔒︎ bool IsLoaded

The value indicating if the mesh is loaded.
## int Flags

The  [set of usage flags](#USAGE_DYNAMIC_VERTEX) (*USAGE_DYNAMIC_VERTEX, USAGE_DYNAMIC_INDICES, USAGE_DYNAMIC_ALL*) that control how vertex and index data are stored and accessed during rendering.
> **Notice:** These flags are only supported with **DirectX12**. When used with **Vulkan**, they are ignored and have no effect on rendering behavior.


## 🔒︎ bool IsSupportedMultiThreadedLoad

The support status for multi-threaded mesh loading.
This feature is considered supported if the [GPU Upload heap](../../../code/console/index.md#d3d12_gpu_upload_heap) is available or *[USAGE_DYNAMIC_ALL](#USAGE_DYNAMIC_ALL)* is enabled.


> **Notice:** This feature is supported for **DirectX 12** only.

### Members

---

## MeshRender ( )

Constructor. Creates an empty static mesh.
## bool Load ( string path )

Loads the mesh using the specified path.
### Arguments

- *string* **path** - Path to the mesh.

### Return value

true if the mesh is loaded successfully; otherwise false.
## bool Load ( Mesh mesh )

Loads the specified mesh.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - The mesh to be loaded.

### Return value

true if the mesh is loaded successfully; otherwise false.
## void Swap ( MeshRender mesh )

Swaps all internal data between this mesh and the specified one. This includes vertices, indices, usage flags, and other relevant mesh information.
### Arguments

- *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)* **mesh** - The mesh to swap data with.

## void Clear ( )

Clears the mesh (including its surfaces and bounds).
## void Bind ( )

Binds the mesh data (index and vertex buffers) to the input assembler stage.
## void Unbind ( )

Unbinds the mesh data (index and vertex buffers).
## int RenderSurface ( int mode , int surface , int target = 0 )

Renders the surface.
### Arguments

- *int* **mode** - Rendering mode. One of the [MODE_*](#MODE_TRIANGLES) variables.
- *int* **surface** - Surface number.
- *int* **target** - Surface target number. The default value is 0.

### Return value

Number of primitives rendered. Primitive type is determined by the rendering mode.
## int RenderInstancedSurface ( int mode , int num , int surface , int target = 0 )

Renders the specified number of instances of the surface.
### Arguments

- *int* **mode** - Rendering mode. One of the [MODE_*](#MODE_TRIANGLES) variables.
- *int* **num** - Number of instances to be rendered.
- *int* **surface** - Surface number.
- *int* **target** - Surface target number. The default value is 0.

### Return value

Number of primitives rendered. Primitive type is determined by the rendering mode.
## int Render ( int mode , int surface = -1 , int target = 0 )

Renders the static mesh with the specified settings and mode.
### Arguments

- *int* **mode** - Rendering mode. One of the [MODE_*](#MODE_TRIANGLES) variables.
- *int* **surface** - Surface number (use -1 for all surfaces).
- *int* **target** - Surface target number. The default value is 0.

### Return value

Number of primitives rendered. Primitive type is determined by the rendering mode.
## int RenderInstanced ( int mode , int num , int surface = -1 , int target = 0 )

Renders the specified number of instances of the surface.
### Arguments

- *int* **mode** - Rendering mode. One of the [MODE_*](#MODE_TRIANGLES) variables.
- *int* **num** - Number of instances to be rendered.
- *int* **surface** - Surface number (use -1 for all surfaces).
- *int* **target** - Surface target number. The default value is 0.

### Return value

Number of primitives rendered. Primitive type is determined by the rendering mode.
## ulong GetSystemMemoryUsage ( )

Returns the current amount of system memory used by the static mesh, in bytes.
### Return value

System memory amount used by the static mesh, in bytes.
## ulong GetVideoMemoryUsage ( )

Returns the current amount of video memory used by the static mesh.
### Return value

Video memory amount used by the static mesh, in bytes.
## void UpdateDebugName ( )

Updates the friendly name for GPU debugging (RenderDoc, NVIDIA Nsight).
## void SetDebugName ( string name )

Sets a friendly name for GPU debugging (RenderDoc, NVIDIA Nsight). It can be used to help you determine if the corresponding object interface pointer caused the leak. Memory leaks are reported by the [debug software layer](https://docs.microsoft.com/en-us/windows/desktop/direct3d11/overviews-direct3d-11-devices-layers#debug-layer) by outputting a list of object interface pointers along with their friendly names.
### Arguments

- *string* **name** - Friendly debug name to be set.

## string GetDebugName ( )

Returns the currently used friendly name for GPU debugging (RenderDoc, NVIDIA Nsight). It can be used to help you determine if the corresponding object interface pointer caused the leak. Memory leaks are reported by the [debug software layer](https://docs.microsoft.com/en-us/windows/desktop/direct3d11/overviews-direct3d-11-devices-layers#debug-layer) by outputting a list of object interface pointers along with their friendly names.
### Return value

Friendly debug name.
