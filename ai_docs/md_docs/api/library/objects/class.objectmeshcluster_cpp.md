# ObjectMeshCluster Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


A [MeshCluster](../../../objects/objects/mesh_cluster/index.md) class allows you to bake identical meshes (with the same material applied to their surfaces) into one object, which provides less cluttered spatial tree, reduces the number of texture fetches and speeds up rendering.


Meshes are rendered within a specified [visibility distance](#setVisibleDistance_float_void) from the camera. When moving away from this distance, meshes [fade out](#setFadeDistance_float_void) and then disappear completely.


### See Also


- C# Component samples:

  -
  -
- C++ samples:

  -
  -
- UnigineScript samples:

  -
  -


## ObjectMeshCluster Class

### Members

---

## static ObjectMeshClusterPtr create ( const char * path )

ObjectMeshCluster constructor. Creates a mesh cluster with a source mesh loaded from the specified file.
### Arguments

- *const char ** **path** - Path to the source mesh file.

## static ObjectMeshClusterPtr create ( )

ObjectMeshCluster constructor. Creates an empty mesh cluster
## void setFadeDistance ( float distance )

Sets the distance up to which meshes handled by the mesh cluster will be fading out (that is, fewer meshes will be rendered instead of all). The distance is measured starting from the [visible distance](#setVisibleDistance_float_void). The default is 0. Using fade distance allows the objects to disappear one by one until up to the fade distance only a few left. It makes the disappearing smooth and much less noticeable.
### Arguments

- *float* **distance** - Fading distance for meshes in units. If a negative value is provided, 0 will be used instead.

## float getFadeDistance ( ) const

Returns the distance up to which meshes handled by the mesh cluster will be fading out. The default is 0.
### Return value

Fading distance for meshes in units.
## void setMeshPath ( const char * path )

Sets a path to the mesh hadled by the *Mesh Cluster*. Does not update mesh immediately using the new path. If the mesh is in the procedural mode, it will be reset.
### Arguments

- *const char ** **path** - New path to the source *.mesh*-file to be set.

## const char * getMeshPath ( ) const

Returns the path to the source *.mesh*-file of the mesh handled by *Mesh Cluster*.
### Return value

Path to the source *.mesh*-file.
## int addMeshTransform ( )

Adds a new mesh instance transformation to the *Mesh Cluster*. To set the new added transformation pass the return value of this method to the [*setMeshTransform()*](#setMeshTransform_int_mat4_void) method.
### Return value

Number of the last added mesh instance.
## void setMeshTransform ( int num , const Math:: mat4 & transform )

Sets the transformation for the given mesh instance.
### Arguments

- *int* **num** - Mesh instance number.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Mesh transformation matrix.

## Math:: mat4 getMeshTransform ( int num ) const

Returns the transformation of the given mesh instance.
### Arguments

- *int* **num** - Mesh instance number.

### Return value

Mesh transformation matrix.
## void removeMeshTransform ( int num )

Removes the transformation of the specified mesh instance from the cluster.
### Arguments

- *int* **num** - Mesh instance number.

## void removeMeshTransformFast ( int num )

Removes the transformation of the specified mesh instance from the cluster.
### Arguments

- *int* **num** - Mesh instance number.

## int getNumMeshes ( ) const

Returns the total number of meshes handled by the mesh cluster.
### Return value

Number of meshes.
## void setVisibleDistance ( float distance )

Sets the distance up to which meshes handled by the mesh cluster will be rendered. The default is infinity (in this case, [fade distance](#setFadeDistance_float_void) will be ignored).
### Arguments

- *float* **distance** - Visibility distance for meshes in units. If a negative value is provided, 0 will be used instead.

## float getVisibleDistance ( ) const

Returns the distance up to which meshes handled by the mesh cluster are rendered. The default is infinity (in this case, [fade distance](#setFadeDistance_float_void) is ignored).
### Return value

Visibility distance for meshes in units.
## void clearMeshes ( )

Deletes all meshes currently baked into mesh cluster.
## void createMeshes ( const Vector < Math:: Mat4 > & world_transforms )

Creates meshes in accordance with the transformations vector (world coordinates) and bakes them into the cluster. All baked meshes are identical to the source [mesh](#getMeshPath_cstr) and have the same material applied to their surfaces.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)> &* **world_transforms** - Transformations vector in world coordinates.

## void appendMeshes ( const Vector < Math:: Mat4 > & world_transforms )

Appends new meshes with transformations stored in the specified vector (world coordinates) and bakes them into the cluster. All baked meshes are identical to the source [mesh](#getMeshPath_cstr) and have the same material applied to their surfaces.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)> &* **world_transforms** - Transformations vector in world coordinates.

## static int type ( )

Returns the type of the node.
### Return value

[Node](../../../api/library/nodes/class.node_cpp.md) type identifier.
## bool removeClusterTransforms ( const Math:: WorldBoundBox & bb )

Removes cluster meshes, found within the specified bounding box, from the cluster.
### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - Bounding box defining the area, within which the cluster meshes are to be removed from the cluster.

### Return value

true if cluster meshes, found within the specified bounding box are successfully removed; otherwise, false.
## bool removeClusterTransformsFromSphere ( const Math:: WorldBoundSphere & bb )

Removes cluster meshes, found within the specified bounding sphere, from the cluster.
### Arguments

- *const  Math::[WorldBoundSphere](../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bb** - Bounding sphere defining the area, for which the transformations of cluster meshes are to be collected.

### Return value

**true** if cluster meshes, found within the specified bounding sphere are successfully removed; otherwise, **false**.
## bool detachClusterTransforms ( const Math:: WorldBoundBox & bb , Vector < Math:: mat4 > & OUT_transforms )

Detaches cluster meshes found within the area specified by the given bounding box from the cluster and puts their transformations (local coordinates) to the specified buffer.
### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - Bounding box defining the area, within which the cluster meshes are to be detached from the cluster.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[mat4](../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Buffer to store transformations of detached cluster meshes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if cluster meshes have been detached from the cluster; otherwise false.
## bool detachClusterWorldTransforms ( const Math:: WorldBoundBox & bb , Vector < Math:: Mat4 > & OUT_transforms )

Detaches cluster meshes found within the area specified by the given bounding box from the cluster and puts their transformations (world coordinates) to the specified buffer.
### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - Bounding box defining the area, within which the cluster meshes are to be detached from the cluster.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Buffer to store transformations of detached cluster meshes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if cluster meshes have been detached from the cluster; otherwise false.
## bool detachClusterWorldTransformsFromSphere ( const Math:: WorldBoundSphere & bb , Vector < Math:: Mat4 > & OUT_transforms )

Detaches cluster meshes found within the area specified by the given bounding box from the cluster and puts their transformations (world coordinates) to the specified buffer.
### Arguments

- *const  Math::[WorldBoundSphere](../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bb** - Bounding sphere defining the area, for which the transformations of cluster meshes are to be collected.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Buffer to store transformations of cluster meshes, in world coordinates. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if cluster meshes have been detached from the cluster; otherwise false.
## bool getClusterTransforms ( const Math:: WorldBoundBox & bounds , Vector < Math:: mat4 > & OUT_transforms )

Collects transformations (local coordinates) for all cluster meshes within the area specified by the given bounding box and puts them to the specified buffer.
### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bounds** - Bounding box defining the area, for which the transformations of cluster meshes are to be collected.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[mat4](../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Buffer to store transformations of cluster meshes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true, if there are transformations of cluster meshes; or false, if there are no transformations of cluster meshes found.
## bool getClusterWorldTransforms ( const Math:: WorldBoundBox & bounds , Vector < Math:: Mat4 > & OUT_transforms )

Collects transformations (world coordinates) for all cluster meshes within the area specified by the given bounding box and puts them to the specified buffer.
### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bounds** - Bounding box defining the area, for which the transformations of cluster meshes are to be collected.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Buffer to store transformations of cluster meshes, in world coordinates. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true, if there are transformations of cluster meshes; or false, if there are no transformations of cluster meshes within the specified area.
## bool getClusterWorldTransformsFromSphere ( const Math:: WorldBoundSphere & bounds , Vector < Math:: Mat4 > & OUT_transforms )

Collects transformations (world coordinates) for all cluster meshes within the area specified by the given bounding sphere and puts them to the specified buffer.
### Arguments

- *const  Math::[WorldBoundSphere](../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bounds** - Bounding sphere defining the area, for which the transformations of cluster meshes are to be collected.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Buffer to store transformations of cluster meshes, in world coordinates. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true, if there are transformations of cluster meshes; or false, if there are no transformations of cluster meshes within the specified area.
## bool getInstancesFromSphere ( const Math:: WorldBoundSphere & bb , Vector <int> & OUT_instances )

Returns the indices of instances inside the bounding sphere.
> **Notice:** The returned list of instance indices is **unsorted**.


### Arguments

- *const  Math::[WorldBoundSphere](../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bb** - Bounding sphere defining the area within which instances are to be collected.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **OUT_instances** - Vector containing instance indices. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true, if there is at least one instance inside the bounding sphere; or false.
## Ptr<ConstMesh> getMeshCurrentRAM ( ) const

 Returns the current source mesh used for the object and loaded to memory (RAM).
### Return value

A current source mesh used for the object.
## Ptr < MeshRender > getMeshCurrentVRAM ( )

Returns the current render mesh used for the object and loaded to video memory (VRAM).
### Return value

A current render mesh used for the object.
## Ptr<ConstMesh> getMeshForceRAM ( )

Returns the source mesh used for the object and loads it to memory (RAM) immediately.
### Return value

A source mesh used for the object.
## Ptr < MeshRender > getMeshForceVRAM ( )

Returns the render mesh used for the object and loads it to video memory (VRAM) immediately. At that, the static mesh will also be loaded to memory (RAM).
> **Notice:** Loading to VRAM must be performed in the main thread only.


### Return value

A render mesh used for the object.
## Ptr<ConstMesh> getMeshAsyncRAM ( )

Returns the source mesh used for the object and loads it to memory (RAM) asynchronously.
### Return value

A source mesh used for the object.
## Ptr < MeshRender > getMeshAsyncVRAM ( )

**[ Main Thread ]**Returns the render mesh used for the object and loads it to video memory (VRAM) asynchronously. At that, the static mesh will also be loaded to memory (RAM).
> **Notice:** Loading to VRAM must be performed in the main thread only.


### Return value

A render mesh used for the object.
## Ptr < Mesh > getMeshDynamicRAM ( )

Returns the procedural source mesh associated with the object and ensures it is loaded into system memory (RAM). This method is only available when the mesh is in the **dynamic** (*[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_DYNAMIC)*) mode. A *procedural mesh* is a mesh created via code and uses a specific streaming mode. In *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_DYNAMIC)*, the object stays in memory after creation and is only unloaded manually using *[deleteDynamicMesh()](../../../api/library/objects/class.objectmeshstatic_cpp.md#deleteDynamicMesh_int)* or when the procedural mode is changed.
> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Return value

A procedural source mesh used for the object.
## Ptr < MeshRender > getMeshDynamicVRAM ( )

Returns the procedural render mesh associated with the object and ensures it is loaded into video memory (VRAM). This method is only available when the mesh is in the **dynamic** (*[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_DYNAMIC)*) mode. A *procedural mesh* is a mesh created via code and uses a specific streaming mode. In *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_DYNAMIC)*, the object stays in memory after creation and is only unloaded manually using *[deleteDynamicMesh()](../../../api/library/objects/class.objectmeshstatic_cpp.md#deleteDynamicMesh_int)* or when the procedural mode is changed.
> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Return value

A procedural render mesh used for the object.
## bool loadAsyncVRAM ( )

**[ Main Thread ]**Asynchronously loads the mesh to video memory (VRAM) if the [async streaming mode for meshes](../../../api/library/rendering/class.render_cpp.md#STREAMING_MODE) is enabled. Otherwise, the [forced](#loadForceVRAM_bool) loading is performed. This method is recommended for implementing your own prefetch system (i.e. asynchronous pre-loading of meshes to video memory before they are used).
> **Notice:** Loading to VRAM must be performed in the main thread only.


### Return value

true if the mesh is loaded successfully, otherwise false. If the mesh is already loaded to VRAM, true will be returned.
## bool loadAsyncRAM ( )

Asynchronously loads the mesh to memory (RAM) if the [async streaming mode for meshes](../../../api/library/rendering/class.render_cpp.md#STREAMING_MODE) is enabled. Otherwise, the [forced](#loadForceRAM_bool) loading is performed. This method is recommended for implementing your own prefetch system (i.e. asynchronous pre-loading of meshes to memory before they are used).
### Return value

true if the mesh is loaded successfully, otherwise false. If the mesh is already loaded to RAM, true will be returned.
## bool loadForceVRAM ( )

Performs force-loading of the mesh to video memory (VRAM) immediately. The forced loading to VRAM is performed in the main thread.
> **Notice:** Loading to VRAM must be performed in the main thread only.


### Return value

true if the mesh is loaded successfully, otherwise false. If the mesh is already loaded to VRAM, true will be returned.
## bool loadForceRAM ( )

Performs force-loading of the mesh to memory (RAM) immediately.
### Return value

true if the mesh is loaded successfully, otherwise false. If the mesh is already loaded to RAM, true will be returned.
## bool isMeshNull ( ) const

Returns a value indicating if the source mesh used for the object is null (does not exist, unassigned, not loaded, etc.).
### Return value

true if the source mesh used for the object is null; otherwise, false.
## bool isMeshLoadedRAM ( ) const

Returns a value indicating if the source mesh used for the object is loaded to memory (RAM).
### Return value

true if the source mesh used for the object is loaded to RAM; otherwise, false.
## bool isMeshLoadedVRAM ( ) const

Returns a value indicating if the source mesh used for the object is loaded to video memory (VRAM).
### Return value

true if the source mesh used for the object is loaded to VRAM; otherwise, false.
## Ptr < Mesh > createCopyMeshRAM ( ) const

Creates and returns a copy of the source mesh used by the object, loading it directly from disk if it is not present in cache. This method does not stream the copied mesh into memory cache, resulting in lower RAM usage.
### Return value

A copy of the source mesh, or nullptr if source mesh is not presented in RAM or its file path is invalid.
## bool getCopyMeshRAM ( Ptr < Mesh > & result ) const

Retrieves a copy of the source mesh used by the object and writes it to the provided mesh object. If the mesh is not present in cache, it is loaded directly from disk. This method does not stream the copied mesh into memory cache, resulting in lower RAM usage.
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **result** - Object that will receive a copy of the source mesh.

### Return value

true if the mesh was copied successfully, false if source mesh is not present in RAM or its file path is invalid.
## bool isMeshProceduralDone ( ) const

Returns a value indicating if all asynchronous operations on the procedural mesh have completed.
> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Return value

true if no asynchronous geometry operation is active, otherwise false.
## bool isMeshProceduralActive ( ) const

Returns a value indicating if an asynchronous operation on the procedural mesh is currently in progress.
> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Return value

true if an asynchronous geometry operation is active, otherwise false.
## bool isMeshProceduralDynamic ( ) const

Returns a value indicating if the current procedural mode is *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_DYNAMIC)*.
> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Return value

true if *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_DYNAMIC)* is active, otherwise false.
## void setMeshProceduralMode ( ObjectMeshStatic::PROCEDURAL_MODE mode , int mesh_render_flags = 0 )

Sets the procedural mode for the mesh. The specified mode defines how procedural data is stored, updated, and unloaded.
> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *[ObjectMeshStatic::PROCEDURAL_MODE](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE)* **mode** - One of the *[PROCEDURAL_MODE](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE)* to apply to the mesh.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cpp.md#USAGE_DYNAMIC_VERTEX) that control how vertex and index data are stored for the mesh render.

## ObjectMeshStatic::PROCEDURAL_MODE getMeshProceduralMode ( ) const

Returns a value indicating which procedural mode assigned to the mesh. The value corresponds to one of the available *[PROCEDURAL_MODE](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE)* types, determining how procedural data is stored, updated, and unloaded.
> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Return value

Current procedural mode of the mesh.
## bool applyCopyMeshProceduralForce ( const Ptr<ConstMesh> & mesh , int mesh_render_flags = 0 )

**[ Main Thread ]**
Copies all vertex data from the given mesh into the object's procedural mesh forcibly, executing the operation immediately. Works only when **procedural mode is enabled**.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *[const Ptr<ConstMesh> &](#ConstMeshPtr)* **mesh** - Source mesh to copy vertex data from.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cpp.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cpp.md)*.

### Return value

true if the mesh was copied successfully, otherwise false.
## bool applyMoveMeshProceduralForce ( const Ptr < Mesh > & mesh , int mesh_render_flags = 0 )

**[ Main Thread ]**
Moves all vertex data from the given mesh into the object's procedural mesh forcibly, executing the operation immediately without memory allocation and data copying (move semantics). Works only when **procedural mode is enabled**.


In *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_DYNAMIC)*, this method behaves identically to its asynchronous variant.


This operation **swaps the object's mesh data with the given mesh**. When reusing the same mesh object for further data generation, ensure that its internal state (e.g. number of surfaces) is valid.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - Source mesh to move vertex data from.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cpp.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cpp.md)*.

### Return value

true if the mesh was moved (transferred without copying) successfully, otherwise false.
## bool applyMoveMeshProceduralForce ( const Ptr < Mesh > & mesh_ram , const Ptr < MeshRender > & mesh_vram )

**[ Main Thread ]**
Moves all vertex and render data from the given *mesh_ram* and *mesh_vram* into the object's procedural mesh forcibly, executing the operation immediately using move semantics, without data copying or VRAM allocation. Works only when **procedural mode is enabled**.


This operation **swaps the object's mesh data with the given mesh**. When reusing the same mesh object for further data generation, ensure that its internal state (e.g. number of surfaces) is valid.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh_ram** - Source mesh containing vertex data.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[MeshRender](../../../api/library/rendering/class.meshrender_cpp.md)> &* **mesh_vram** - Source mesh containing render data.

### Return value

true if the data was moved (transferred without copying) successfully, otherwise false.
## bool applyCopyMeshProceduralAsync ( const Ptr<ConstMesh> & mesh , int mesh_render_flags = 0 )

**[ Main Thread ]**
Copies all vertex data from the given mesh into the object's procedural mesh asynchronously. The operation is not forced and is executed in the background with no noticeable delay. Works only when **procedural mode is enabled**.


In *[PROCEDURAL_MODE_FILE](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_FILE)* and *[PROCEDURAL_MODE_BLOB](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_BLOB)*, this method performs faster compared to the forced variant, as file writes and memory operations are offloaded to background threads.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *[const Ptr<ConstMesh> &](#ConstMeshPtr)* **mesh** - Source mesh to copy vertex data from.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cpp.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cpp.md)*.

### Return value

true if the mesh was copied successfully, otherwise false.
## bool applyMoveMeshProceduralAsync ( const Ptr < Mesh > & mesh , int mesh_render_flags = 0 )

**[ Main Thread ]**
Moves all vertex data from the given mesh into the object's procedural mesh asynchronously. The operation is not forced and is executed in the background with no noticeable delay, without memory allocation and data copying (move semantics). Works only when **procedural mode is enabled**.


In *[PROCEDURAL_MODE_FILE](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_FILE)* and *[PROCEDURAL_MODE_BLOB](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_BLOB)*, this method performs faster compared to the forced variant, as file writes and memory operations are offloaded to background threads.


This operation **swaps the object's mesh data with the given mesh**. When reusing the same mesh object for further data generation, ensure that its internal state (e.g. number of surfaces) is valid.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - Source mesh to copy vertex data from.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cpp.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cpp.md)*.

## bool applyMoveMeshProceduralAsync ( const Ptr < Mesh > & mesh_ram , const Ptr < MeshRender > & mesh_vram )

**[ Main Thread ]**
Moves all vertex and render data from the given mesh_ram and mesh_vram into the object's procedural mesh asynchronously, without copying or allocating VRAM. The operation is not forced and is executed in the background with no noticeable delay. Works only when **procedural mode is enabled**.


In *[PROCEDURAL_MODE_FILE](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_FILE)* and *[PROCEDURAL_MODE_BLOB](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_BLOB)*, this method performs faster, as file writes and memory operations are offloaded to background threads.


In *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_DYNAMIC)*, this method behaves identically to its forced variant.


This operation **swaps the object's mesh data with the given mesh**. When reusing the same mesh object for further data generation, ensure that its internal state (e.g. number of surfaces) is valid.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh_ram** - Source mesh containing vertex data.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[MeshRender](../../../api/library/rendering/class.meshrender_cpp.md)> &* **mesh_vram** - Source mesh containing render data.

### Return value

true if the data was moved successfully, otherwise false.
## bool deleteDynamicMesh ( )

**[ Main Thread ]**
Releases all memory used by the procedural mesh, including both VRAM and RAM. Works only when procedural mode is set to *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_DYNAMIC)*.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Return value

true if the memory was released successfully, otherwise false.
## bool runGenerateMeshProceduralAsync ( CallbackBase1 < Ptr < Mesh >> * callback_generate , int mesh_render_flags = 0 )

**[ Main Thread ]**
Starts asynchronous generation of procedural mesh data. The *callback_generate* function is executed in a background thread and must create and fill a mesh object with new data. The generated mesh will be transferred to the object once complete, without blocking the main thread. Works only when **procedural mode is enabled**.


Note that the callback is executed in a single dedicated thread controlled by the engine, it is not parallelized and must not spawn additional threads.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *[CallbackBase1](../../../api/library/common/callbacks/class.callbackbase1_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)>> ** **callback_generate** -  Callback function responsible for creating and filling the source mesh. Executed in the main thread. The function must be wrapped using *[MakeCallback()](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Classm_RetClassm)* and have the following signature: ```cpp void callback_generate(Ptr<Mesh> mesh) ```
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cpp.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cpp.md)*.

### Return value

true if the modification was completed and applied successfully, otherwise false
## bool runGenerateMeshProceduralAsync ( CallbackBase1 < Ptr < Mesh >> * callback_generate , CallbackBase * callback_done , int mesh_render_flags = 0 )

**[ Main Thread ]**
Starts asynchronous generation of procedural mesh data. The *callback_generate* function is executed in a background thread and must create and fill a mesh object with new data. The generated mesh will be transferred to the object once complete, without blocking the main thread. After the mesh has been applied to the object, the optional callback_done will be called. Works only when **procedural mode is enabled**.


Note that the callback is executed in a single dedicated thread controlled by the engine, it is not parallelized and must not spawn additional threads.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *[CallbackBase1](../../../api/library/common/callbacks/class.callbackbase1_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)>> ** **callback_generate** -  Callback function responsible for creating and filling the source mesh. Executed in the main thread. The function must be wrapped using *[MakeCallback()](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Classm_RetClassm)* and have the following signature: ```cpp void callback_generate(Ptr<Mesh> mesh) ```
- *[CallbackBase](../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **callback_done** -  Optional callback executed after geometry has been fully applied. The function must be wrapped using *[MakeCallback()](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Classm_RetClassm)* and have the following signature: ```cpp void callback_done() ```
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cpp.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cpp.md)*.

### Return value

true if the generation was completed and applied successfully, otherwise false
## bool runGenerateMeshProceduralForce ( CallbackBase1 < Ptr < Mesh >> * callback_generate , int mesh_render_flags = 0 )

**[ Main Thread ]**
Starts immediate (forced) generation of procedural mesh data. The *callback_generate* function is executed in the main thread and must create and fill a mesh object with new data. The generated mesh is applied to the object as soon as generation completes. Works only when **procedural mode is enabled**.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *[CallbackBase1](../../../api/library/common/callbacks/class.callbackbase1_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)>> ** **callback_generate** -  Callback function responsible for creating and filling the source mesh. Executed in the main thread. The function must be wrapped using *[MakeCallback()](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Classm_RetClassm)* and have the following signature: ```cpp void callback_generate(Ptr<Mesh> mesh) ```
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cpp.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cpp.md)*.

### Return value

true if the generation was completed and applied successfully, otherwise false
## bool runGenerateMeshProceduralForce ( CallbackBase1 < Ptr < Mesh >> * callback_generate , CallbackBase * callback_done , int mesh_render_flags = 0 )

**[ Main Thread ]**
Starts immediate (forced) generation of procedural mesh data. The *callback_generate* function is executed in the main thread and must create and fill a Mesh object with vertex data. Once the mesh is applied to the object, the optional *callback_done* is called on the main thread. Works only when **procedural mode is enabled**.


> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *[CallbackBase1](../../../api/library/common/callbacks/class.callbackbase1_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)>> ** **callback_generate** -  Callback function responsible for creating and filling the source mesh. Executed in the main thread. The function must be wrapped using *[MakeCallback()](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Classm_RetClassm)* and have the following signature: ```cpp void callback_generate(Ptr<Mesh> mesh) ```
- *[CallbackBase](../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **callback_done** -  Optional callback executed after geometry has been fully applied. The function must be wrapped using *[MakeCallback()](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Classm_RetClassm)* and have the following signature: ```cpp void callback_done() ```
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cpp.md#USAGE_DYNAMIC_VERTEX) for *[MeshRender](../../../api/library/rendering/class.meshrender_cpp.md)*.

### Return value

true if the generation was completed and applied successfully, otherwise false
