# ObjectMeshClutter Class (CS)

**Inherits from:** Object


[MeshClutter](../../../objects/objects/mesh_clutter/index.md) is used to scatter identical meshes (with the same material applied to their surfaces), as well as randomly scale and orient them. Scattered meshes are baked into one object, which allows for less cluttered spatial tree, reduces the number of texture fetches and speeds up rendering.


Meshes are rendered within a specified [distance](#setVisibleDistance_float_void) from the camera. Further than this distance, nodes [fade out](#setFadeDistance_float_void) and then disappear completely.


You can use [a mask](#setCutoutIntersectionMask_int_void) to cut out clutter objects in the areas of intersection with other objects and decals (e.g. to remove vegetation under houses or from the surface of roads projected using decals).


### Important Notes


The number of clutter elements in each cell is determined by the clutter *Size* along *[X](#setSizeX_float_void)* and *[Y](#setSizeY_float_void)* axes, as well as by *[Density](#setDensity_float_void)* and *[Step](#setStep_float_void)* values. Relationship between these values in internal calculations may result in an invisible clutter (generated with empty cells), when the calculated density for cells becomes lower than 1 (each cell will have "less than 1 element" - meaning no clutter elements at all). Please take it into account when setting these values.


Number of clutter cells is calculated using the following formulas:


```cpp
num_cells_x = max(Math::ftoi(Math::ceil(clutter_size_x / step)), 1);
num_cells_y = max(Math::ftoi(Math::ceil(clutter_size_y / step)), 1);

```


The size of each cell along X and Y axes is calculated as follows:


```cpp
cell_size_x = clutter_size_x / Math::itof(num_cells_x);
cell_size_y = clutter_size_y / Math::itof(num_cells_y);

```


And the resulting cell density:


```cpp
cell_density = cell_size_x * cell_size_y * density;

```


**Example:**


The default *[Step](#setStep_float_void)* and *[Density](#setDensity_float_void)* values for the clutter are equal to 1.0f. Setting clutter size along any of the axes to a non-integer value with a non-zero fractional part (e.g., 200.1) automatically increases the number of cells along the corresponding axis by 1 (e.g. 201 instead of 200). This results in a cell size < 1, which makes cell density drop below 1.


## ObjectMeshClutter Class

### Properties

## int CutoutInverse

The value indicating if the clutter objects is rendered inside or outside the areas determined by the [cutout intersection mask](#setCutoutIntersectionMask_int_void).
## int CutoutIntersectionMask

The cutout intersection mask. this mask allows you to cut out clutter objects in the areas of intersection with other objects and decals (e.g. can be used to remove vegetation under houses or from the surface of roads projected using decals). clutter objects will be cut out by objects and decals that have their intersection mask matching this one (one bit at least).
> **Notice:** To set intersection masks the following methods can be used:
> - **for decals** use *[getIntersectionMask()](../../../api/library/decals/class.decal_cs.md#getIntersectionMask_int)*
> - **for objects** use *[getIntersectionMask()](../../../api/library/objects/class.object_cs.md#getIntersectionMask_int_int)*

## int MaskInverse

The flag indicating if clutter meshes are rendered inside or outside the mask mesh contour.
## string MaskMeshName

The name (path) of the current mesh used as a mask for the mesh clutter. this mesh should be plane.
## int MaskMaxValue

The maximum value of the mask application range, **[0;255]**.
## int MaskMinValue

The minimum value of the mask application range.
## int MaskFlipY

The flag indicating if a mask is flipped by y axis.
## int MaskFlipX

The flag indicating if a mask is flipped by x axis.
## string MaskImageName

The name of a mask image (in *R8* format) that defines the placement of meshes.
## float Angle

The angle cosine that defines the slope steepness appropriate for positioning meshes. The provided value will be clipped in range **[0;1]**.
## float Threshold

The density threshold (for a mask) starting from which meshes are rendered if placed dense enough.
## float Density

The density factor that defines the number of meshes per square unit.
> **Notice:** The number of clutter elements in each cell is determined by the clutter *Size* along X and Y axes, as well as by *[Density](#setDensity_float_void)* and *[Step](#setStep_float_void)* values. Relationship between these values in internal calculations **may result in an invisible clutter**. When setting these values, please consider [this information](#important_notes).

## float Step

The step for cells used to render meshes scattered by the mesh clutter.
> **Notice:** The number of clutter elements in each cell is determined by the clutter *Size* along X and Y axes, as well as by *[Density](#setDensity_float_void)* and *[Step](#setStep_float_void)* values. Relationship between these values in internal calculations **may result in an invisible clutter**. When setting these values, please consider [this information](#important_notes).

## float SizeX

The width of the mesh clutter along the X-axis, in units. If a negative value is provided, **0** will be used instead.
> **Notice:** The number of clutter elements in each cell is determined by the clutter *Size* along X and Y axes, as well as by *[Density](#setDensity_float_void)* and *[Step](#setStep_float_void)* values. Relationship between these values in internal calculations **may result in an invisible clutter**. When setting these values, please consider [this information](#important_notes).

## float SizeY

The length of the mesh clutter along the Y-axis, in units. If a negative value is provided, **0** will be used instead.
> **Notice:** The number of clutter elements in each cell is determined by the clutter *Size* along X and Y axes, as well as by *[Density](#setDensity_float_void)* and *[Step](#setStep_float_void)* values. Relationship between these values in internal calculations **may result in an invisible clutter**. When setting these values, please consider [this information](#important_notes).

## int Seed

The seed used for pseudo-random positioning of meshes. If a negative value is provided, **0** will be used instead.
## float FadeDistance

The distance up to which meshes scattered by the mesh clutter are fading out (that is, fewer meshes will be rendered instead of all). the distance is measured starting from the [visible distance](#setVisibleDistance_float_void). If a negative value is provided, **0** will be used instead.
> **Notice:** In order for a fade distance to be applied, [visibility distance](#getVisibleDistance_float) should not be infinite.

## float VisibleDistance

The distance up to which meshes scattered by the mesh clutter are rendered. If a negative value is provided, **0** will be used instead.
## bool Intersection

The value indicating whether meshes are scattered upon the ground (along its relief): either the terrain or a mesh set as a parent node.
## bool Orientation

The value indicating whether meshes are oriented along the normals of the ground (either the terrain or a mesh set as a parent node).
## bool Collision

The value indicating if collisions with the object should be taken into account.
> **Notice:** If the return value is **0** the new geometry will never be generated by collision detection request.

## int TerrainMask

The index of the [Landscape Terrain mask](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cs.md#getDetailMask_int_TerrainDetailMask) currently used to define placement of meshes, in the [0; 19] range.
## string MeshPath

The path to the source *.mesh*-file of the mesh scattered by mesh clutter.
> **Notice:** Setting a new path does not update the mesh immediately. If the mesh is in the procedural mode, it will be reset.

## 🔒︎ bool IsMeshLoadedVRAM

The value indicating if the source mesh used for the object is loaded to video memory (VRAM).
## 🔒︎ bool IsMeshLoadedRAM

The value indicating if the source mesh used for the object is loaded to memory (RAM).
## 🔒︎ bool IsMeshNull

The value indicating if the source mesh used for the object is null (does not exist, unassigned, not loaded, etc.).
## 🔒︎ ObjectMeshStatic.PROCEDURAL_MODE MeshProceduralMode

The value indicating if the source mesh used for the object is [procedural](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE). A procedural mesh is a [mesh](../../../api/library/rendering/class.mesh_cs.md) created via code, such meshes have a specific streaming mode - they are always kept in memory after creation and never unloaded until the object is destroyed via code or the mesh returns to its normal mode (streaming from a source file). Changing of the static mesh is possible only if it is in the procedural mode.
## int IntersectionMask

The intersection mask for the world clutter. This mask can be used to cut out areas intersected by the world clutter from [grass](../../../api/library/objects/class.objectgrass_cs.md#setCutoutIntersectionMask_int_void), [mesh clutter](../../../api/library/objects/class.objectmeshclutter_cs.md#setCutoutIntersectionMask_int_void) and another [world clutter](#setCutoutIntersectionMask_int_void) (e.g. to remove grass or forest from the surface of roads projected using decals).
> **Notice:** The areas will be cut out only if intersection masks of grass and clutter objects matches this mask (one bit at least).

## 🔒︎ bool IsMeshProceduralDynamic

The value indicating if the current procedural mode is *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_DYNAMIC)*.
## 🔒︎ bool IsMeshProceduralActive

The value indicating if an asynchronous operation on the procedural mesh is currently in progress.
## 🔒︎ bool IsMeshProceduralDone

The value indicating if all asynchronous operations on the procedural mesh have completed.
### Members

---

## ObjectMeshClutter ( string path )

ObjectMeshClutter constructor. Creates a clutter using the path to the source mesh provided.
### Arguments

- *string* **path** - Path to the source mesh file.

## ObjectMeshClutter ( )

Default ObjectMeshClutter constructor. Creates an empty clutter.
## int SetMaskImage ( Image image , bool invalidate = 1 )

Sets an image (in *R8* format) as a mask, that defines placement of meshes.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image instance.
- *bool* **invalidate** - Invalidate flag. Set true to invalidate all mesh clutter cells; otherwise, set false. All invalidated cells will be regenerated.

### Return value

**1** if the mask image is successfully set; otherwise, **0**.
## int GetMaskImage ( Image image )

Writes the image that is currently used as a mask for placement of meshes to the given buffer.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image buffer to store a mask into.

### Return value

**1** if the mask image is successfully written into the buffer; otherwise, **0**.
## void SetMaskImageName ( string image_name , bool invalidate = 1 )

Sets the path to a mask image (in *R8* format) that defines the placement of meshes.
### Arguments

- *string* **image_name** - Path to the mask image.
- *bool* **invalidate** - Invalidate flag. Set true to invalidate all mesh clutter cells; otherwise, set false. All invalidated cells will be regenerated.

## int SetMaskMesh ( Mesh mesh , bool invalidate = true )

Sets a mesh to be used as a mask on-the-fly. Limitations:
- Before the method is called, another mesh must be set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void) first.
- If the world is reloaded, the mesh set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void) will be loaded.
- If the memory limit is exceeded, the new mesh might be replaced with the mesh set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void).


### Arguments

- *Mesh* **mesh**
- *bool* **invalidate** - Invalidate flag. Set true to invalidate all mesh clutter cells; otherwise, set false. All invalidated cells will be regenerated.

### Return value

**1** if the mesh is set successfully; otherwise - **0**.
## int GetMaskMesh ( Mesh mesh )

Copies the current mask mesh (if it exists) to the specified target mesh.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Mesh instance to copy the current mask mesh to.

### Return value

**1** if mesh mask exists; otherwise - **0**.
## void SetMaskMeshName ( string mesh_name , bool invalidate = 1 )

Sets a mesh to be used as a mask for the mesh clutter. This mesh should be plane.
### Arguments

- *string* **mesh_name** - Path to the **.mesh* file.
- *bool* **invalidate** - Invalidate flag. Set true to invalidate all mesh clutter cells; otherwise, set false. All invalidated cells will be regenerated.

## void CreateClutterTransforms ( )

Creates transformations for all clutter meshes.
## void SetMaxScale ( float mean , float spread )

Sets the scale for meshes in the areas with high density (according to the mask). With the minimum scale it is possible to automatically render, for example, big trees in the center of the forest. A spread value allows you to control the range of scales relative to the mean value.
### Arguments

- *float* **mean** - Scale mean value.
- *float* **spread** - Maximum spread value to randomly upscale or downscale objects.

## float GetMaxScaleMean ( )

Returns the scale mean value for meshes in the areas with high density (according to the mask).
### Return value

Scale mean value.
## float GetMaxScaleSpread ( )

Returns the scale spread value that controls the range of mesh scales in the areas with high density (according to the mask).
### Return value

Scale spread value.
## void SetMeshesRotation ( vec3 mean , vec3 spread )

Sets the parameters of pseudo-random rotation of meshes along X, Y and Z axes.
### Arguments

- *vec3* **mean** - Mean values of meshes rotation angles, in degrees.
- *vec3* **spread** - Maximum spread values of meshes rotation angles, in degrees.

## vec3 GetMeshesRotationMean ( )

Returns the vector of mean values of meshes rotation along X, Y and Z axes.
### Return value

Mean values of meshes rotation angles, in degrees.
## vec3 GetMeshesRotationSpread ( )

Returns the vector of spread values of meshes rotation along X, Y and Z axes.
### Return value

Maximum spread values of meshes rotation angles, in degrees.
## void SetMinScale ( float mean , float spread )

Sets the scale for meshes in the areas with low density (according to the mask). With the minimum scale it is possible to automatically render, for example, small trees at the forest border. A spread value allows you to control the range of scales relative to the mean value.
### Arguments

- *float* **mean** - Scale mean value.
- *float* **spread** - Maximum spread value to randomly upscale or downscale objects.

## float GetMinScaleMean ( )

Returns the scale mean value for meshes in the areas with low density (according to the mask).
### Return value

Scale mean value.
## float GetMinScaleSpread ( )

Returns the scale spread value that controls the range of mesh scales in the areas with low density (according to the mask).
### Return value

Scale spread value.
## void SetOffset ( float mean , float spread )

Sets the vertical offset that determines the placement of meshes above or below the surface.
### Arguments

- *float* **mean** - Mean value of the offset in units.
- *float* **spread** - Spread value of the offset in units.

## float GetOffsetMean ( )

Returns the current mean value of the vertical offset that determines the placement of meshes above or below the surface.
### Return value

Mean value of the offset in units.
## float GetOffsetSpread ( )

Returns the current spread value of the vertical offset that determines the placement of meshes above or below the surface.
### Return value

Spread value of the offset in units.
## void Invalidate ( )

Invalidates all mesh clutter cells. All invalidated cells will be regenerated.
## void Invalidate ( WorldBoundBox bounds )

Invalidates all mesh clutter cells within the area specified by the given bounding box. All invalidated cells will be regenerated.
### Arguments

- *[WorldBoundBox](../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bounds** - Bounding box, defining the area, where mesh clutter cells will be regenerated.

## static int type ( )

Returns the node type.
### Return value

[Node](../../../api/library/nodes/class.node_cs.md) type identifier.
## void ClearClutterExcludes ( )

Restores all cells removed by the calls to the [setClutterExclude()](#setClutterExclude_WorldBoundBox_int_void) method. Restored cells will be regenerated.
## void SetClutterExclude ( WorldBoundBox bounds , int exclude )

Removes all cells within the area specified by the given bounding box. Generation of these cells will be skipped. This method can be used to replace some parts of the clutter with modified meshes (e.g., broken trees within the area around the shell crater in the forest).
### Arguments

- *[WorldBoundBox](../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bounds** - Bounding box, defining the area, where mesh clutter cells will not be generated.
- *int* **exclude** - Exclude flag. Set **1** to remove all mesh clutter cells within the area; otherwise, set **0** to restore the removed ones. Restored cells will be regenerated.

## bool GetClutterTransforms ( WorldBoundBox bounds , mat4[] OUT_transforms , bool precise = 1 , bool force = 1 )

Collects transformations for all clutter meshes in the generated cells within the area specified by the given bounding box and puts them to the specified buffer.
> **Notice:** Generation of clutter cells is performed in separate threads. Some of the cells may have their lifetime expired. Therefore, the content of certain cells might be unavailable at the moment, such cells are considered as not generated.


### Arguments

- *[WorldBoundBox](../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bounds** - Bounding box, defining the area, for which the transformations of clutter meshes are to be collected.
- *mat4[]* **OUT_transforms** - Buffer to store transformations of clutter meshes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *bool* **precise** - Precision flag:

  - **1** - transformations will be collected for clutter meshes within the specified bounding box
  - **0** - transformations will be collected for clutter meshes within the cells intersected by the specified bounding box
- *bool* **force** - Force flag.

  - **1** - regenerate all cells within the area, that were not generated, before collecting transformations for the meshes inside them.
  - **0** - transformations will be collected only for the meshes inside the clutter cells, that were generated.

### Return value

true, if there are transformations of clutter meshes; or false, if there are no transformations of clutter meshes found.
## bool GetClutterTransforms ( mat4[] OUT_transforms )

Collects transformations for all clutter meshes within the generated cells and puts them to the specified buffer.
> **Notice:** Generation of clutter cells is performed in separate threads. Some of the cells may have their lifetime expired. Therefore, the content of certain cells might be unavailable at the moment, such cells are considered as not generated.


### Arguments

- *mat4[]* **OUT_transforms** - Buffer to store transformations of clutter meshes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true, if there are transformations of clutter meshes; or false, if there are no transformations of clutter meshes found.
## bool GetClutterWorldTransforms ( WorldBoundBox bounds , mat4[] OUT_transforms , bool precise = 1 , bool force = 1 )

Collects transformations (in world coordinates) for all clutter meshes in the generated cells within the area specified by the given bounding box and puts them to the specified buffer.
> **Notice:** Generation of clutter cells is performed in separate threads. Some of the cells may have their lifetime expired. Therefore, the content of certain cells might be unavailable at the moment, such cells are considered as not generated.


### Arguments

- *[WorldBoundBox](../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bounds** - Bounding box, defining the area, for which the transformations of clutter meshes are to be collected.
- *mat4[]* **OUT_transforms** - Buffer to store transformations of clutter meshes, in world coordinates. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *bool* **precise** - Precision flag:

  - **1** - transformations will be collected for clutter meshes within the specified bounding box
  - **0** - transformations will be collected for clutter meshes within the cells intersected by the specified bounding box
- *bool* **force** - Force flag.

  - **1** - regenerate all cells within the area, that were not generated, before collecting transformations for the meshes inside them.
  - **0** - transformations will be collected only for the meshes inside the clutter cells, that were generated.

### Return value

true, if there are transformations of clutter meshes; or false, if there are no transformations of clutter meshes found.
## bool GetClutterWorldTransforms ( mat4[] OUT_transforms )

Collects transformations (in world coordinates) for all clutter meshes within the generated cells and puts them to the specified buffer.
> **Notice:** Generation of clutter cells is performed in separate threads. Some of the cells may have their lifetime expired. Therefore, the content of certain cells might be unavailable at the moment, such cells are considered as not generated.


### Arguments

- *mat4[]* **OUT_transforms** - Buffer to store transformations of clutter meshes, in world coordinates. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true, if there are transformations of clutter meshes; or false, if there are no transformations of clutter meshes found.
## int GetClutterLocalTransforms ( BoundBox bounds , mat4[] OUT_transforms , int precise = 1 , int force = 1 )

Collects transformations (in local coordinates) for all clutter meshes within the generated cells and puts them to the specified buffer.
> **Notice:** Generation of clutter cells is performed in separate threads. Some of the cells may have their lifetime expired. Therefore, the content of certain cells might be unavailable at the moment, such cells are considered as not generated.


### Arguments

- *[BoundBox](../../../api/library/math/cs/bounds/boundbox_cs.md)* **bounds** - Bounding box, defining the area, for which the transformations of clutter meshes are to be collected.
- *mat4[]* **OUT_transforms** - Buffer to store transformations of clutter meshes, in local coordinates. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **precise** - Precision flag:

  - **1** - transformations will be collected for clutter meshes within the specified bounding box
  - **0** - transformations will be collected for clutter meshes within the cells intersected by the specified bounding box
- *int* **force** - Force flag.

  - **1** - regenerate all cells within the area, that were not generated, before collecting transformations for the meshes inside them.
  - **0** - transformations will be collected only for the meshes inside the clutter cells, that were generated.

### Return value

true, if there are transformations of clutter meshes; or false, if there are no transformations of clutter meshes found.
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

- *[ObjectMeshStatic.PROCEDURAL_MODE](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE)* **mode** - One of the *[PROCEDURAL_MODE](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE)* to apply to the mesh.
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
