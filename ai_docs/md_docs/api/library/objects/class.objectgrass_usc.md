# ObjectGrass Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


This class is used to create [grass](../../../objects/objects/grass/index.md). The grass object is rendered in grid [cells](../../../objects/objects/grass/index.md#step).


You can use [a mask](#setCutoutIntersectionMask_int_void) to cut out grass in the areas of intersection with other objects and decals (e.g. to remove vegetation under houses or from the surface of roads projected using decals).


## ObjectGrass Class

### Members

## void setCutoutInverse ( int inverse )

Sets a new value indicating if the grass is rendered inside or outside the areas determined by the [cutout intersection mask](#setCutoutIntersectionMask_int_void).
### Arguments

- *int* **inverse** - The value indicating if the grass is rendered inside or outside the areas determined by the cutout intersection mask

## int getCutoutInverse () const

Returns the current value indicating if the grass is rendered inside or outside the areas determined by the [cutout intersection mask](#setCutoutIntersectionMask_int_void).
### Return value

Current value indicating if the grass is rendered inside or outside the areas determined by the cutout intersection mask
## void setCutoutIntersectionMask ( int mask )

Sets a new cutout intersection mask. this mask allows you to cut out the grass in the areas of intersection with objects and decals (e.g. can be used to remove grass under houses or from the surface of roads projected using decals). the grass will be cut out by objects and decals that have their intersection mask matching this one (one bit at least).
> **Notice:** To set intersection masks the following methods can be used:
> - **for decals** use *[getIntersectionMask()](../../../api/library/decals/class.decal_usc.md#getIntersectionMask_int)*
> - **for objects** use *[getIntersectionMask()](../../../api/library/objects/class.object_usc.md#getIntersectionMask_int_int)*

### Arguments

- *int* **mask** - The cutout intersection mask

## int getCutoutIntersectionMask () const

Returns the current cutout intersection mask. this mask allows you to cut out the grass in the areas of intersection with objects and decals (e.g. can be used to remove grass under houses or from the surface of roads projected using decals). the grass will be cut out by objects and decals that have their intersection mask matching this one (one bit at least).
> **Notice:** To set intersection masks the following methods can be used:
> - **for decals** use *[getIntersectionMask()](../../../api/library/decals/class.decal_usc.md#getIntersectionMask_int)*
> - **for objects** use *[getIntersectionMask()](../../../api/library/objects/class.object_usc.md#getIntersectionMask_int_int)*

### Return value

Current cutout intersection mask
## void setMaskInverse ( int inverse )

Sets a new flag indicating if the grass is rendered inside or outside the mask mesh contour.
### Arguments

- *int* **inverse** - The flag indicating if the grass is rendered inside or outside the mask mesh contour

## int getMaskInverse () const

Returns the current flag indicating if the grass is rendered inside or outside the mask mesh contour.
### Return value

Current flag indicating if the grass is rendered inside or outside the mask mesh contour
## void setMaskMaxValue ( int value )

Sets a new maximum value of the mask application range (a color range from **0** to **255**, indicating that only that part of mask, which contains this color range, will be applied to the image).
### Arguments

- *int* **value** - The maximum value of the mask application range

## int getMaskMaxValue () const

Returns the current maximum value of the mask application range (a color range from **0** to **255**, indicating that only that part of mask, which contains this color range, will be applied to the image).
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
## void setProbability ( vec4 probability )

Sets a new grass rendering probability per column (in the diffuse texture). the higher the value for some column, the more frequently it will be rendered. Any values can be set, since they are normalized.
### Arguments

- *vec4* **probability** - The grass rendering probability per column (in the diffuse texture)

## vec4 getProbability () const

Returns the current grass rendering probability per column (in the diffuse texture). the higher the value for some column, the more frequently it will be rendered. Any values can be set, since they are normalized.
### Return value

Current grass rendering probability per column (in the diffuse texture)
## void setAngle ( float angle )

Sets a new angle cosine defining the slope steepness appropriate for grass growing, in range from **0** to **1**.
### Arguments

- *float* **angle** - The angle cosine defining the slope steepness appropriate for grass growing

## float getAngle () const

Returns the current angle cosine defining the slope steepness appropriate for grass growing, in range from **0** to **1**.
### Return value

Current angle cosine defining the slope steepness appropriate for grass growing
## void setThreshold ( float threshold )

Sets a new threshold for density, starting from which the grass is rendered.
### Arguments

- *float* **threshold** - The threshold for density, starting from which the grass is rendered

## float getThreshold () const

Returns the current threshold for density, starting from which the grass is rendered.
### Return value

Current threshold for density, starting from which the grass is rendered
## void setDensity ( float density )

Sets a new density factor for the grass per square unit.
### Arguments

- *float* **density** - The density factor for the grass per square unit

## float getDensity () const

Returns the current density factor for the grass per square unit.
### Return value

Current density factor for the grass per square unit
## void setSubdivision ( int subdivision )

Sets a new divisor used to subdivide grass rendering cells into smaller sub-cells. The value is clamped to a range **[1;32]**. subdividing is used if a grass node is used as a distant lod for [WorldClutter](../../../api/library/worlds/class.worldclutter_usc.md) or [ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_usc.md) with smaller cells. This way, positions of randomly scattered objects will coincide with those of grass-based impostors.
### Arguments

- *int* **subdivision** - The divisor used to subdivide grass rendering cells into smaller sub-cells

## int getSubdivision () const

Returns the current divisor used to subdivide grass rendering cells into smaller sub-cells. The value is clamped to a range **[1;32]**. subdividing is used if a grass node is used as a distant lod for [WorldClutter](../../../api/library/worlds/class.worldclutter_usc.md) or [ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_usc.md) with smaller cells. This way, positions of randomly scattered objects will coincide with those of grass-based impostors.
### Return value

Current divisor used to subdivide grass rendering cells into smaller sub-cells
## void setStep ( float step )

Sets a new step for cells used to render grass.
### Arguments

- *float* **step** - The step for cells used to render grass

## float getStep () const

Returns the current step for cells used to render grass.
### Return value

Current step for cells used to render grass
## void setSizeY ( float y )

Sets a new length of the grass object along the y-coordinate, in units. If a negative value is provided, **0** will be used instead.
### Arguments

- *float* **y** - The length of the grass object along the y-coordinate

## float getSizeY () const

Returns the current length of the grass object along the y-coordinate, in units. If a negative value is provided, **0** will be used instead.
### Return value

Current length of the grass object along the y-coordinate
## void setSizeX ( float x )

Sets a new width of the grass object along the x-coordinate, in units. If a negative value is provided, **0** will be used instead.
### Arguments

- *float* **x** - The width of the grass object along the x-coordinate

## float getSizeX () const

Returns the current width of the grass object along the x-coordinate, in units. If a negative value is provided, **0** will be used instead.
### Return value

Current width of the grass object along the x-coordinate
## void setSeed ( int seed )

Sets a new seed used for pseudo-random positioning of grass. If a negative value is provided, **0** will be used instead.
### Arguments

- *int* **seed** - The seed used for pseudo-random positioning of grass

## int getSeed () const

Returns the current seed used for pseudo-random positioning of grass. If a negative value is provided, **0** will be used instead.
### Return value

Current seed used for pseudo-random positioning of grass
## void setNumTextures ( int textures )

Sets a new number of rows contained in the [grass diffuse texture](../../../content/materials/library/grass_base/index.md#texture_diffuse), in the **[1; 4]** range.
### Arguments

- *int* **textures** - The number of rows contained in the grass diffuse texture

## int getNumTextures () const

Returns the current number of rows contained in the [grass diffuse texture](../../../content/materials/library/grass_base/index.md#texture_diffuse), in the **[1; 4]** range.
### Return value

Current number of rows contained in the grass diffuse texture
## void setIntersection ( int intersection )

Sets a new value indicating whether grass grow upon the ground: either the terrain or a mesh set as a parent node.
### Arguments

- *int* **intersection** - The value indicating whether grass grow upon the ground: either the terrain or a mesh set as a parent node

## int getIntersection () const

Returns the current value indicating whether grass grow upon the ground: either the terrain or a mesh set as a parent node.
### Return value

Current value indicating whether grass grow upon the ground: either the terrain or a mesh set as a parent node
## void setIntersectionMask ( int mask )

Sets a new intersection mask for the object.
### Arguments

- *int* **mask** - The intersection mask for the object

## int getIntersectionMask () const

Returns the current intersection mask for the object.
### Return value

Current intersection mask for the object
## void setOrientation ( int orientation )

Sets a new flag indicating if grass polygons are oriented along the normal of its parent (for example, a terrain).
### Arguments

- *int* **orientation** - The flag indicating if grass polygons are oriented along the normal of its parent (for example, a terrain)

## int getOrientation () const

Returns the current flag indicating if grass polygons are oriented along the normal of its parent (for example, a terrain).
### Return value

Current flag indicating if grass polygons are oriented along the normal of its parent (for example, a terrain)
## void setVariation ( int variation )

Sets a new value indicating if the random horizontal flip for grass polygons is set.
### Arguments

- *int* **variation** - The value indicating if the random horizontal flip for grass polygons is set

## int getVariation () const

Returns the current value indicating if the random horizontal flip for grass polygons is set.
### Return value

Current value indicating if the random horizontal flip for grass polygons is set
## void setThinning ( int thinning )

Sets a new flag indicating if the grass is thinned out with a distance (random grass polygons are not rendered across the grass fade distance).
### Arguments

- *int* **thinning** - The flag indicating if the grass is thinned out with a distance

## int getThinning () const

Returns the current flag indicating if the grass is thinned out with a distance (random grass polygons are not rendered across the grass fade distance).
### Return value

Current flag indicating if the grass is thinned out with a distance
## void setFieldMask ( int mask )

Sets a new mask specifying the area of the field node to be applied to the grass. The integer is treated as a bit mask, where each bit is a separate mask.
### Arguments

- *int* **mask** - The mask specifying the area of the field node to be applied to the grass

## int getFieldMask () const

Returns the current mask specifying the area of the field node to be applied to the grass. The integer is treated as a bit mask, where each bit is a separate mask.
### Return value

Current mask specifying the area of the field node to be applied to the grass
## void setTerrainMasks ( ivec4 masks )

Sets a new set of [Landscape Terrain masks](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_usc.md#getDetailMask_int_TerrainDetailMask) used for grass placement (a four-component vector combining mask indices, each component in the [0; 19] range, to be used for the corresponding diffuse texture column).
### Arguments

- *ivec4* **masks** - The set of Landscape Terrain masks used for grass placement

## ivec4 getTerrainMasks () const

Returns the current set of [Landscape Terrain masks](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_usc.md#getDetailMask_int_TerrainDetailMask) used for grass placement (a four-component vector combining mask indices, each component in the [0; 19] range, to be used for the corresponding diffuse texture column).
### Return value

Current set of Landscape Terrain masks used for grass placement
---

## static ObjectGrass ( )

Constructor. Creates a new grass object.
## void setAspect ( vec4 mean , vec4 spread )

Sets the aspect of the grass polygons (width to height ratio).
### Arguments

- *vec4* **mean** - Mean value of grass aspect.
- *vec4* **spread** - Spread value of grass aspect.

## vec4 getAspectMean ( )

Returns the current mean value of the grass aspect (width to height ratio), defined for four diffuse texture columns.
### Return value

Mean value of grass aspect.
## vec4 getAspectSpread ( )

Returns the current spread value of the grass aspect (width to height ratio), defined for four diffuse texture columns.
### Return value

Spread value of grass aspect.
## int setMaskImage ( Image image , int invalidate = 1 )

Sets an image that defines the areas of growing grass. Possible mask formats are *R8*, *RG8*, *RGB8* and *RGBA8*.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Pointer to the image.
- *int* **invalidate** - Invalidate flag. Set **1** to invalidate all grass cells; otherwise, set **0**. All invalidated cells will be regenerated.

### Return value

**1** if the mask image is successfully set; otherwise, **0**.
## int getMaskImage ( Image image )

Writes the image that is currently used to define the areas of grass growing into the given buffer. Possible mask formats are *R8*, *RG8*, *RGB8* and *RGBA8*.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image buffer to store a mask into.

### Return value

**1** if the mask image is successfully written into the buffer; otherwise, **0**.
## void setMaskImageName ( string image_name , int invalidate = 1 )

Sets the name of a mask image that defines the areas of growing grass. Possible mask formats are *R8*, *RG8*, *RGB8* and *RGBA8*.
### Arguments

- *string* **image_name** - Name (path) of the mask image.
- *int* **invalidate** - Invalidate flag. Set **1** to invalidate all grass cells; otherwise, set **0**. All invalidated cells will be regenerated.

## string getMaskImageName ( )

Returns a name of the current mask image that defines the areas of grass growing. Possible mask formats are *R8*, *RG8*, *RGB8* and *RGBA8*.
### Return value

Name (path) of the mask image.
## int setMaskMesh ( Mesh mesh , int invalidate = 1 )

Sets a mesh to be used as a mask on-the-fly. Limitations:
- Before the method is called, another mesh must be set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void) first.
- If the world is reloaded, the mesh set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void) will be loaded.
- If the memory limit is exceeded, the new mesh might be replaced with the mesh set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void).


### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **mesh** - Mesh instance.
- *int* **invalidate** - Invalidate flag. Set **1** to invalidate all grass cells; otherwise, set **0**. All invalidated cells will be regenerated.

### Return value

**1** if the mesh is set successfully; otherwise - **0**.
## int getMaskMesh ( Mesh mesh )

Copies the current mask mesh (if it exists) to the specified target mesh.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **mesh** - Mesh instance to copy the current mask mesh to.

### Return value

**1** if mesh mask exists; otherwise - **0**.
## void setMaskMeshName ( string mesh_name , int invalidate = 1 )

Sets a mesh to be used as a mask for the grass. This mesh should be plane.
### Arguments

- *string* **mesh_name** - Path to the **.mesh* file.
- *int* **invalidate** - Invalidate flag. Set **1** to invalidate all grass cells; otherwise, set **0**. All invalidated cells will be regenerated.

## string getMaskMeshName ( )

Returns the name (path) of the current mesh used as a mask for the grass. This mesh should be plane.
### Return value

Path to the **.mesh* file.
## void setMaxBend ( vec4 mean , vec4 spread )

Sets the maximum grass bending parameters (rendered in areas with the highest density according to the mask). Bend angles (mean and spread) are defined for four diffuse texture columns. The resulting value is determined as follows: `Result = Mean + Random * Spread`, where `Random` is a random value in range from -1 to 1.
### Arguments

- *vec4* **mean** - Vector of mean values of grass bending angles to be set for four diffuse texture columns.
- *vec4* **spread** - Vector of spread values of grass bending angles to be set for four diffuse texture columns.

## vec4 getMaxBendMean ( )

Returns the mean value for the maximum grass bending (rendered in areas with the highest density according to the mask). Bend angles are defined for four diffuse texture columns.
### Return value

Vector of mean values of grass bending angles for four diffuse texture columns.
## vec4 getMaxBendSpread ( )

Returns the spread value for the maximum grass bending (rendered in areas with the highest density according to the mask). Bend angles are defined for four diffuse texture columns.
### Return value

Vector of spread values of grass bending angles for four diffuse texture columns.
## void setMinBend ( vec4 mean , vec4 spread )

Sets the minimum grass bending parameters (rendered in areas with the lowest density according to the mask). Bend angles (mean and spread) are defined for four diffuse texture columns. The resulting value is determined as follows: `Result = Mean + Random * Spread`, where `Random` is a random value in range from -1 to 1.
### Arguments

- *vec4* **mean** - Vector of mean values of grass bending angles to be set for four diffuse texture columns.
- *vec4* **spread** - Vector of spread values of grass bending angles to be set for four diffuse texture columns.

## vec4 getMinBendMean ( )

Returns the mean value for the minimum grass bending (rendered in areas with the lowest density according to the mask). Bend angles are defined for four diffuse texture columns.
### Return value

Vector of mean values of grass bending angles for four diffuse texture columns.
## vec4 getMinBendSpread ( )

Returns the spread value for the minimum grass bending (rendered in areas with the lowest density according to the mask). Bend angles are defined for four diffuse texture columns.
### Return value

Vector of spread values of grass bending angles for four diffuse texture columns.
## void setMaxHeight ( vec4 mean , vec4 spread )

Sets the maximum grass height (rendered in areas with the highest density according to the mask). The height is defined for four diffuse texture columns, as mean and spread values ( `Result = Mean + Random * Spread`, where `Random` is a random value in range from -1 to 1).
### Arguments

- *vec4* **mean** - Mean value for the maximum grass height in units. If a negative value is provided, EPSILON will be used instead.
- *vec4* **spread** - Spread value for the maximum grass height in units.

## vec4 getMaxHeightMean ( )

Returns the mean value for the maximum grass height (rendered in areas with the highest density according to the mask). The height is defined for four diffuse texture columns.
### Return value

Mean value for the maximum grass height in units.
## vec4 getMaxHeightSpread ( )

Returns the spread value for the maximum grass height (rendered in areas with the highest density according to the mask). The height is defined for four diffuse texture columns.
### Return value

Spread value for the maximum grass height in units.
## void setMinHeight ( vec4 mean , vec4 spread )

Sets the minimum grass height (rendered in areas with the lowest density according to the mask). The height is defined for four diffuse texture columns, as mean and spread values ( `Result = Mean + Random * Spread`, where `Random` is a random value in range from -1 to 1).
### Arguments

- *vec4* **mean** - Mean value for the minimum grass height in units. If a negative value is provided, EPSILON will be used instead.
- *vec4* **spread** - Spread value for the minimum grass height in units.

## vec4 getMinHeightMean ( )

Returns the mean value for the minimum grass height (rendered in areas with the lowest density according to the mask). The height is defined for four diffuse texture columns.
### Return value

Mean value for the minimum grass height in units.
## vec4 getMinHeightSpread ( )

Returns the spread value for the minimum grass height (rendered in areas with the lowest density according to the mask). The height is defined for four diffuse texture columns.
### Return value

Spread value for the minimum grass height in units.
## void setOffset ( vec4 mean , vec4 spread )

Sets the grass offset from the surface along the surface normal, defined for four diffuse texture columns. If a negative mean value is provided, **vec4_eps** will be used instead.
### Arguments

- *vec4* **mean** - Mean value of grass polygons offset in units.
- *vec4* **spread** - Spread value of grass polygons offset in units.

## vec4 getOffsetMean ( )

Returns the current mean value of the grass offset from the surface along the surface normal, defined for four diffuse texture columns.
### Return value

Mean value of grass polygons offset in units.
## vec4 getOffsetSpread ( )

Returns the current spread value for the grass offset from the surface along the surface normal, defined for four diffuse texture columns.
### Return value

Spread value for grass polygons offset in units.
## void setRotation ( vec4 mean , vec4 spread )

Sets the grass rotation. Rotation is defined for four diffuse texture columns, as mean and spread values ( `Result = Mean + Random * Spread`, where `Random` is a random value in range from -1 to 1).
### Arguments

- *vec4* **mean** - Mean value of grass polygons rotation, in degrees.
- *vec4* **spread** - Spread value of grass polygons rotation, in degrees.

## vec4 getRotationMean ( )

Returns the current mean value for the grass rotation, defined for four diffuse texture columns.
### Return value

Mean value of grass polygons rotation, in degrees.
## vec4 getRotationSpread ( )

Returns the current spread value for the grass rotation, defined for four diffuse texture columns.
### Return value

Spread value of grass polygons rotation, in degrees.
## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_usc.md) type identifier.
## void invalidate ( )

Invalidates all grass cells. All invalidated cells will be regenerated.
## void invalidate ( WorldBoundBox bounds )

Invalidates all grass cells within the area specified by the given bounding box. All invalidated cells will be regenerated.
### Arguments

- *WorldBoundBox* **bounds** - Bounding box, defining the area, where grass cells will be regenerated.
