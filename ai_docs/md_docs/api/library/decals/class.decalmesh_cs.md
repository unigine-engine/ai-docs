# Unigine.DecalMesh Class (CS)

**Inherits from:** Decal


This class describes how to create and modify [mesh decals](../../../objects/decals/mesh/index.md).


### Creating a Mesh Decal


The following code illustrates how to create a mesh decal, set its parameters and add the node to UnigineEditor.


```csharp
using Unigine;

namespace UnigineApp
{
	class AppWorldLogic : WorldLogic
	{
        private DecalMesh decal_mesh;

        public override bool Init()
        {
            // create a mesh with a surface (e.g. a box primitive)
            Mesh mesh = new Mesh();
            mesh.addBoxSurface("box_0", new vec3(1.0f));

            // create a mesh decal using created mesh and setting its radius to 10, material to "decal_base_0"
            decal_mesh = new DecalMesh();
            decal_mesh.SetMesh(mesh);
            decal_mesh.Radius = 10.0f;
            decal_mesh.MaterialPath = "decal_base_0.mat";

            // set the name and position of the decal
            decal_mesh.setName("Mesh Decal");
            decal_mesh.setWorldPosition(new Vec3(0.0f, 0.0f, 5.0f));
            return true;
        }

		public override bool Shutdown()
		{
			// clear pointer
			decal_mesh.clearPtr();

			return true;
		}
	}
}

```


## DecalMesh Class

### Properties

## string MeshPath

The path to the source *.mesh*-file used for the decal.
## 🔒︎ bool IsMeshLoadedVRAM

The value indicating if the source mesh used for the object is loaded to video memory (VRAM).
## 🔒︎ bool IsMeshLoadedRAM

The value indicating if the source mesh used for the object is loaded to memory (RAM).
## 🔒︎ bool IsMeshNull

The value indicating if the source mesh used for the object is null (does not exist, unassigned, not loaded, etc.).
## 🔒︎ ObjectMeshStatic.PROCEDURAL_MODE MeshProceduralMode

The value indicating which procedural mesh generation mode assigned to the mesh. The value corresponds to one of the available *[PROCEDURAL_MODE](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE)* types, determining how procedural data is stored, updated, and unloaded.
## 🔒︎ bool IsMeshProceduralDynamic

The value indicating if the current procedural mode is *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_DYNAMIC)*.
## 🔒︎ bool IsMeshProceduralActive

The value indicating if an asynchronous operation on the procedural mesh is currently in progress.
## 🔒︎ bool IsMeshProceduralDone

The value indicating if all asynchronous operations on the procedural mesh have completed.
### Members

---

## DecalMesh ( )

Constructor. Creates a new *Mesh Decal*.
## DecalMesh ( string path )

DecalMesh constructor. Creates a *Mesh Decal* with a source mesh loaded from the specified file.
### Arguments

- *string* **path** - Path to the source mesh file.

## static int type ( )

Returns a DecalMesh type identifier.
### Return value

Type identifier.
## Mesh GetMeshCurrentRAM ( )

 Returns the current source mesh used for the object and loaded to memory (RAM).
> **Notice:** **Do not modify the meshes returned by this method**, as they are intended to be immutable. Changing them directly may cause **unexpected behavior**.


### Return value

A current source mesh used for the object.
## MeshRender GetMeshCurrentVRAM ( )

Returns the current render mesh used for the object and loaded to video memory (VRAM).
### Return value

A current render mesh used for the object.
## Mesh GetMeshForceRAM ( )

 Returns the source mesh used for the object and loads it to memory (RAM) immediately.
> **Notice:** **Do not modify the meshes returned by this method**, as they are intended to be immutable. Changing them directly may cause **unexpected behavior**.


### Return value

A source mesh used for the object.
## MeshRender GetMeshForceVRAM ( )

Returns the render mesh used for the object and loads it to video memory (VRAM) immediately. At that, the static mesh will also be loaded to memory (RAM).
> **Notice:** Loading to VRAM must be performed in the main thread only.


### Return value

A render mesh used for the object.
## Mesh GetMeshAsyncRAM ( )

 Returns the source mesh used for the object and loads it to memory (RAM) asynchronously.
> **Notice:** **Do not modify the meshes returned by this method**, as they are intended to be immutable. Changing them directly may cause **unexpected behavior**.


### Return value

A source mesh used for the object.
## MeshRender GetMeshAsyncVRAM ( )

**[ Main Thread ]**Returns the render mesh used for the object and loads it to video memory (VRAM) asynchronously. At that, the static mesh will also be loaded to memory (RAM).
> **Notice:** Loading to VRAM must be performed in the main thread only.


### Return value

A render mesh used for the object.
## Mesh GetMeshDynamicRAM ( )

Returns the procedural source mesh associated with the object and ensures it is loaded into system memory (RAM). This method is only available when the mesh is in the **dynamic** (*[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_DYNAMIC)*) mode. A *procedural mesh* is a mesh created via code and uses a specific streaming mode. In *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_DYNAMIC)*, the object stays in memory after creation and is only unloaded manually using *[deleteDynamicMesh()](../../../api/library/objects/class.objectmeshstatic_cs.md#deleteDynamicMesh_int)* or when the procedural mode is changed.
> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Return value

A procedural source mesh used for the object.
## MeshRender GetMeshDynamicVRAM ( )

Returns the procedural render mesh associated with the object and ensures it is loaded into video memory (VRAM). This method is only available when the mesh is in the **dynamic** (*[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_DYNAMIC)*) mode. A *procedural mesh* is a mesh created via code and uses a specific streaming mode. In *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_DYNAMIC)*, the object stays in memory after creation and is only unloaded manually using *[deleteDynamicMesh()](../../../api/library/objects/class.objectmeshstatic_cs.md#deleteDynamicMesh_int)* or when the procedural mode is changed.
> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Return value

A procedural render mesh used for the object.
## bool LoadAsyncVRAM ( )

**[ Main Thread ]**Asynchronously loads the mesh to video memory (VRAM) if the [async streaming mode for meshes](../../../api/library/rendering/class.render_cs.md#STREAMING_MODE) is enabled. Otherwise, the [forced](#loadForceVRAM_bool) loading is performed. This method is recommended for implementing your own prefetch system (i.e. asynchronous pre-loading of meshes to video memory before they are used).
> **Notice:** Loading to VRAM must be performed in the main thread only.


### Return value

true if the mesh is loaded successfully, otherwise false. If the mesh is already loaded to VRAM, true will be returned.
## bool LoadAsyncRAM ( )

Asynchronously loads the mesh to memory (RAM) if the [async streaming mode for meshes](../../../api/library/rendering/class.render_cs.md#STREAMING_MODE) is enabled. Otherwise, the [forced](#loadForceRAM_bool) loading is performed. This method is recommended for implementing your own prefetch system (i.e. asynchronous pre-loading of meshes to video memory before they are used).
### Return value

true if the mesh is loaded successfully, otherwise false. If the mesh is already loaded to RAM, true will be returned.
## bool LoadForceVRAM ( )

Performs force-loading of the mesh to video memory (VRAM) immediately. The forced loading to VRAM is performed in the main thread.
> **Notice:** Loading to VRAM must be performed in the main thread only.


### Return value

true if the mesh is loaded successfully, otherwise false. If the mesh is already loaded to VRAM, true will be returned.
## bool LoadForceRAM ( )

Performs force-loading of the mesh to memory (RAM) immediately.
### Return value

true if the mesh is loaded successfully, otherwise false. If the mesh is already loaded to RAM, true will be returned.
## void SetMeshProceduralMode ( ObjectMeshStatic.PROCEDURAL_MODE mode , int mesh_render_flags = 0 )

Sets the procedural mode for the mesh. The specified mode defines how procedural data is stored, updated, and unloaded.
> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *[ObjectMeshStatic.PROCEDURAL_MODE](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE)* **mode** - One of the *[PROCEDURAL_MODE](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE)* to apply to the mesh.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cs.md#USAGE_DYNAMIC_VERTEX) that control how vertex and index data are stored for the mesh render.

## int GetStatDrawCalls ( )

Returns the number of draw calls (DIP) for the decal during the last frame.
### Return value

Number of draw calls (DIP) for the decal during the last frame.
## int GetStatDrawCountViewport ( )

Returns the number of times the decal was drawn in the viewport last frame.
### Return value

Number of times the decal was drawn in the viewport last frame.
## int GetStatDrawCountReflection ( )

Returns the number of times the decal was drawn during reflections rendering in the last frame.
### Return value

Number of times the decal was drawn during rendering in the last frame.
## int GetStatDrawCountShadow ( )

Returns the number of times the decal was drawn during shadows rendering in the last frame.
### Return value

Number of times the decal was drawn during shadows rendering in the last frame.
## long GetStatFrame ( )

Returns the number of [Engine frame](../../../api/library/engine/class.engine_cs.md#getFrame_int64_t), in which the decal was drawn last time.
### Return value

Number of frame, in which the decal was drawn last time.
## Mesh CreateCopyMeshRAM ( )

Creates and returns a copy of the source mesh used by the object, loading it directly from disk if it is not present in cache. This method does not stream the copied mesh into memory cache, resulting in lower RAM usage.
### Return value

A copy of the source mesh, or nullptr if source mesh is not presented in RAM or its file path is invalid.
## bool GetCopyMeshRAM ( Mesh result )

Retrieves a copy of the source mesh used by the object and writes it to the provided mesh object. If the mesh is not present in cache, it is loaded directly from disk. This method does not stream the copied mesh into memory cache, resulting in lower RAM usage.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **result** - Object that will receive a copy of the source mesh.

### Return value

true if the mesh was copied successfully, false if source mesh is not present in RAM or its file path is invalid.
## bool ApplyCopyMeshProceduralForce ( Mesh mesh , int mesh_render_flags = 0 )

**[ Main Thread ]**
Copies all vertex data from the given mesh into the object's procedural mesh forcibly, executing the operation immediately. Works only when **procedural mode is enabled**.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *Mesh* **mesh** - Source mesh to copy vertex data from.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cs.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)*.

### Return value

true if the mesh was copied successfully, otherwise false.
## bool ApplyMoveMeshProceduralForce ( Mesh mesh , int mesh_render_flags = 0 )

**[ Main Thread ]**
Moves all vertex data from the given mesh into the object's procedural mesh forcibly, executing the operation immediately without memory allocation and data copying (move semantics). Works only when **procedural mode is enabled**.


In *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_DYNAMIC)*, this method behaves identically to its asynchronous variant.


This operation **swaps the object's mesh data with the given mesh**. When reusing the same mesh object for further data generation, ensure that its internal state (e.g. number of surfaces) is valid.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Source mesh to move vertex data from.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cs.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)*.

### Return value

true if the mesh was moved (transferred without copying) successfully, otherwise false.
## bool ApplyMoveMeshProceduralForce ( Mesh mesh_ram , MeshRender mesh_vram )

**[ Main Thread ]**
Moves all vertex and render data from the given *mesh_ram* and *mesh_vram* into the object's procedural mesh forcibly, executing the operation immediately using move semantics, without data copying or VRAM allocation. Works only when **procedural mode is enabled**.


This operation **swaps the object's mesh data with the given mesh**. When reusing the same mesh object for further data generation, ensure that its internal state (e.g. number of surfaces) is valid.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh_ram** - Source mesh containing vertex data.
- *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)* **mesh_vram** - Source mesh containing render data.

### Return value

true if the data was moved (transferred without copying) successfully, otherwise false.
## bool ApplyCopyMeshProceduralAsync ( Mesh mesh , int mesh_render_flags = 0 )

**[ Main Thread ]**
Copies all vertex data from the given mesh into the object's procedural mesh asynchronously. The operation is not forced and is executed in the background with no noticeable delay. Works only when **procedural mode is enabled**.


In *[PROCEDURAL_MODE_FILE](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_FILE)* and *[PROCEDURAL_MODE_BLOB](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_BLOB)*, this method performs faster compared to the forced variant, as file writes and memory operations are offloaded to background threads.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *Mesh* **mesh** - Source mesh to copy vertex data from.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cs.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)*.

### Return value

true if the mesh was copied successfully, otherwise false.
## bool ApplyMoveMeshProceduralAsync ( Mesh mesh , int mesh_render_flags = 0 )

**[ Main Thread ]**
Moves all vertex data from the given mesh into the object's procedural mesh asynchronously. The operation is not forced and is executed in the background with no noticeable delay, without memory allocation and data copying (move semantics). Works only when **procedural mode is enabled**.


In *[PROCEDURAL_MODE_FILE](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_FILE)* and *[PROCEDURAL_MODE_BLOB](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_BLOB)*, this method performs faster compared to the forced variant, as file writes and memory operations are offloaded to background threads.


This operation **swaps the object's mesh data with the given mesh**. When reusing the same mesh object for further data generation, ensure that its internal state (e.g. number of surfaces) is valid.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Source mesh to copy vertex data from.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cs.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)*.

## bool ApplyMoveMeshProceduralAsync ( Mesh mesh_ram , MeshRender mesh_vram )

**[ Main Thread ]**
Moves all vertex and render data from the given mesh_ram and mesh_vram into the object's procedural mesh asynchronously, without copying or allocating VRAM. The operation is not forced and is executed in the background with no noticeable delay. Works only when **procedural mode is enabled**.


In *[PROCEDURAL_MODE_FILE](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_FILE)* and *[PROCEDURAL_MODE_BLOB](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_BLOB)*, this method performs faster, as file writes and memory operations are offloaded to background threads.


In *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_DYNAMIC)*, this method behaves identically to its forced variant.


This operation **swaps the object's mesh data with the given mesh**. When reusing the same mesh object for further data generation, ensure that its internal state (e.g. number of surfaces) is valid.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh_ram** - Source mesh containing vertex data.
- *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)* **mesh_vram** - Source mesh containing render data.

### Return value

true if the data was moved successfully, otherwise false.
## bool DeleteDynamicMesh ( )

**[ Main Thread ]**
Releases all memory used by the procedural mesh, including both VRAM and RAM. Works only when procedural mode is set to *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_DYNAMIC)*.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Return value

true if the memory was released successfully, otherwise false.
## bool RunGenerateMeshProceduralAsync ( GenerateMeshProcedural callback_generate , int mesh_render_flags = 0 )

**[ Main Thread ]**
Starts asynchronous generation of procedural mesh data. The *callback_generate* function is executed in a background thread and must create and fill a mesh object with new data. The generated mesh will be transferred to the object once complete, without blocking the main thread. Works only when **procedural mode is enabled**.


Note that the callback is executed in a single dedicated thread controlled by the engine, it is not parallelized and must not spawn additional threads.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *GenerateMeshProcedural* **callback_generate** -  Callback function responsible for creating and filling the source mesh. Executed in the main thread. The function must have the following signature: ```csharp void GenerateMeshProcedural(Mesh mesh) ```
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cs.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)*.

### Return value

true if the modification was completed and applied successfully, otherwise false
## bool RunGenerateMeshProceduralAsync ( GenerateMeshProcedural callback_generate , DoneMeshProcedural callback_done , int mesh_render_flags = 0 )

**[ Main Thread ]**
Starts asynchronous generation of procedural mesh data. The *callback_generate* function is executed in a background thread and must create and fill a mesh object with new data. The generated mesh will be transferred to the object once complete, without blocking the main thread. After the mesh has been applied to the object, the optional callback_done will be called. Works only when **procedural mode is enabled**.


Note that the callback is executed in a single dedicated thread controlled by the engine, it is not parallelized and must not spawn additional threads.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *GenerateMeshProcedural* **callback_generate** -  Callback function responsible for creating and filling the source mesh. Executed in the main thread. The function must have the following signature: ```csharp void GenerateMeshProcedural(Mesh mesh) ```
- *DoneMeshProcedural* **callback_done** -  Optional callback executed after geometry has been fully applied. The function must have the following signature: ```csharp void DoneMeshProcedural() ```
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cs.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)*.

### Return value

true if the generation was completed and applied successfully, otherwise false
## bool RunGenerateMeshProceduralForce ( GenerateMeshProcedural callback_generate , int mesh_render_flags = 0 )

**[ Main Thread ]**
Starts immediate (forced) generation of procedural mesh data. The *callback_generate* function is executed in the main thread and must create and fill a mesh object with new data. The generated mesh is applied to the object as soon as generation completes. Works only when **procedural mode is enabled**.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *GenerateMeshProcedural* **callback_generate** -  Callback function responsible for creating and filling the source mesh. Executed in the main thread. The function must have the following signature: ```csharp void GenerateMeshProcedural(Mesh mesh) ```
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cs.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)*.

### Return value

true if the generation was completed and applied successfully, otherwise false
## bool RunGenerateMeshProceduralForce ( GenerateMeshProcedural callback_generate , DoneMeshProcedural callback_done , int mesh_render_flags = 0 )

**[ Main Thread ]**
Starts immediate (forced) generation of procedural mesh data. The *callback_generate* function is executed in the main thread and must create and fill a Mesh object with vertex data. Once the mesh is applied to the object, the optional *callback_done* is called on the main thread. Works only when **procedural mode is enabled**.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *GenerateMeshProcedural* **callback_generate** -  Callback function responsible for creating and filling the source mesh. Executed in the main thread. The function must have the following signature: ```csharp void GenerateMeshProcedural(Mesh mesh) ```
- *DoneMeshProcedural* **callback_done** -  Optional callback executed after geometry has been fully applied. The function must have the following signature: ```csharp void DoneMeshProcedural() ```
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cs.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)*.

### Return value

true if the generation was completed and applied successfully, otherwise false
