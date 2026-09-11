# ObjectMeshClutter Class (CPP)

**Header:** #include <UnigineObjects.h>

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

### Members

## void setCutoutInverse ( int inverse )

Sets a new value indicating if the clutter objects is rendered inside or outside the areas determined by the [cutout intersection mask](#setCutoutIntersectionMask_int_void).
### Arguments

- *int* **inverse** - The value indicating if the clutter objects is rendered inside or outside the areas determined by the cutout intersection mask

## int getCutoutInverse () const

Returns the current value indicating if the clutter objects is rendered inside or outside the areas determined by the [cutout intersection mask](#setCutoutIntersectionMask_int_void).
### Return value

Current value indicating if the clutter objects is rendered inside or outside the areas determined by the cutout intersection mask
## void setCutoutIntersectionMask ( int mask )

Sets a new cutout intersection mask. this mask allows you to cut out clutter objects in the areas of intersection with other objects and decals (e.g. can be used to remove vegetation under houses or from the surface of roads projected using decals). clutter objects will be cut out by objects and decals that have their intersection mask matching this one (one bit at least).
> **Notice:** To set intersection masks the following methods can be used:
> - **for decals** use *[getIntersectionMask()](../../../api/library/decals/class.decal_cpp.md#getIntersectionMask_int)*
> - **for objects** use *[getIntersectionMask()](../../../api/library/objects/class.object_cpp.md#getIntersectionMask_int_int)*

### Arguments

- *int* **mask** - The cutout intersection mask

## int getCutoutIntersectionMask () const

Returns the current cutout intersection mask. this mask allows you to cut out clutter objects in the areas of intersection with other objects and decals (e.g. can be used to remove vegetation under houses or from the surface of roads projected using decals). clutter objects will be cut out by objects and decals that have their intersection mask matching this one (one bit at least).
> **Notice:** To set intersection masks the following methods can be used:
> - **for decals** use *[getIntersectionMask()](../../../api/library/decals/class.decal_cpp.md#getIntersectionMask_int)*
> - **for objects** use *[getIntersectionMask()](../../../api/library/objects/class.object_cpp.md#getIntersectionMask_int_int)*

### Return value

Current cutout intersection mask
## void setMaskInverse ( int inverse )

Sets a new flag indicating if clutter meshes are rendered inside or outside the mask mesh contour.
### Arguments

- *int* **inverse** - The flag indicating if clutter meshes are rendered inside or outside the mask mesh contour

## int getMaskInverse () const

Returns the current flag indicating if clutter meshes are rendered inside or outside the mask mesh contour.
### Return value

Current flag indicating if clutter meshes are rendered inside or outside the mask mesh contour
## void setMaskMeshName ( const char * name )

Sets a new name (path) of the current mesh used as a mask for the mesh clutter. this mesh should be plane.
### Arguments

- *const char ** **name** - The name (path) of the current mesh used as a mask for the mesh clutter

## const char * getMaskMeshName () const

Returns the current name (path) of the current mesh used as a mask for the mesh clutter. this mesh should be plane.
### Return value

Current name (path) of the current mesh used as a mask for the mesh clutter
## void setMaskMaxValue ( int value )

Sets a new maximum value of the mask application range, **[0;255]**.
### Arguments

- *int* **value** - The maximum value of the mask application range

## int getMaskMaxValue () const

Returns the current maximum value of the mask application range, **[0;255]**.
### Return value

Current maximum value of the mask application range
## void setMaskMinValue ( int value )

Sets a new minimum value of the mask application range.
### Arguments

- *int* **value** - The minimum value of the mask application range

## int getMaskMinValue () const

Returns the current minimum value of the mask application range.
### Return value

Current minimum value of the mask application range
## void setMaskFlipY ( int y )

Sets a new flag indicating if a mask is flipped by y axis.
### Arguments

- *int* **y** - The flag indicating if a mask is flipped by y axis

## int getMaskFlipY () const

Returns the current flag indicating if a mask is flipped by y axis.
### Return value

Current flag indicating if a mask is flipped by y axis
## void setMaskFlipX ( int x )

Sets a new flag indicating if a mask is flipped by x axis.
### Arguments

- *int* **x** - The flag indicating if a mask is flipped by x axis

## int getMaskFlipX () const

Returns the current flag indicating if a mask is flipped by x axis.
### Return value

Current flag indicating if a mask is flipped by x axis
## void setMaskImageName ( const char * name )

Sets a new name of a mask image (in *R8* format) that defines the placement of meshes.
### Arguments

- *const char ** **name** - The name of a mask image (in R8 format) that defines the placement of meshes

## const char * getMaskImageName () const

Returns the current name of a mask image (in *R8* format) that defines the placement of meshes.
### Return value

Current name of a mask image (in R8 format) that defines the placement of meshes
## void setAngle ( float angle )

Sets a new angle cosine that defines the slope steepness appropriate for positioning meshes. The provided value will be clipped in range **[0;1]**.
### Arguments

- *float* **angle** - The angle cosine that defines the slope steepness appropriate for positioning meshes

## float getAngle () const

Returns the current angle cosine that defines the slope steepness appropriate for positioning meshes. The provided value will be clipped in range **[0;1]**.
### Return value

Current angle cosine that defines the slope steepness appropriate for positioning meshes
## void setThreshold ( float threshold )

Sets a new density threshold (for a mask) starting from which meshes are rendered if placed dense enough.
### Arguments

- *float* **threshold** - The density threshold (for a mask) starting from which meshes are rendered if placed dense enough

## float getThreshold () const

Returns the current density threshold (for a mask) starting from which meshes are rendered if placed dense enough.
### Return value

Current density threshold (for a mask) starting from which meshes are rendered if placed dense enough
## void setDensity ( float density )

Sets a new density factor that defines the number of meshes per square unit.
> **Notice:** The number of clutter elements in each cell is determined by the clutter *Size* along X and Y axes, as well as by *[Density](#setDensity_float_void)* and *[Step](#setStep_float_void)* values. Relationship between these values in internal calculations **may result in an invisible clutter**. When setting these values, please consider [this information](#important_notes).

### Arguments

- *float* **density** - The density factor that defines the number of meshes per square unit

## float getDensity () const

Returns the current density factor that defines the number of meshes per square unit.
> **Notice:** The number of clutter elements in each cell is determined by the clutter *Size* along X and Y axes, as well as by *[Density](#setDensity_float_void)* and *[Step](#setStep_float_void)* values. Relationship between these values in internal calculations **may result in an invisible clutter**. When setting these values, please consider [this information](#important_notes).

### Return value

Current density factor that defines the number of meshes per square unit
## void setStep ( float step )

Sets a new step for cells used to render meshes scattered by the mesh clutter.
> **Notice:** The number of clutter elements in each cell is determined by the clutter *Size* along X and Y axes, as well as by *[Density](#setDensity_float_void)* and *[Step](#setStep_float_void)* values. Relationship between these values in internal calculations **may result in an invisible clutter**. When setting these values, please consider [this information](#important_notes).

### Arguments

- *float* **step** - The step for cells used to render meshes scattered by the mesh clutter

## float getStep () const

Returns the current step for cells used to render meshes scattered by the mesh clutter.
> **Notice:** The number of clutter elements in each cell is determined by the clutter *Size* along X and Y axes, as well as by *[Density](#setDensity_float_void)* and *[Step](#setStep_float_void)* values. Relationship between these values in internal calculations **may result in an invisible clutter**. When setting these values, please consider [this information](#important_notes).

### Return value

Current step for cells used to render meshes scattered by the mesh clutter
## void setSizeX ( float x )

Sets a new width of the mesh clutter along the X-axis, in units. If a negative value is provided, **0** will be used instead.
> **Notice:** The number of clutter elements in each cell is determined by the clutter *Size* along X and Y axes, as well as by *[Density](#setDensity_float_void)* and *[Step](#setStep_float_void)* values. Relationship between these values in internal calculations **may result in an invisible clutter**. When setting these values, please consider [this information](#important_notes).

### Arguments

- *float* **x** - The width of the mesh clutter along the X-axis

## float getSizeX () const

Returns the current width of the mesh clutter along the X-axis, in units. If a negative value is provided, **0** will be used instead.
> **Notice:** The number of clutter elements in each cell is determined by the clutter *Size* along X and Y axes, as well as by *[Density](#setDensity_float_void)* and *[Step](#setStep_float_void)* values. Relationship between these values in internal calculations **may result in an invisible clutter**. When setting these values, please consider [this information](#important_notes).

### Return value

Current width of the mesh clutter along the X-axis
## void setSizeY ( float y )

Sets a new length of the mesh clutter along the Y-axis, in units. If a negative value is provided, **0** will be used instead.
> **Notice:** The number of clutter elements in each cell is determined by the clutter *Size* along X and Y axes, as well as by *[Density](#setDensity_float_void)* and *[Step](#setStep_float_void)* values. Relationship between these values in internal calculations **may result in an invisible clutter**. When setting these values, please consider [this information](#important_notes).

### Arguments

- *float* **y** - The length of the mesh clutter along the Y-axis

## float getSizeY () const

Returns the current length of the mesh clutter along the Y-axis, in units. If a negative value is provided, **0** will be used instead.
> **Notice:** The number of clutter elements in each cell is determined by the clutter *Size* along X and Y axes, as well as by *[Density](#setDensity_float_void)* and *[Step](#setStep_float_void)* values. Relationship between these values in internal calculations **may result in an invisible clutter**. When setting these values, please consider [this information](#important_notes).

### Return value

Current length of the mesh clutter along the Y-axis
## void setSeed ( int seed )

Sets a new seed used for pseudo-random positioning of meshes. If a negative value is provided, **0** will be used instead.
### Arguments

- *int* **seed** - The seed used for pseudo-random positioning of meshes

## int getSeed () const

Returns the current seed used for pseudo-random positioning of meshes. If a negative value is provided, **0** will be used instead.
### Return value

Current seed used for pseudo-random positioning of meshes
## void setFadeDistance ( float distance )

Sets a new distance up to which meshes scattered by the mesh clutter are fading out (that is, fewer meshes will be rendered instead of all). the distance is measured starting from the [visible distance](#setVisibleDistance_float_void). If a negative value is provided, **0** will be used instead.
> **Notice:** In order for a fade distance to be applied, [visibility distance](#getVisibleDistance_float) should not be infinite.

### Arguments

- *float* **distance** - The distance up to which meshes scattered by the mesh clutter are fading out

## float getFadeDistance () const

Returns the current distance up to which meshes scattered by the mesh clutter are fading out (that is, fewer meshes will be rendered instead of all). the distance is measured starting from the [visible distance](#setVisibleDistance_float_void). If a negative value is provided, **0** will be used instead.
> **Notice:** In order for a fade distance to be applied, [visibility distance](#getVisibleDistance_float) should not be infinite.

### Return value

Current distance up to which meshes scattered by the mesh clutter are fading out
## void setVisibleDistance ( float distance )

Sets a new distance up to which meshes scattered by the mesh clutter are rendered. If a negative value is provided, **0** will be used instead.
### Arguments

- *float* **distance** - The distance up to which meshes scattered by the mesh clutter are rendered

## float getVisibleDistance () const

Returns the current distance up to which meshes scattered by the mesh clutter are rendered. If a negative value is provided, **0** will be used instead.
### Return value

Current distance up to which meshes scattered by the mesh clutter are rendered
## void setIntersection ( bool intersection )

Sets a new value indicating whether meshes are scattered upon the ground (along its relief): either the terrain or a mesh set as a parent node.
### Arguments

- *bool* **intersection** - value indicating whether meshes are scattered upon the ground (along its relief): either the terrain or a mesh set as a parent node

## bool getIntersection () const

Returns the current value indicating whether meshes are scattered upon the ground (along its relief): either the terrain or a mesh set as a parent node.
### Return value

value indicating whether meshes are scattered upon the ground (along its relief): either the terrain or a mesh set as a parent node
## void setOrientation ( bool orientation )

Sets a new value indicating whether meshes are oriented along the normals of the ground (either the terrain or a mesh set as a parent node).
### Arguments

- *bool* **orientation** - value indicating whether meshes are oriented along the normals of the ground (either the terrain or a mesh set as a parent node)

## bool getOrientation () const

Returns the current value indicating whether meshes are oriented along the normals of the ground (either the terrain or a mesh set as a parent node).
### Return value

value indicating whether meshes are oriented along the normals of the ground (either the terrain or a mesh set as a parent node)
## void setCollision ( bool collision )

Sets a new value indicating if collisions with the object should be taken into account.
> **Notice:** If the return value is **0** the new geometry will never be generated by collision detection request.

### Arguments

- *bool* **collision** - value indicating if collisions with the object should be taken into account

## bool getCollision () const

Returns the current value indicating if collisions with the object should be taken into account.
> **Notice:** If the return value is **0** the new geometry will never be generated by collision detection request.

### Return value

value indicating if collisions with the object should be taken into account
## void setTerrainMask ( int mask )

Sets a new index of the [Landscape Terrain mask](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md#getDetailMask_int_TerrainDetailMask) currently used to define placement of meshes, in the [0; 19] range.
### Arguments

- *int* **mask** - The index of the Landscape Terrain mask currently used to define placement of meshes

## int getTerrainMask () const

Returns the current index of the [Landscape Terrain mask](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md#getDetailMask_int_TerrainDetailMask) currently used to define placement of meshes, in the [0; 19] range.
### Return value

Current index of the Landscape Terrain mask currently used to define placement of meshes
## void setMeshPath ( const char * path )

Sets a new path to the source *.mesh*-file of the mesh scattered by mesh clutter.
> **Notice:** Setting a new path does not update the mesh immediately. If the mesh is in the procedural mode, it will be reset.

### Arguments

- *const char ** **path** - The path to the source .mesh-file of the mesh scattered by mesh clutter

## const char * getMeshPath () const

Returns the current path to the source *.mesh*-file of the mesh scattered by mesh clutter.
> **Notice:** Setting a new path does not update the mesh immediately. If the mesh is in the procedural mode, it will be reset.

### Return value

Current path to the source .mesh-file of the mesh scattered by mesh clutter
## bool isMeshLoadedVRAM () const

Returns the current value indicating if the source mesh used for the object is loaded to video memory (VRAM).
### Return value

**true** if the source mesh used for the object is loaded to video memory (VRAM); otherwise **false**.
## bool isMeshLoadedRAM () const

Returns the current value indicating if the source mesh used for the object is loaded to memory (RAM).
### Return value

**true** if the source mesh used for the object is loaded to memory (RAM); otherwise **false**.
## bool isMeshNull () const

Returns the current value indicating if the source mesh used for the object is null (does not exist, unassigned, not loaded, etc.).
### Return value

**true** if the source mesh used for the object is null (does not exist, unassigned, not loaded, etc.); otherwise **false**.
## ObjectMeshStatic::PROCEDURAL_MODE getMeshProceduralMode () const

Returns the current value indicating if the source mesh used for the object is [procedural](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE). A procedural mesh is a [mesh](../../../api/library/rendering/class.mesh_cpp.md) created via code, such meshes have a specific streaming mode - they are always kept in memory after creation and never unloaded until the object is destroyed via code or the mesh returns to its normal mode (streaming from a source file). Changing of the static mesh is possible only if it is in the procedural mode.
### Return value

Current procedural mode of the source mesh used for the object
## bool isMeshProceduralDynamic () const

Returns the current value indicating if the current procedural mode is *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_DYNAMIC)*.
### Return value

**true** if the current procedural mode is PROCEDURAL_MODE_DYNAMIC; otherwise **false**.
## bool isMeshProceduralActive () const

Returns the current value indicating if an asynchronous operation on the procedural mesh is currently in progress.
### Return value

**true** if an asynchronous operation on the procedural mesh is currently in progress; otherwise **false**.
## bool isMeshProceduralDone () const

Returns the current value indicating if all asynchronous operations on the procedural mesh have completed.
### Return value

**true** if all asynchronous operations on the procedural mesh have completed; otherwise **false**.
---

## static ObjectMeshClutterPtr create ( const char * path )

ObjectMeshClutter constructor. Creates a clutter using the path to the source mesh provided.
### Arguments

- *const char ** **path** - Path to the source mesh file.

## static ObjectMeshClutterPtr create ( )

Default ObjectMeshClutter constructor. Creates an empty clutter.
## int setMaskImage ( const Ptr < Image > & image , bool invalidate = 1 )

Sets an image (in *R8* format) as a mask, that defines placement of meshes.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image smart pointer.
- *bool* **invalidate** - Invalidate flag. Set true to invalidate all mesh clutter cells; otherwise, set false. All invalidated cells will be regenerated.

### Return value

**1** if the mask image is successfully set; otherwise, **0**.
## int getMaskImage ( const Ptr < Image > & image ) const

Writes the image that is currently used as a mask for placement of meshes to the given buffer.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image smart pointer.

### Return value

**1** if the mask image is successfully written into the buffer; otherwise, **0**.
## void setMaskImageName ( const char * image_name , bool invalidate = 1 )

Sets the path to a mask image (in *R8* format) that defines the placement of meshes.
### Arguments

- *const char ** **image_name** - Path to the mask image.
- *bool* **invalidate** - Invalidate flag. Set true to invalidate all mesh clutter cells; otherwise, set false. All invalidated cells will be regenerated.

## int setMaskMesh ( const Ptr<ConstMesh> & mesh , bool invalidate = true )

Sets a mesh to be used as a mask on-the-fly. Limitations:
- Before the method is called, another mesh must be set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void) first.
- If the world is reloaded, the mesh set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void) will be loaded.
- If the memory limit is exceeded, the new mesh might be replaced with the mesh set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void).


### Arguments

- *[const Ptr<ConstMesh> &](#ConstMeshPtr)* **mesh** - Pointer to the mesh.
- *bool* **invalidate** - Invalidate flag. Set true to invalidate all mesh clutter cells; otherwise, set false. All invalidated cells will be regenerated.

### Return value

**1** if the mesh is set successfully; otherwise - **0**.
## int getMaskMesh ( const Ptr < Mesh > & mesh ) const

Copies the current mask mesh (if it exists) to the specified target mesh.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - Pointer to the mesh to copy the current mask mesh to.

### Return value

**1** if mesh mask exists; otherwise - **0**.
## void setMaskMeshName ( const char * mesh_name , bool invalidate = 1 )

Sets a mesh to be used as a mask for the mesh clutter. This mesh should be plane.
### Arguments

- *const char ** **mesh_name** - Path to the **.mesh* file.
- *bool* **invalidate** - Invalidate flag. Set true to invalidate all mesh clutter cells; otherwise, set false. All invalidated cells will be regenerated.

## void createClutterTransforms ( )

Creates transformations for all clutter meshes.
## void setMaxScale ( float mean , float spread )

Sets the scale for meshes in the areas with high density (according to the mask). With the minimum scale it is possible to automatically render, for example, big trees in the center of the forest. A spread value allows you to control the range of scales relative to the mean value.
### Arguments

- *float* **mean** - Scale mean value.
- *float* **spread** - Maximum spread value to randomly upscale or downscale objects.

## float getMaxScaleMean ( ) const

Returns the scale mean value for meshes in the areas with high density (according to the mask).
### Return value

Scale mean value.
## float getMaxScaleSpread ( ) const

Returns the scale spread value that controls the range of mesh scales in the areas with high density (according to the mask).
### Return value

Scale spread value.
## void setMeshesRotation ( const Math:: vec3 & mean , const Math:: vec3 & spread )

Sets the parameters of pseudo-random rotation of meshes along X, Y and Z axes.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **mean** - Mean values of meshes rotation angles, in degrees.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **spread** - Maximum spread values of meshes rotation angles, in degrees.

## Math:: vec3 getMeshesRotationMean ( ) const

Returns the vector of mean values of meshes rotation along X, Y and Z axes.
### Return value

Mean values of meshes rotation angles, in degrees.
## Math:: vec3 getMeshesRotationSpread ( ) const

Returns the vector of spread values of meshes rotation along X, Y and Z axes.
### Return value

Maximum spread values of meshes rotation angles, in degrees.
## void setMinScale ( float mean , float spread )

Sets the scale for meshes in the areas with low density (according to the mask). With the minimum scale it is possible to automatically render, for example, small trees at the forest border. A spread value allows you to control the range of scales relative to the mean value.
### Arguments

- *float* **mean** - Scale mean value.
- *float* **spread** - Maximum spread value to randomly upscale or downscale objects.

## float getMinScaleMean ( ) const

Returns the scale mean value for meshes in the areas with low density (according to the mask).
### Return value

Scale mean value.
## float getMinScaleSpread ( ) const

Returns the scale spread value that controls the range of mesh scales in the areas with low density (according to the mask).
### Return value

Scale spread value.
## void setOffset ( float mean , float spread )

Sets the vertical offset that determines the placement of meshes above or below the surface.
### Arguments

- *float* **mean** - Mean value of the offset in units.
- *float* **spread** - Spread value of the offset in units.

## float getOffsetMean ( ) const

Returns the current mean value of the vertical offset that determines the placement of meshes above or below the surface.
### Return value

Mean value of the offset in units.
## float getOffsetSpread ( ) const

Returns the current spread value of the vertical offset that determines the placement of meshes above or below the surface.
### Return value

Spread value of the offset in units.
## void invalidate ( )

Invalidates all mesh clutter cells. All invalidated cells will be regenerated.
## void invalidate ( const Math:: WorldBoundBox & bounds )

Invalidates all mesh clutter cells within the area specified by the given bounding box. All invalidated cells will be regenerated.
### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bounds** - Bounding box, defining the area, where mesh clutter cells will be regenerated.

## static int type ( )

Returns the node type.
### Return value

[Node](../../../api/library/nodes/class.node_cpp.md) type identifier.
## void clearClutterExcludes ( )

Restores all cells removed by the calls to the [setClutterExclude()](#setClutterExclude_WorldBoundBox_int_void) method. Restored cells will be regenerated.
## void setClutterExclude ( const Math:: WorldBoundBox & bounds , int exclude )

Removes all cells within the area specified by the given bounding box. Generation of these cells will be skipped. This method can be used to replace some parts of the clutter with modified meshes (e.g., broken trees within the area around the shell crater in the forest).
### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bounds** - Bounding box, defining the area, where mesh clutter cells will not be generated.
- *int* **exclude** - Exclude flag. Set **1** to remove all mesh clutter cells within the area; otherwise, set **0** to restore the removed ones. Restored cells will be regenerated.

## bool getClutterTransforms ( const Math:: WorldBoundBox & bounds , Vector < Math:: mat4 > & OUT_transforms , bool precise = 1 , bool force = 1 ) const

Collects transformations for all clutter meshes in the generated cells within the area specified by the given bounding box and puts them to the specified buffer.
> **Notice:** Generation of clutter cells is performed in separate threads. Some of the cells may have their lifetime expired. Therefore, the content of certain cells might be unavailable at the moment, such cells are considered as not generated.


### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bounds** - Bounding box, defining the area, for which the transformations of clutter meshes are to be collected.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[mat4](../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Buffer to store transformations of clutter meshes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *bool* **precise** - Precision flag:

  - **1** - transformations will be collected for clutter meshes within the specified bounding box
  - **0** - transformations will be collected for clutter meshes within the cells intersected by the specified bounding box
- *bool* **force** - Force flag.

  - **1** - regenerate all cells within the area, that were not generated, before collecting transformations for the meshes inside them.
  - **0** - transformations will be collected only for the meshes inside the clutter cells, that were generated.

### Return value

true, if there are transformations of clutter meshes; or false, if there are no transformations of clutter meshes found.
## bool getClutterTransforms ( Vector < Math:: mat4 > & OUT_transforms ) const

Collects transformations for all clutter meshes within the generated cells and puts them to the specified buffer.
> **Notice:** Generation of clutter cells is performed in separate threads. Some of the cells may have their lifetime expired. Therefore, the content of certain cells might be unavailable at the moment, such cells are considered as not generated.


### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[mat4](../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Buffer to store transformations of clutter meshes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true, if there are transformations of clutter meshes; or false, if there are no transformations of clutter meshes found.
## bool getClutterWorldTransforms ( const Math:: WorldBoundBox & bounds , Vector < Math:: Mat4 > & OUT_transforms , bool precise = 1 , bool force = 1 ) const

Collects transformations (in world coordinates) for all clutter meshes in the generated cells within the area specified by the given bounding box and puts them to the specified buffer.
> **Notice:** Generation of clutter cells is performed in separate threads. Some of the cells may have their lifetime expired. Therefore, the content of certain cells might be unavailable at the moment, such cells are considered as not generated.


### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bounds** - Bounding box, defining the area, for which the transformations of clutter meshes are to be collected.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Buffer to store transformations of clutter meshes, in world coordinates. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *bool* **precise** - Precision flag:

  - **1** - transformations will be collected for clutter meshes within the specified bounding box
  - **0** - transformations will be collected for clutter meshes within the cells intersected by the specified bounding box
- *bool* **force** - Force flag.

  - **1** - regenerate all cells within the area, that were not generated, before collecting transformations for the meshes inside them.
  - **0** - transformations will be collected only for the meshes inside the clutter cells, that were generated.

### Return value

true, if there are transformations of clutter meshes; or false, if there are no transformations of clutter meshes found.
## bool getClutterWorldTransforms ( Vector < Math:: Mat4 > & OUT_transforms ) const

Collects transformations (in world coordinates) for all clutter meshes within the generated cells and puts them to the specified buffer.
> **Notice:** Generation of clutter cells is performed in separate threads. Some of the cells may have their lifetime expired. Therefore, the content of certain cells might be unavailable at the moment, such cells are considered as not generated.


### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Buffer to store transformations of clutter meshes, in world coordinates. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true, if there are transformations of clutter meshes; or false, if there are no transformations of clutter meshes found.
## int getClutterLocalTransforms ( const Math:: BoundBox & bounds , Vector < Math:: mat4 > & OUT_transforms , int precise = 1 , int force = 1 ) const

Collects transformations (in local coordinates) for all clutter meshes within the generated cells and puts them to the specified buffer.
> **Notice:** Generation of clutter cells is performed in separate threads. Some of the cells may have their lifetime expired. Therefore, the content of certain cells might be unavailable at the moment, such cells are considered as not generated.


### Arguments

- *const  Math::[BoundBox](../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bounds** - Bounding box, defining the area, for which the transformations of clutter meshes are to be collected.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[mat4](../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Buffer to store transformations of clutter meshes, in local coordinates. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **precise** - Precision flag:

  - **1** - transformations will be collected for clutter meshes within the specified bounding box
  - **0** - transformations will be collected for clutter meshes within the cells intersected by the specified bounding box
- *int* **force** - Force flag.

  - **1** - regenerate all cells within the area, that were not generated, before collecting transformations for the meshes inside them.
  - **0** - transformations will be collected only for the meshes inside the clutter cells, that were generated.

### Return value

true, if there are transformations of clutter meshes; or false, if there are no transformations of clutter meshes found.
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

Performs force-loading of the mesh to video memory (VRAM) immediately.
> **Notice:** Loading to VRAM must be performed in the main thread only.


### Return value

true if the mesh is loaded successfully, otherwise false. If the mesh is already loaded to VRAM, true will be returned.
## bool loadForceRAM ( )

Performs force-loading of the mesh to memory (RAM) immediately.
### Return value

true if the mesh is loaded successfully, otherwise false. If the mesh is already loaded to RAM, true will be returned.
## void setMeshProceduralMode ( ObjectMeshStatic::PROCEDURAL_MODE mode , int mesh_render_flags = 0 )

Sets the procedural mode for the mesh. The specified mode defines how procedural data is stored, updated, and unloaded.
> **Notice:** Please note that procedural mesh modification **directly affects streaming and memory usage (RAM, VRAM, and disk)** depending on the selected procedural mode. For details, see the [Procedural Mesh Workflow](#procedural_workflow) section.

### Arguments

- *[ObjectMeshStatic::PROCEDURAL_MODE](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE)* **mode** - One of the *[PROCEDURAL_MODE](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE)* to apply to the mesh.
- *int* **mesh_render_flags** - Optional [usage flags](../../../api/library/rendering/class.meshrender_cpp.md#USAGE_DYNAMIC_VERTEX) that control how vertex and index data are stored for the mesh render.

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
## void setIntersectionMask ( int mask )

 Sets a new intersection mask for the world clutter. This mask can be used to cut out areas intersected by the world clutter from [grass](../../../api/library/objects/class.objectgrass_cpp.md#setCutoutIntersectionMask_int_void), [mesh clutter](../../../api/library/objects/class.objectmeshclutter_cpp.md#setCutoutIntersectionMask_int_void) and another [world clutter](#setCutoutIntersectionMask_int_void) (e.g. to remove grass or forest from the surface of roads projected using decals).
> **Notice:** The areas will be cut out only if intersection masks of grass and clutter objects matches this mask (one bit at least).


### Arguments

- *int* **mask** - The intersection mask - an integer, each bit of which is a mask.

## int getIntersectionMask ( ) const

 Returns the current intersection mask for the world clutter. This mask can be used to cut out areas intersected by the world clutter from [grass](../../../api/library/objects/class.objectgrass_cpp.md#setCutoutIntersectionMask_int_void), [mesh clutter](../../../api/library/objects/class.objectmeshclutter_cpp.md#setCutoutIntersectionMask_int_void) and another [world clutter](#setCutoutIntersectionMask_int_void) (e.g. to remove grass or forest from the surface of roads projected using decals).
> **Notice:** The areas will be cut out only if intersection masks of grass and clutter objects matches this mask (one bit at least).


### Return value

Current intersection mask - an integer, each bit of which is a mask.
