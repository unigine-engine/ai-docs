# ObjectGrass Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


This class is used to create [grass](../../../objects/objects/grass/index.md). The grass object is rendered in grid [cells](../../../objects/objects/grass/index.md#step).


You can use [a mask](#setCutoutIntersectionMask_int_void) to cut out grass in the areas of intersection with other objects and decals (e.g. to remove vegetation under houses or from the surface of roads projected using decals).


## ObjectGrass Class

### Members

---

## static ObjectGrass ( )

Constructor. Creates a new grass object.
## void setAngle ( float angle )

Sets the angle cosine defining the slope steepness appropriate for grass growing.
### Arguments

- *float* **angle** - Slope angle cosine in range from **0** to **1**.

## float getAngle ( )

Returns the current angle cosine defining the slope steepness appropriate for grass growing.
### Return value

Slope angle cosine.
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
## void setDensity ( float density )

Sets the density factor for the grass per square unit.
### Arguments

- *float* **density** - Density factor. If a negative value is provided, **0** will be used instead.

## float getDensity ( )

Returns the current density factor for the grass per square unit.
### Return value

Density factor.
## void setFieldMask ( int mask )

Sets a mask specifying the area of the Field node to be applied to the grass.
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getFieldMask ( )

Returns a mask specifying the area of the Field node to be applied to the grass.
### Return value

Integer, each bit of which is a mask.
## void setIntersection ( int intersection )

Sets a value indicating whether grass should grow upon the ground: either the terrain or a mesh set as a parent node.
### Arguments

- *int* **intersection** - Positive number to enable intersection; **0** to disable.

## int getIntersection ( )

Returns a value indicating whether grass grow upon the ground: either the terrain or a mesh set as a parent node.
### Return value

Positive number if intersection is enabled; otherwise, **0**.
## void setMaskFlipX ( int maskflipx )

Flip the mask by X axis.
### Arguments

- *int* **maskflipx** - Positive value to flip the mask; otherwise, **0**.

## int getMaskFlipX ( )

Returns a flag indicating if a mask is flipped by X axis.
### Return value

Positive value if the mask is flipped; otherwise, **0**.
## void setMaskFlipY ( int maskflipy )

Flip the mask by Y axis.
### Arguments

- *int* **maskflipy** - Positive value to flip the mask; otherwise, **0**.

## int getMaskFlipY ( )

Returns a flag indicating if a mask is flipped by Y axis.
### Return value

Positive value if the mask is flipped; otherwise, **0**.
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
## void setMaskInverse ( int inverse )

Specifies if the grass should be rendered inside or outside the mask mesh contour.
### Arguments

- *int* **inverse** - **0** to render the grass inside the mesh contour; **1** to render it outside.

## int getMaskInverse ( )

Returns a flag indicating if the grass is rendered inside or outside the mask mesh contour.
### Return value

**0** if the grass is rendered inside the mesh contour; **1** if outside.
## void setMaskMaxValue ( int value )

Sets the maximum value of the mask application range.
### Arguments

- *int* **value** - Maximum mask value, **[0;255]**.

## int getMaskMaxValue ( )

Returns the maximum value of the mask application range.
### Return value

Maximum mask value.
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
## void setMaskMinValue ( int value )

Sets the minimum value of the mask application range.
### Arguments

- *int* **value** - Minimum mask value, **[0;255]**.

## int getMaskMinValue ( )

Returns the minimum value of the mask application range.
### Return value

Minimum mask value.
## void setTerrainMasks ( ivec4 masks )

Sets a new set of [Landscape Terrain masks](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_usc.md#getDetailMask_int_TerrainDetailMask) to be used for grass placement.
### Arguments

- *ivec4* **masks** - Four-component vector combining Landscape Terrain mask indices (each component in the [0; 19] range) to be used for the corresponding diffuse texture column.

## ivec4 getTerrainMasks ( )

Returns the current set of [Landscape Terrain masks](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_usc.md#getDetailMask_int_TerrainDetailMask) used for grass placement.
### Return value

Four-component vector combining Landscape Terrain mask indices (each component in the [0; 19] range) to be used for the corresponding diffuse texture column.
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
## void setNumTextures ( int textures )

Sets the number of rows contained in the [grass diffuse texture](../../../content/materials/library/grass_base/index.md#texture_diffuse).
### Arguments

- *int* **textures** - Number of rows in the grass diffuse texture in the [**1; 4**] range.

## int getNumTextures ( )

Returns the number of rows contained in the [grass diffuse texture](../../../content/materials/library/grass_base/index.md#texture_diffuse).
### Return value

The number of rows in the grass diffuse texture in the [**1; 4**] range.
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
## void setOrientation ( int orientation )

Sets a flag to orient grass polygons along the normal of its parent (for example, a terrain).
### Arguments

- *int* **orientation** - **1** to orient the grass along the normals of the ground; **0** to render it always pointing upwards.

## int getOrientation ( )

Returns a flag indicating if grass polygons are oriented along the normal of its parent (for example, a terrain).
### Return value

**1** if the grass is oriented along the normals of the ground; **0** if it always points upwards.
## void setProbability ( vec4 probability )

Sets the grass rendering probability per column (in the diffuse texture). The higher the value for some column, the more frequently it will be rendered.
### Arguments

- *vec4* **probability** - Per-column probability. Any values can be set, since they are normalized.

## vec4 getProbability ( )

Returns the current grass rendering probability per column (in the diffuse texture). The higher the value for some column, the more frequently it will be rendered.
### Return value

Per-column probability.
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
## void setSeed ( int seed )

Sets the seed for pseudo-random positioning of grass.
### Arguments

- *int* **seed** - Number used to initialize a pseudo-random sequence. If a negative value is provided, **0** will be used instead.

## int getSeed ( )

Returns the seed used for pseudo-random positioning of grass.
### Return value

Number used to initialize a pseudo-random sequence.
## void setSizeX ( float sizex )

Sets the width of the grass object along the X-coordinate.
### Arguments

- *float* **sizex** - X-coordinate width in units. If a negative value is provided, **0** will be used instead.

## float getSizeX ( )

Returns the current width of the grass object along the X-coordinate.
### Return value

X-coordinate width in units.
## void setSizeY ( float sizey )

Sets the length of the grass object along the Y-coordinate.
### Arguments

- *float* **sizey** - Y-coordinate length in units. If a negative value is provided, **0** will be used instead.

## float getSizeY ( )

Returns the current length of the grass object along the Y-coordinate.
### Return value

Y-coordinate length in units.
## int getSpawnCount ( )

Returns the number of cells to be generated.
### Return value

Number of cells to be generated if the scene generation is not completed; otherwise, 0.
## void setStep ( float step )

Sets the step for cells used to render grass.
### Arguments

- *float* **step** - Step for grass cells.

## float getStep ( )

Returns the current step for cells used to render grass.
### Return value

Step for grass cells.
## void setSubdivision ( int subdivision )

Subdivide grass rendering cells into smaller sub-cells. It is used if a grass node is used as a distant LOD for [WorldClutter](../../../api/library/worlds/class.worldclutter_usc.md) or [ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_usc.md) with smaller cells. This way, positions of randomly scattered objects will coincide with those of grass-based impostors.
### Arguments

- *int* **subdivision** - Divisor for cells. The value is clamped to a range [1;32].

## int getSubdivision ( )

Returns the current divisor used to subdivide grass rendering cells into smaller sub-cells. Subdividing is used if a grass node is used as a distant LOD for [WorldClutter](../../../api/library/worlds/class.worldclutter_usc.md) or [ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_usc.md) with smaller cells. This way, positions of randomly scattered objects will coincide with those of grass-based impostors.
### Return value

Divisor for cells.
## void setThinning ( int thinning )

Sets a flag to thin out grass with a distance (random grass polygons are not rendered across the grass Fade distance).
### Arguments

- *int* **thinning** - **1** to thin out the grass; **0** to render all grass polygons at the distance.

## int getThinning ( )

Returns a flag indicating if the grass is thinned out with a distance (random grass polygons are not rendered across the grass Fade distance).
### Return value

**1** if the grass is thinned out; **0** if all grass polygons are rendered at the distance.
## void setThreshold ( float threshold )

Sets the threshold for density, starting from which the grass will be rendered.
### Arguments

- *float* **threshold** - Threshold value in range from **0** to **1**.

## float getThreshold ( )

Returns the current threshold for density, starting from which the grass is rendered.
### Return value

Threshold value.
## void setVariation ( int variation )

Sets the random horizontal flip for grass polygons.
### Arguments

- *int* **variation** - **1** to enable grass flipping, **0** to disable it.

## int getVariation ( )

Returns a value indicating if the random horizontal flip for grass polygons is set.
### Return value

**1** if grass flipping is enabled; otherwise, **0**.
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

## void setCutoutIntersectionMask ( int mask )

Sets a new cutout intersection mask. This mask allows you to cut out the grass in the areas of intersection with objects and decals (e.g. can be used to remove grass under houses or from the surface of roads projected using decals). The grass will be cut out by objects and decals that have their intersection mask matching this one (one bit at least).
> **Notice:** To set intersection masks the following methods can be used:
> - **for decals** use *[getIntersectionMask()](../../../api/library/decals/class.decal_usc.md#getIntersectionMask_int)*
> - **for objects** use *[getIntersectionMask()](../../../api/library/objects/class.object_usc.md#getIntersectionMask_int_int)*


### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getCutoutIntersectionMask ( )

Returns the current cutout intersection mask. This mask allows you to cut out the grass in the areas of intersection with objects and decals (e.g. can be used to remove grass under houses or from the surface of roads projected using decals). The grass will be cut out by objects and decals that have their intersection mask matching this one (one bit at least).
> **Notice:** To set intersection masks the following methods can be used:
> - **for decals** use *[getIntersectionMask()](../../../api/library/decals/class.decal_usc.md#getIntersectionMask_int)*
> - **for objects** use *[getIntersectionMask()](../../../api/library/objects/class.object_usc.md#getIntersectionMask_int_int)*


### Return value

Integer, each bit of which is a mask.
## void setCutoutInverse ( int inverse )

Sets a value indicating whether the grass should be rendered inside or outside the areas determined by the [cutout intersection mask](#setCutoutIntersectionMask_int_void).
### Arguments

- *int* **inverse** - **0** to render the grass outside the areas determined by the cutout intersection mask; **1** to render the grass inside these areas.

## int getCutoutInverse ( )

Returns a value indicating if the grass is rendered inside or outside the areas determined by the [cutout intersection mask](#setCutoutIntersectionMask_int_void).
### Return value

**0** if the grass is rendered outside the areas determined by the cutout intersection mask; **1** if inside.
