# Unigine.DecalMesh Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Decal


This class describes how to create and modify [mesh decals](../../../objects/decals/mesh/index.md).


### Creating a Mesh Decal


The following code illustrates how to create a mesh decal, set its parameters and add the node to UnigineEditor.


```cpp
#include <core/unigine.h>

int init() {

	DecalMesh decal_mesh;

	// create a mesh
	Mesh mesh = new Mesh();
	mesh.addBoxSurface("box_0", vec3(1.0f));

	// create a mesh decal using created mesh and setting its radius to 10, material to "decal_base_0"
	decal_mesh = new DecalMesh();
	decal_mesh.setMesh(mesh);
	decal_mesh.setRadius(10.0f);
	decal_mesh.setMaterialPath("decal_base_0.mat");

	// set the name and position of the decal
	decal_mesh.setName("Mesh Decal");
    decal_mesh.setWorldPosition(vec3(0.0f, 0.0f, 5.0f));

	return 1;
}

```


## DecalMesh Class

### Members

---

## static DecalMesh ( )

Constructor. Creates a new *Mesh Decal*.
## static DecalMesh ( string path )

DecalMesh constructor. Creates a *Mesh Decal* with a source mesh loaded from the specified file.
### Arguments

- *string* **path** - Path to the source mesh file.

## void setMeshPath ( string path )

Sets a new path to the source mesh for the current decal mesh. If the mesh is in the procedural mode, it will be reset.
> **Notice:** The mesh should contain a single surface. In case if the mesh contains several surfaces, only the one with the 0 index will be used. Thus, the area of the decal will differ from the initial mesh.


### Arguments

- *string* **path** - New path to the source *.mesh*-file to be set.

## string getMeshPath ( )

Returns the path to the source *.mesh*-file currently used for the decal.
### Return value

Path to the source *.mesh*-file.
## static int type ( )

Returns a DecalMesh type identifier.
### Return value

Type identifier.
## ConstMesh getMeshCurrentRAM ( )

### Return value

A current source mesh used for the object.
## MeshRender getMeshCurrentVRAM ( )

Returns the current render mesh used for the object and loaded to video memory (VRAM).
### Return value

A current render mesh used for the object.
## ConstMesh getMeshForceRAM ( )

### Return value

A source mesh used for the object.
## MeshRender getMeshForceVRAM ( )

Returns the render mesh used for the object and loads it to video memory (VRAM) immediately. At that, the static mesh will also be loaded to memory (RAM).
> **Notice:** Loading to VRAM must be performed in the main thread only.


### Return value

A render mesh used for the object.
## ConstMesh getMeshAsyncRAM ( )

### Return value

A source mesh used for the object.
## MeshRender getMeshAsyncVRAM ( )

**[ Main Thread ]**Returns the render mesh used for the object and loads it to video memory (VRAM) asynchronously. At that, the static mesh will also be loaded to memory (RAM).
> **Notice:** Loading to VRAM must be performed in the main thread only.


### Return value

A render mesh used for the object.
## Mesh getMeshDynamicRAM ( )

Returns the procedural source mesh associated with the object and ensures it is loaded into system memory (RAM). This method is only available when the mesh is in the **dynamic** (*[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_usc.md#PROCEDURAL_MODE_DYNAMIC)*) mode. A *procedural mesh* is a mesh created via code and uses a specific streaming mode. In *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_usc.md#PROCEDURAL_MODE_DYNAMIC)*, the object stays in memory after creation and is only unloaded manually using *[deleteDynamicMesh()](../../../api/library/objects/class.objectmeshstatic_usc.md#deleteDynamicMesh_int)* or when the procedural mode is changed.
> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Return value

A procedural source mesh used for the object.
## MeshRender getMeshDynamicVRAM ( )

Returns the procedural render mesh associated with the object and ensures it is loaded into video memory (VRAM). This method is only available when the mesh is in the **dynamic** (*[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_usc.md#PROCEDURAL_MODE_DYNAMIC)*) mode. A *procedural mesh* is a mesh created via code and uses a specific streaming mode. In *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_usc.md#PROCEDURAL_MODE_DYNAMIC)*, the object stays in memory after creation and is only unloaded manually using *[deleteDynamicMesh()](../../../api/library/objects/class.objectmeshstatic_usc.md#deleteDynamicMesh_int)* or when the procedural mode is changed.
> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Return value

A procedural render mesh used for the object.
## int loadAsyncVRAM ( )

**[ Main Thread ]**Asynchronously loads the mesh to video memory (VRAM) if the [async streaming mode for meshes](../../../api/library/rendering/class.render_usc.md#STREAMING_MODE) is enabled. Otherwise, the [forced](#loadForceVRAM_bool) loading is performed. This method is recommended for implementing your own prefetch system (i.e. asynchronous pre-loading of meshes to video memory before they are used).
> **Notice:** Loading to VRAM must be performed in the main thread only.


### Return value

**1** if the mesh is loaded successfully, otherwise **0**. If the mesh is already loaded to VRAM, **1** will be returned.
## int loadAsyncRAM ( )

Asynchronously loads the mesh to memory (RAM) if the [async streaming mode for meshes](../../../api/library/rendering/class.render_usc.md#STREAMING_MODE) is enabled. Otherwise, the [forced](#loadForceRAM_bool) loading is performed. This method is recommended for implementing your own prefetch system (i.e. asynchronous pre-loading of meshes to video memory before they are used).
### Return value

**1** if the mesh is loaded successfully, otherwise **0**. If the mesh is already loaded to RAM, **1** will be returned.
## int loadForceVRAM ( )

Performs force-loading of the mesh to video memory (VRAM) immediately. The forced loading to VRAM is performed in the main thread.
> **Notice:** Loading to VRAM must be performed in the main thread only.


### Return value

**1** if the mesh is loaded successfully, otherwise **0**. If the mesh is already loaded to VRAM, **1** will be returned.
## int loadForceRAM ( )

Performs force-loading of the mesh to memory (RAM) immediately.
### Return value

**1** if the mesh is loaded successfully, otherwise **0**. If the mesh is already loaded to RAM, **1** will be returned.
## void setMeshProceduralMode ( int mode , int mesh_render_flags = 0 )

Sets the procedural mode for the mesh. The specified mode defines how procedural data is stored, updated, and unloaded.
> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *int* **mode** - One of the *[PROCEDURAL_MODE](../../../api/library/objects/class.objectmeshstatic_usc.md#PROCEDURAL_MODE)* to apply to the mesh.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_usc.md#USAGE_DYNAMIC_VERTEX) that control how vertex and index data are stored for the mesh render.

## int getMeshProceduralMode ( )

Returns a value indicating which procedural mode assigned to the mesh. The value corresponds to one of the available *[PROCEDURAL_MODE](../../../api/library/objects/class.objectmeshstatic_usc.md#PROCEDURAL_MODE)* types, determining how procedural data is stored, updated, and unloaded.
> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Return value

Current procedural mode of the mesh.
## int isMeshNull ( )

Returns a value indicating if the source mesh used for the object is null (does not exist, unassigned, not loaded, etc.).
### Return value

**1** if the source mesh used for the object is null; otherwise, **0**.
## int isMeshLoadedRAM ( )

Returns a value indicating if the source mesh used for the object is loaded to memory (RAM).
### Return value

**1** if the source mesh used for the object is loaded to RAM; otherwise, **0**.
## int isMeshLoadedVRAM ( )

Returns a value indicating if the source mesh used for the object is loaded to video memory (VRAM).
### Return value

**1** if the source mesh used for the object is loaded to VRAM; otherwise, **0**.
## int getStatDrawCalls ( )

Returns the number of draw calls (DIP) for the decal during the last frame.
### Return value

Number of draw calls (DIP) for the decal during the last frame.
## int getStatDrawCountViewport ( )

Returns the number of times the decal was drawn in the viewport last frame.
### Return value

Number of times the decal was drawn in the viewport last frame.
## int getStatDrawCountReflection ( )

Returns the number of times the decal was drawn during reflections rendering in the last frame.
### Return value

Number of times the decal was drawn during rendering in the last frame.
## int getStatDrawCountShadow ( )

Returns the number of times the decal was drawn during shadows rendering in the last frame.
### Return value

Number of times the decal was drawn during shadows rendering in the last frame.
## long getStatFrame ( )

Returns the number of [Engine frame](../../../api/library/engine/class.engine_usc.md#getFrame_int64_t), in which the decal was drawn last time.
### Return value

Number of frame, in which the decal was drawn last time.
## Mesh createCopyMeshRAM ( )

Creates and returns a copy of the source mesh used by the object, loading it directly from disk if it is not present in cache. This method does not stream the copied mesh into memory cache, resulting in lower RAM usage.
### Return value

A copy of the source mesh, or nullptr if source mesh is not presented in RAM or its file path is invalid.
## int getCopyMeshRAM ( Mesh & result )

Retrieves a copy of the source mesh used by the object and writes it to the provided mesh object. If the mesh is not present in cache, it is loaded directly from disk. This method does not stream the copied mesh into memory cache, resulting in lower RAM usage.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md) &* **result** - Object that will receive a copy of the source mesh.

### Return value

true if the mesh was copied successfully, false if source mesh is not present in RAM or its file path is invalid.
## int applyCopyMeshProceduralForce ( ConstMesh mesh , int mesh_render_flags = 0 )

**[ Main Thread ]**
Copies all vertex data from the given mesh into the object's procedural mesh forcibly, executing the operation immediately. Works only when **procedural mode is enabled**.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *ConstMesh* **mesh** - Source mesh to copy vertex data from.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_usc.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_usc.md)*.

### Return value

true if the mesh was copied successfully, otherwise false.
## int applyMoveMeshProceduralForce ( Mesh mesh , int mesh_render_flags = 0 )

**[ Main Thread ]**
Moves all vertex data from the given mesh into the object's procedural mesh forcibly, executing the operation immediately without memory allocation and data copying (move semantics). Works only when **procedural mode is enabled**.


In *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_usc.md#PROCEDURAL_MODE_DYNAMIC)*, this method behaves identically to its asynchronous variant.


This operation **swaps the object's mesh data with the given mesh**. When reusing the same mesh object for further data generation, ensure that its internal state (e.g. number of surfaces) is valid.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **mesh** - Source mesh to move vertex data from.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_usc.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_usc.md)*.

### Return value

true if the mesh was moved (transferred without copying) successfully, otherwise false.
## int applyCopyMeshProceduralAsync ( ConstMesh mesh , int mesh_render_flags = 0 )

**[ Main Thread ]**
Copies all vertex data from the given mesh into the object's procedural mesh asynchronously. The operation is not forced and is executed in the background with no noticeable delay. Works only when **procedural mode is enabled**.


In *[PROCEDURAL_MODE_FILE](../../../api/library/objects/class.objectmeshstatic_usc.md#PROCEDURAL_MODE_FILE)* and *[PROCEDURAL_MODE_BLOB](../../../api/library/objects/class.objectmeshstatic_usc.md#PROCEDURAL_MODE_BLOB)*, this method performs faster compared to the forced variant, as file writes and memory operations are offloaded to background threads.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *ConstMesh* **mesh** - Source mesh to copy vertex data from.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_usc.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_usc.md)*.

### Return value

true if the mesh was copied successfully, otherwise false.
## int applyMoveMeshProceduralAsync ( Mesh mesh , int mesh_render_flags = 0 )

**[ Main Thread ]**
Moves all vertex data from the given mesh into the object's procedural mesh asynchronously. The operation is not forced and is executed in the background with no noticeable delay, without memory allocation and data copying (move semantics). Works only when **procedural mode is enabled**.


In *[PROCEDURAL_MODE_FILE](../../../api/library/objects/class.objectmeshstatic_usc.md#PROCEDURAL_MODE_FILE)* and *[PROCEDURAL_MODE_BLOB](../../../api/library/objects/class.objectmeshstatic_usc.md#PROCEDURAL_MODE_BLOB)*, this method performs faster compared to the forced variant, as file writes and memory operations are offloaded to background threads.


This operation **swaps the object's mesh data with the given mesh**. When reusing the same mesh object for further data generation, ensure that its internal state (e.g. number of surfaces) is valid.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **mesh** - Source mesh to copy vertex data from.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_usc.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_usc.md)*.

## int deleteDynamicMesh ( )

**[ Main Thread ]**
Releases all memory used by the procedural mesh, including both VRAM and RAM. Works only when procedural mode is set to *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_usc.md#PROCEDURAL_MODE_DYNAMIC)*.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Return value

true if the memory was released successfully, otherwise false.
## int runGenerateMeshProceduralAsync ( GenerateMeshProcedural callback_generate , int mesh_render_flags = 0 )

**[ Main Thread ]**
Starts asynchronous generation of procedural mesh data. The *callback_generate* function is executed in a background thread and must create and fill a mesh object with new data. The generated mesh will be transferred to the object once complete, without blocking the main thread. Works only when **procedural mode is enabled**.


Note that the callback is executed in a single dedicated thread controlled by the engine, it is not parallelized and must not spawn additional threads.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *GenerateMeshProcedural* **callback_generate** -  Callback function responsible for creating and filling the source mesh. Executed in the main thread. The function must have the following signature: ```csharp void GenerateMeshProcedural(Mesh mesh) ```
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_usc.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_usc.md)*.

### Return value

true if the modification was completed and applied successfully, otherwise false
## int runGenerateMeshProceduralAsync ( GenerateMeshProcedural callback_generate , DoneMeshProcedural callback_done , int mesh_render_flags = 0 )

**[ Main Thread ]**
Starts asynchronous generation of procedural mesh data. The *callback_generate* function is executed in a background thread and must create and fill a mesh object with new data. The generated mesh will be transferred to the object once complete, without blocking the main thread. After the mesh has been applied to the object, the optional callback_done will be called. Works only when **procedural mode is enabled**.


Note that the callback is executed in a single dedicated thread controlled by the engine, it is not parallelized and must not spawn additional threads.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *GenerateMeshProcedural* **callback_generate** -  Callback function responsible for creating and filling the source mesh. Executed in the main thread. The function must have the following signature: ```csharp void GenerateMeshProcedural(Mesh mesh) ```
- *DoneMeshProcedural* **callback_done** -  Optional callback executed after geometry has been fully applied. The function must have the following signature: ```csharp void DoneMeshProcedural() ```
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_usc.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_usc.md)*.

### Return value

true if the generation was completed and applied successfully, otherwise false
## int runGenerateMeshProceduralForce ( GenerateMeshProcedural callback_generate , int mesh_render_flags = 0 )

**[ Main Thread ]**
Starts immediate (forced) generation of procedural mesh data. The *callback_generate* function is executed in the main thread and must create and fill a mesh object with new data. The generated mesh is applied to the object as soon as generation completes. Works only when **procedural mode is enabled**.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *GenerateMeshProcedural* **callback_generate** -  Callback function responsible for creating and filling the source mesh. Executed in the main thread. The function must have the following signature: ```csharp void GenerateMeshProcedural(Mesh mesh) ```
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_usc.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_usc.md)*.

### Return value

true if the generation was completed and applied successfully, otherwise false
## int runGenerateMeshProceduralForce ( GenerateMeshProcedural callback_generate , DoneMeshProcedural callback_done , int mesh_render_flags = 0 )

**[ Main Thread ]**
Starts immediate (forced) generation of procedural mesh data. The *callback_generate* function is executed in the main thread and must create and fill a Mesh object with vertex data. Once the mesh is applied to the object, the optional *callback_done* is called on the main thread. Works only when **procedural mode is enabled**.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *GenerateMeshProcedural* **callback_generate** -  Callback function responsible for creating and filling the source mesh. Executed in the main thread. The function must have the following signature: ```csharp void GenerateMeshProcedural(Mesh mesh) ```
- *DoneMeshProcedural* **callback_done** -  Optional callback executed after geometry has been fully applied. The function must have the following signature: ```csharp void DoneMeshProcedural() ```
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_usc.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_usc.md)*.

### Return value

true if the generation was completed and applied successfully, otherwise false
