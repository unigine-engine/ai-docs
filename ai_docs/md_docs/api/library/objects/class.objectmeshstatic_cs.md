# ObjectMeshStatic Class (CS)

**Inherits from:** Object


This class is used for handling [static meshes](../../../objects/objects/mesh/index.md).


A static mesh represents a non-deformable collection of vertices, edges, and triangles defining the object's geometry. By default, its geometry is fixed at runtime and can only be transformed as a whole (moved, rotated, scaled). However, ***ObjectMeshStatic*** supports optional procedural modes, which allows [modifying or generating](#procedural_workflow) mesh data in runtime via code.


**[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)** also enables procedural geometry modifications, but **ObjectMeshStatic** provides greater flexibility in controlling generation speed and memory usage. See the [Procedural Mesh Workflow](#procedural_workflow) section for more details.


### Procedural Mesh Workflow


Static meshes support [streaming](../../../principles/data_streaming/index.md), allowing geometry to be loaded from disk on demand to reduce memory usage. However, when procedural mode is enabled, streaming behavior changes depending on the [selected mode](#PROCEDURAL_MODE), some modes keep all data RAM or VRAM, while others allow disk-based access. These differences directly affect performance and memory consumption during runtime.


When creating procedural geometry, the typical workflow is:


1. **Create or Load a Mesh** Before working with procedural geometry, first [create an object](#ObjectMeshStatic_class) that will receive the generated mesh. Then, begin by creating a mesh using the *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* API or loading an existing one from disk. You can fully define geometry in code (vertices, indices, surfaces, etc.), or reuse prepared assets as input data.
2. **Enable Procedural Mode** Call *[setMeshProceduralMode](#setMeshProceduralMode_int_int_void)* to enable runtime modification. Geometry cannot be modified unless one of the procedural modes is selected. > **Notice:** Each procedural mode has specific behavior regarding how geometry is stored and accesed (in RAM, VRAM, or file). See the *[PROCEDURAL_MODE](#PROCEDURAL_MODE)* descriptions for details on how each mode handles memory, streaming, and performance.
3. **Generate and Apply Geometry** There are two main approaches to updating procedural mesh data: > **Notice:** If the mesh is intended to participate in collision and intersection checks, you **must explicitly call** **[CreateCollisionData()](../../../api/library/rendering/class.mesh_cs.md#createCollisionData_int_int_void)** (or only **[CreateSpatialTree()](../../../api/library/rendering/class.mesh_cs.md#createSpatialTree_int_void)** for intersections, or **[CreateEdges()](../../../api/library/rendering/class.mesh_cs.md#createEdges_int_void)** for collisions) after modifying the mesh data and before calling any *apply* methods. This ensures that the required internal data structures (such as edges and spatial tree) are generated and up to date. > > > Keep in mind that generating these structures can be time and memory intensive. If the generated mesh is used purely for visual purposes, creating them is not required and can significantly speed up the generation process.

  - **Use Simplified Generation API** For common procedural workflows, the *[runGenerateMeshProceduralAsync()](#runGenerateMeshProceduralAsync_GenerateMeshProcedural_int_int)* and *[runGenerateMeshProceduralForce()](#runGenerateMeshProceduralForce_GenerateMeshProcedural_int_int)* methods allow you to schedule mesh generation via callbacks. In your callback, you define how the geometry is built (populate *[Mesh](../../../api/library/rendering/class.mesh_cs.md)*), and the engine will apply it automatically. > **Notice:** In case of frequent asynchronous generation, it is recommended to use *[IsMeshProceduralDone](../../...md#isMeshProceduralDone_int)* and *[IsMeshProceduralActive](../../...md#isMeshProceduralActive_int)* to check the current mesh state and coordinate updates, preventing race conditions and ensuring deterministic results.
  - **Manual Geometry Update Control** You can also apply mesh data directly using a set of methods that differ by update strategy. All of them serve the same purpose: replace the current mesh with new data. The procedural generation API provides greater flexibility and control over how new geometry is applied, with differences encoded in the method names: > **Notice:** If a method name contains one of these terms, it reflects how the mesh data is transferred and when the operation is performed. Choose the method that matches your needs, e.g. use *[applyCopyMeshProceduralForce()](#applyCopyMeshProceduralForce_ConstMesh_int_int)* for an **immediate copy**, or *[applyMoveMeshProceduralAsync()](#applyMoveMeshProceduralAsync_Mesh_int_int)* to **transfer** data **without blocking** the main thread.

    - **copy**: Mesh data is copied into the object's internal memory. The **given mesh remains unchanged**. This can be useful when reusing the same geometry across multiple objects.
    - **move**: Mesh data is transferred into the object, without memory copying. The operation swaps mesh data between the object and the given mesh, so the **given mesh no longer contains its original vertex data** and its contents are replaced. This avoids the cost of copying operations and allows for faster updates.
    - **force**: The operation is executed immediately in the main thread. Useful for real-time updates when delay is unacceptable. In *[PROCEDURAL_MODE_DYNAMIC](#PROCEDURAL_MODE_DYNAMIC)*, forced move behaves identically to its asynchronous variant.
    - **async**: This avoids blocking the main thread and is especially useful in *[PROCEDURAL_MODE_FILE](#PROCEDURAL_MODE_FILE)* or *[PROCEDURAL_MODE_BLOB](#PROCEDURAL_MODE_BLOB)* modes, where disk I/O or memory streaming can be offloaded.


### See Also


The **full article** with examples and implementation details for an in-depth exploration of the concepts described above:


- ***[Procedural Meshes](../../../code/usage/procedural_meshes/index_cs.md)* article**


Detailed examples of procedural mesh generation and modification, along with comprehensive comments:


- C# Component samples:

  -
  -
  -
- C++ samples:

  -
  -
  -
- UnigineScript samples:

  -
  -


## ObjectMeshStatic Class

### Enums

## LIGHTMAP_QUALITY

Lightmap baking quality preset to be used.
| Name | Description |
|---|---|
| **GLOBAL** = 0 | Global quality preset set in the [Bake Lighting](../../../editor2/lighting/gi/bake_lighting/index.md#lightmaps) settings. |
| **DRAFT** = 1 | Draft quality preset for lightmaps. |
| **LOW** = 2 | Low quality preset for lightmaps. |
| **MEDIUM** = 3 | Medium quality preset for lightmaps. |
| **HIGH** = 4 | High quality preset for lightmaps. |
| **ULTRA** = 5 | Ultra quality preset for lightmaps. |

## LIGHTMAP_MODE

Lightmap mode defining the source of lightmap texture to be used.
| Name | Description |
|---|---|
| **UNIQUE** = 0 | Bake a unique lightmap texture for the surface. |
| **CUSTOM** = 1 | Use a custom lightmap texture for the surface. |
| **SURFACE** = 2 | Reuse an already baked lightmap texture from another surface. Can be used for LODs. |

## SURFACE_CUSTOM_TEXTURE_MODE

Mode defining the source of surface custom texture to be used.
| Name | Description |
|---|---|
| **UNIQUE** = 0 | Use a unique custom texture for the surface. |
| **SURFACE** = 1 | Use the custom texture from another surface. This option is intended for use with LODs having the same UV maps. |

## PROCEDURAL_MODE

| Name | Description |
|---|---|
| **DISABLE** = 0 | Disables procedural mode. No procedural data is stored or managed. |
| **DYNAMIC** = 1 | This mode is optimized for high-speed dynamic modifications. Provides the fastest performance, but with the highest RAM and VRAM usage. Meshes are not automatically unloaded, manual memory cleanup is required using **[DeleteDynamicMesh()](../../...md#deleteDynamicMesh_int)**. If a mesh is being streamed while modified, this may lead to a crash. > **Notice:** This mode is intended **only for a small number of lightweight objects** that are updated very frequently. |
| **FILE** = 2 | In this mode, procedural mesh data is stored as temporary files on disk. Each time a procedural mesh is modified, the corresponding file is updated. This allows the engine to unload both RAM and VRAM when needed, at the cost of slightly lower performance due to disk I/O operations. Configuration is available through **[`*.boot`](../../../code/configuration_file_cs.md)** or *[Console](../../../code/console/index.md)*, but only takes effect at engine startup: - *mesh_procedural_path*: defines the path where temporary procedural files are stored. - *mesh_procedural_read_only*: disables writing to disk. > **Notice:** Disabling procedural mode for a mesh will delete its corresponding file. > > > When multiple engine instances share the same *mesh_procedural_path*, one instance may delete files that are still in use by another. |
| **BLOB** = 3 | In this mode, all procedural data is stored in memory as a temporary *[Blob](../../../api/library/common/class.blob_cs.md)*. VRAM and RAM are loaded directly from this Blob, which the engine can unload when needed by itself. Modifications are faster compared to *FILE* mode, but at the cost of increased RAM usage. Rendered (visible) meshes are stored uncompressed for optimal performance, while non-visible meshes are compressed to save memory. |

### Properties

## string MeshPath

The path to the source *.mesh*-file used for the object.
> **Notice:** Setting a new path does not update the mesh immediately. If the mesh is in the procedural mode, it will be reset.

## 🔒︎ bool IsMeshLoadedVRAM

The value indicating if the source mesh used for the object is loaded to video memory (VRAM).
## 🔒︎ bool IsMeshLoadedRAM

The value indicating if the source mesh used for the object is loaded to memory (RAM).
## 🔒︎ bool IsMeshNull

The value indicating if the source mesh used for the object is null (does not exist, unassigned, not loaded, etc.).
## 🔒︎ ObjectMeshStatic.PROCEDURAL_MODE MeshProceduralMode

The value indicating which procedural mesh generation mode assigned to the mesh. The value corresponds to one of the available *[PROCEDURAL_MODE](#PROCEDURAL_MODE)* types, determining how procedural data is stored, updated, and unloaded.
## 🔒︎ bool IsMeshProceduralDynamic

The value indicating if the current procedural mode is *[PROCEDURAL_MODE_DYNAMIC](#PROCEDURAL_MODE_DYNAMIC)*.
## 🔒︎ bool IsMeshProceduralActive

The value indicating if an asynchronous operation on the procedural mesh is currently in progress.
## 🔒︎ bool IsMeshProceduralDone

The value indicating if all asynchronous operations on the procedural mesh have completed.
### Members

---

## ObjectMeshStatic ( string path )

ObjectMeshStatic constructor. Creates a Static Mesh object with mesh loaded from the specified file.
### Arguments

- *string* **path** - Path to the source *.mesh*-file.

## ObjectMeshStatic ( )

ObjectMeshStatic constructor. Creates an empty Static Mesh object.
## static int type ( )

Returns the type of the object.
### Return value

*Object Mesh Static* type identifier.
## void SetLightmapEnabled ( bool enabled , int surface )

Sets a value indicating if [lightmapping](../../../editor2/lighting/gi/lightmaps.md) is to be enabled for the surface with the specified number.
### Arguments

- *bool* **enabled** - true to enable [lightmapping](../../../editor2/lighting/gi/lightmaps.md) for the surface with the specified number, or false - to disable.
- *int* **surface** - Mesh surface number.

## bool IsLightmapEnabled ( int surface )

Returns a value indicating if [lightmapping](../../../editor2/lighting/gi/lightmaps.md) is enabled for the surface with the specified number.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

true if [lightmapping](../../../editor2/lighting/gi/lightmaps.md) is enabled for the surface with the specified number;otherwise, false.
## void SetLightmapMode ( ObjectMeshStatic.LIGHTMAP_MODE mode , int surface )

Sets a new lightmap mode for the surface with the specified number.
### Arguments

- *[ObjectMeshStatic.LIGHTMAP_MODE](../../../api/library/objects/class.objectmeshstatic_cs.md#LIGHTMAP_MODE)* **mode** - New lightmap mode to be set for the surface with the specified number. One of the *[LIGHTMAP_MODE](#LIGHTMAP_MODE)* values.
- *int* **surface** - Mesh surface number.

## ObjectMeshStatic.LIGHTMAP_MODE GetLightmapMode ( int surface )

Returns the current lightmap mode for the surface with the specified number.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Current lightmap mode for the surface with the specified number. One of the *[LIGHTMAP_MODE](#LIGHTMAP_MODE)* values.
## void SetLightmapSourceSurface ( int source_surface , int surface )

Sets a new source mesh surface number for the surface with the specified number. A lightmap texture generated for the source mesh surface shall be used for the specified surface (available only when the [lightmap mode](#setLightmapMode_int_int_void) for the surface is set to [LIGHTMAP_MODE_SURFACE](#LIGHTMAP_MODE_SURFACE) mode. This can be used as optimization for LODs.
### Arguments

- *int* **source_surface** - Source mesh surface number.
- *int* **surface** - Mesh surface number.

## int GetLightmapSourceSurface ( int surface )

Returns the current source mesh surface number for the surface with the specified number. A lightmap texture generated for the source mesh surface is used for the specified surface (available only when the [lightmap mode](#setLightmapMode_int_int_void) for the surface is set to [LIGHTMAP_MODE_SURFACE](#LIGHTMAP_MODE_SURFACE) mode. This can be used as optimization for LODs.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Source mesh surface number.
## bool IsLightmapCompression ( int surface )

Returns a value indicating if the [lightmap](../../../editor2/lighting/gi/lightmaps.md) texture baked for the surface with the specified number is to be compressed. Compressed lightmaps are lightweight, but please note that some compression artifacts may appear.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

true if the [lightmap](../../../editor2/lighting/gi/lightmaps.md) texture baked for the surface with the specified number is to be compressed; otherwise, false.
## void SetLightmapCompression ( bool enabled , int surface )

Sets a value indicating if the [lightmap](../../../editor2/lighting/gi/lightmaps.md) texture baked for the surface with the specified number is to be compressed. Compressed lightmaps are lightweight, but please note that some compression artifacts may appear.
### Arguments

- *bool* **enabled** - true to enable compression for the [lightmap](../../../editor2/lighting/gi/lightmaps.md) texture baked for the surface with the specified number, or false - to disable.
- *int* **surface** - Mesh surface number.

## void SetLightmapQuality ( ObjectMeshStatic.LIGHTMAP_QUALITY quality , int surface )

Sets a new lightmap baking quality preset for the surface with the specified number.
### Arguments

- *[ObjectMeshStatic.LIGHTMAP_QUALITY](../../../api/library/objects/class.objectmeshstatic_cs.md#LIGHTMAP_QUALITY)* **quality** - New lightmap baking quality preset to be used for the surface with the specified number. One of the *[LIGHTMAP_QUALITY](#LIGHTMAP_QUALITY)* values.
- *int* **surface** - Mesh surface number.

## ObjectMeshStatic.LIGHTMAP_QUALITY GetLightmapQuality ( int surface )

Returns the current lightmap baking quality preset for the surface with the specified number.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Current lightmap baking quality preset for the surface with the specified number. One of the *[LIGHTMAP_QUALITY](#LIGHTMAP_QUALITY)* values.
## void SetLightmapTextureFilePath ( string path , int surface )

Sets a new path to the baked [lightmap](../../../editor2/lighting/gi/lightmaps.md) texture file to be used for the surface with the specified number. You can use this method to specify a lightmap texture generated in a third-party software.
### Arguments

- *string* **path** - Path to the baked lightmap texture file to be used for the surface with the specified number.
- *int* **surface** - Mesh surface number.

## string GetLightmapTextureFilePath ( int surface )

Returns the path to the baked [lightmap](../../../editor2/lighting/gi/lightmaps.md) texture file currently used for the surface with the specified number.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Path to the baked lightmap texture file currently used for the surface with the specified number.
## void SetSurfaceCustomTextureEnabled ( bool enabled , int surface )

Sets a value indicating if a [custom texture](../../../editor2/node_parameters/visual_representation/index.md#surface_custom_texture) is to be used for the surface with the specified number.
### Arguments

- *bool* **enabled** - true to enable using the [custom texture](../../../editor2/node_parameters/visual_representation/index.md#surface_custom_texture) for the surface with the specified number, or false - to disable.
- *int* **surface** - Mesh surface number.

## bool IsSurfaceCustomTextureEnabled ( int surface )

Returns a value indicating if a [custom texture](../../../editor2/node_parameters/visual_representation/index.md#surface_custom_texture) is to be used for the surface with the specified number.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

true if a [custom texture](../../../editor2/node_parameters/visual_representation/index.md#surface_custom_texture) is to be used for the surface with the specified number; otherwise, false.
## void SetSurfaceCustomTextureMode ( ObjectMeshStatic.SURFACE_CUSTOM_TEXTURE_MODE mode , int surface )

Sets a new mode for the [custom texture](../../../editor2/node_parameters/visual_representation/index.md#surface_custom_texture) of the surface with the specified number. This mode defines the source of the custom texture for the surface: either use a unique custom texture, or use a custom texture that is assigned to another surface of the mesh.
### Arguments

- *[ObjectMeshStatic.SURFACE_CUSTOM_TEXTURE_MODE](../../../api/library/objects/class.objectmeshstatic_cs.md#SURFACE_CUSTOM_TEXTURE_MODE)* **mode** - Custom texture mode to be set for the surface with the specified number. One of the *[SURFACE_CUSTOM_TEXTURE_MODE_](#SURFACE_CUSTOM_TEXTURE_MODE)* values.
- *int* **surface** - Mesh surface number.

## ObjectMeshStatic.SURFACE_CUSTOM_TEXTURE_MODE GetSurfaceCustomTextureMode ( int surface )

Returns the current mode for the [custom texture](../../../editor2/node_parameters/visual_representation/index.md#surface_custom_texture) of the surface with the specified number. This mode defines the source of the custom texture for the surface: either use a unique custom texture, or use a custom texture that is assigned to another surface of the mesh.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Current custom texture mode for the surface with the specified number. One of the *[SURFACE_CUSTOM_TEXTURE_MODE_](#SURFACE_CUSTOM_TEXTURE_MODE)* values.
## void SetSurfaceCustomTextureSourceSurface ( int source_surface , int surface )

Sets a new source mesh surface number for the surface with the specified number. A [custom texture](../../../editor2/node_parameters/visual_representation/index.md#surface_custom_texture) generated for the source mesh surface shall be used for the specified surface (available only when the [custom texture mode](#setSurfaceCustomTextureMode_int_int_void) for the surface is set to [SURFACE_CUSTOM_TEXTURE_MODE_SURFACE](#SURFACE_CUSTOM_TEXTURE_MODE_SURFACE). This can be used as optimization for LODs.
### Arguments

- *int* **source_surface** - Source mesh surface number.
- *int* **surface** - Mesh surface number.

## int GetSurfaceCustomTextureSourceSurface ( int surface )

Returns the current source mesh surface number for the surface with the specified number. A [custom texture](../../../editor2/node_parameters/visual_representation/index.md#surface_custom_texture) generated for the source mesh surface is used for the specified surface (available only when the [custom texture mode](#setSurfaceCustomTextureMode_int_int_void) for the surface is set to [SURFACE_CUSTOM_TEXTURE_MODE_SURFACE](#SURFACE_CUSTOM_TEXTURE_MODE_SURFACE). This can be used as optimization for LODs.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Source mesh surface number.
## void SetSurfaceCustomTexturePath ( string path , int surface )

Sets a new path to the [custom texture](../../../editor2/node_parameters/visual_representation/index.md#surface_custom_texture) to be used for the surface with the specified number. You can use this method to specify a texture generated in a third-party software.
### Arguments

- *string* **path** - Path to the custom texture to be assigned to the surface with the specified number.
- *int* **surface** - Mesh surface number.

## string GetSurfaceCustomTexturePath ( int surface )

Returns the path to the [custom texture](../../../editor2/node_parameters/visual_representation/index.md#surface_custom_texture) currently assigned to the surface with the specified index.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Path to the custom texture currently assigned to the surface with the specified number.
## void SetSurfaceCustomTexture ( Texture texture , int surface )

Sets a new texture to be used as a [custom texture](../../../editor2/node_parameters/visual_representation/index.md#surface_custom_texture) for the surface with the specified number. You can use this method to set any texture.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Texture to be set.
- *int* **surface** - Mesh surface number.

## Texture GetSurfaceCustomTexture ( int surface )

Returns the texture currently used as a [custom texture](../../../editor2/node_parameters/visual_representation/index.md#surface_custom_texture) for the surface with the specified number.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Texture used as a custom texture for the specified surface.
## Mesh GetMeshCurrentRAM ( )

 Returns the current source mesh used for the object and loaded to memory (RAM).
> **Notice:** **Do not modify the meshes returned by this method**, as they are intended to be immutable. Changing them directly may cause **unexpected behavior**.


### Return value

A current source mesh used for the object.
## MeshRender GetMeshCurrentVRAM ( )

Returns the current source mesh used for the object and loaded to video memory (VRAM).
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

Returns the procedural source mesh associated with the object and ensures it is loaded into system memory (RAM). This method is only available when the mesh is in the **dynamic** (**[PROCEDURAL_MODE.DYNAMIC](../../...md#PROCEDURAL_MODE_DYNAMIC)**) mode. A *procedural mesh* is a mesh created via code and uses a specific streaming mode. In **dynamic** mode, the object constantly remains in memory after creation and is only unloaded manually using **[DeleteDynamicMesh()](../../...md#deleteDynamicMesh_int)** or when the procedural mode is changed.
> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Return value

A procedural source mesh used for the object.
## MeshRender GetMeshDynamicVRAM ( )

Returns the procedural render mesh associated with the object and ensures it is loaded into video memory (VRAM). This method is only available when the mesh is in the **dynamic** (**[PROCEDURAL_MODE.DYNAMIC](../../...md#PROCEDURAL_MODE_DYNAMIC)**) mode. A *procedural mesh* is a mesh created via code and uses a specific streaming mode. In **dynamic** mode, the object constantly remains in memory after creation and is only unloaded manually using **[DeleteDynamicMesh()](../../...md#deleteDynamicMesh_int)** or when the procedural mode is changed.
> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Return value

A procedural render mesh used for the object.
## bool LoadAsyncVRAM ( )

**[ Main Thread ]**Asynchronously loads the mesh to video memory (VRAM) if the [async streaming mode for meshes](../../../api/library/rendering/class.render_cs.md#STREAMING_MODE) is enabled. Otherwise, the [forced](#loadForceVRAM_bool) loading is performed. This method is recommended for implementing your own prefetch system (i.e. asynchronous pre-loading of meshes to video memory before they are used).
> **Notice:** Loading to VRAM must be performed in the main thread only.


### Return value

true if the mesh is loaded successfully, otherwise false. If the mesh is already loaded to VRAM, true will be returned.
## bool LoadAsyncRAM ( )

Asynchronously loads the mesh to memory (RAM) if the [async streaming mode for meshes](../../../api/library/rendering/class.render_cs.md#STREAMING_MODE) is enabled. Otherwise, the [forced](#loadForceRAM_bool) loading is performed. This method is recommended for implementing your own prefetch system (i.e. asynchronous pre-loading of meshes to memory before they are used).
### Return value

true if the mesh is loaded successfully, otherwise false. If the mesh is already loaded to RAM, true will be returned.
## bool LoadForceVRAM ( )

Performs force-loading of the mesh to video memory (VRAM) immediately.
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

- *[ObjectMeshStatic.PROCEDURAL_MODE](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE)* **mode** - One of the *[PROCEDURAL_MODE](#PROCEDURAL_MODE)* to apply to the mesh.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cs.md#USAGE_DYNAMIC_VERTEX) that control how vertex and index data are stored for the mesh render.

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


In *[PROCEDURAL_MODE_DYNAMIC](#PROCEDURAL_MODE_DYNAMIC)*, this method behaves identically to its asynchronous variant.


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


In *[PROCEDURAL_MODE_FILE](#PROCEDURAL_MODE_FILE)* and *[PROCEDURAL_MODE_BLOB](#PROCEDURAL_MODE_BLOB)*, this method performs faster compared to the forced variant, as file writes and memory operations are offloaded to background threads.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *Mesh* **mesh** - Source mesh to copy vertex data from.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cs.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)*.

### Return value

true if the mesh was copied successfully, otherwise false.
## bool ApplyMoveMeshProceduralAsync ( Mesh mesh , int mesh_render_flags = 0 )

**[ Main Thread ]**
Moves all vertex data from the given mesh into the object's procedural mesh asynchronously. The operation is not forced and is executed in the background with no noticeable delay, without memory allocation and data copying (move semantics). Works only when **procedural mode is enabled**.


In *[PROCEDURAL_MODE_FILE](#PROCEDURAL_MODE_FILE)* and *[PROCEDURAL_MODE_BLOB](#PROCEDURAL_MODE_BLOB)*, this method performs faster compared to the forced variant, as file writes and memory operations are offloaded to background threads.


This operation **swaps the object's mesh data with the given mesh**. When reusing the same mesh object for further data generation, ensure that its internal state (e.g. number of surfaces) is valid.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Source mesh to copy vertex data from.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cs.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)*.

## bool ApplyMoveMeshProceduralAsync ( Mesh mesh_ram , MeshRender mesh_vram )

**[ Main Thread ]**
Moves all vertex and render data from the given mesh_ram and mesh_vram into the object's procedural mesh asynchronously, without copying or allocating VRAM. The operation is not forced and is executed in the background with no noticeable delay. Works only when **procedural mode is enabled**.


In *[PROCEDURAL_MODE_FILE](#PROCEDURAL_MODE_FILE)* and *[PROCEDURAL_MODE_BLOB](#PROCEDURAL_MODE_BLOB)*, this method performs faster, as file writes and memory operations are offloaded to background threads.


In *[PROCEDURAL_MODE_DYNAMIC](#PROCEDURAL_MODE_DYNAMIC)*, this method behaves identically to its forced variant.


This operation **swaps the object's mesh data with the given mesh**. When reusing the same mesh object for further data generation, ensure that its internal state (e.g. number of surfaces) is valid.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh_ram** - Source mesh containing vertex data.
- *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)* **mesh_vram** - Source mesh containing render data.

### Return value

true if the data was moved successfully, otherwise false.
## bool DeleteDynamicMesh ( )

**[ Main Thread ]**
Releases all memory used by the procedural mesh, including both VRAM and RAM. Works only when procedural mode is set to *[PROCEDURAL_MODE_DYNAMIC](#PROCEDURAL_MODE_DYNAMIC)*.


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
