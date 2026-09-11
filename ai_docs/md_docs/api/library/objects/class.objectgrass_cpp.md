# ObjectGrass Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


This class is used to create [grass](../../../objects/objects/grass/index.md). The grass object is rendered in grid [cells](../../../objects/objects/grass/index.md#step).


You can use [a mask](#setCutoutIntersectionMask_int_void) to cut out grass in the areas of intersection with other objects and decals (e.g. to remove vegetation under houses or from the surface of roads projected using decals).


## ObjectGrass Class

### Members

## void setCutoutInverse ( bool inverse )

Sets a new value indicating if the grass is rendered inside or outside the areas determined by the [cutout intersection mask](#setCutoutIntersectionMask_int_void).
### Arguments

- *bool* **inverse** - value indicating if the grass is rendered inside or outside the areas determined by the cutout intersection mask

## bool getCutoutInverse () const

Returns the current value indicating if the grass is rendered inside or outside the areas determined by the [cutout intersection mask](#setCutoutIntersectionMask_int_void).
### Return value

value indicating if the grass is rendered inside or outside the areas determined by the cutout intersection mask
## void setCutoutIntersectionMask ( int mask )

Sets a new cutout intersection mask. this mask allows you to cut out the grass in the areas of intersection with objects and decals (e.g. can be used to remove grass under houses or from the surface of roads projected using decals). the grass will be cut out by objects and decals that have their intersection mask matching this one (one bit at least).
> **Notice:** To set intersection masks the following methods can be used:
> - **for decals** use *[getIntersectionMask()](../../../api/library/decals/class.decal_cpp.md#getIntersectionMask_int)*
> - **for objects** use *[getIntersectionMask()](../../../api/library/objects/class.object_cpp.md#getIntersectionMask_int_int)*

### Arguments

- *int* **mask** - The cutout intersection mask

## int getCutoutIntersectionMask () const

Returns the current cutout intersection mask. this mask allows you to cut out the grass in the areas of intersection with objects and decals (e.g. can be used to remove grass under houses or from the surface of roads projected using decals). the grass will be cut out by objects and decals that have their intersection mask matching this one (one bit at least).
> **Notice:** To set intersection masks the following methods can be used:
> - **for decals** use *[getIntersectionMask()](../../../api/library/decals/class.decal_cpp.md#getIntersectionMask_int)*
> - **for objects** use *[getIntersectionMask()](../../../api/library/objects/class.object_cpp.md#getIntersectionMask_int_int)*

### Return value

Current cutout intersection mask
## void setMaskInverse ( bool inverse )

Sets a new flag indicating if the grass is rendered inside or outside the mask mesh contour.
### Arguments

- *bool* **inverse** - flag indicating if the grass is rendered inside or outside the mask mesh contour

## bool getMaskInverse () const

Returns the current flag indicating if the grass is rendered inside or outside the mask mesh contour.
### Return value

flag indicating if the grass is rendered inside or outside the mask mesh contour
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
## void setProbability ( const Math:: vec4 & probability )

Sets a new grass rendering probability per column (in the diffuse texture). the higher the value for some column, the more frequently it will be rendered. Any values can be set, since they are normalized.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **probability** - The grass rendering probability per column (in the diffuse texture)

## Math:: vec4 getProbability () const

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

Sets a new divisor used to subdivide grass rendering cells into smaller sub-cells. The value is clamped to a range **[1;32]**. subdividing is used if a grass node is used as a distant lod for [WorldClutter](../../../api/library/worlds/class.worldclutter_cpp.md) or [ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_cpp.md) with smaller cells. This way, positions of randomly scattered objects will coincide with those of grass-based impostors.
### Arguments

- *int* **subdivision** - The divisor used to subdivide grass rendering cells into smaller sub-cells

## int getSubdivision () const

Returns the current divisor used to subdivide grass rendering cells into smaller sub-cells. The value is clamped to a range **[1;32]**. subdividing is used if a grass node is used as a distant lod for [WorldClutter](../../../api/library/worlds/class.worldclutter_cpp.md) or [ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_cpp.md) with smaller cells. This way, positions of randomly scattered objects will coincide with those of grass-based impostors.
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
## void setIntersection ( bool intersection )

Sets a new value indicating whether grass grow upon the ground: either the terrain or a mesh set as a parent node.
### Arguments

- *bool* **intersection** - value indicating whether grass grow upon the ground: either the terrain or a mesh set as a parent node

## bool getIntersection () const

Returns the current value indicating whether grass grow upon the ground: either the terrain or a mesh set as a parent node.
### Return value

value indicating whether grass grow upon the ground: either the terrain or a mesh set as a parent node
## void setIntersectionMask ( int mask )

Sets a new intersection mask for the object.
### Arguments

- *int* **mask** - The intersection mask for the object

## int getIntersectionMask () const

Returns the current intersection mask for the object.
### Return value

Current intersection mask for the object
## void setOrientation ( bool orientation )

Sets a new flag indicating if grass polygons are oriented along the normal of its parent (for example, a terrain).
### Arguments

- *bool* **orientation** - flag indicating if grass polygons are oriented along the normal of its parent (for example, a terrain)

## bool getOrientation () const

Returns the current flag indicating if grass polygons are oriented along the normal of its parent (for example, a terrain).
### Return value

flag indicating if grass polygons are oriented along the normal of its parent (for example, a terrain)
## void setVariation ( bool variation )

Sets a new value indicating if the random horizontal flip for grass polygons is set.
### Arguments

- *bool* **variation** - value indicating if the random horizontal flip for grass polygons is set

## bool getVariation () const

Returns the current value indicating if the random horizontal flip for grass polygons is set.
### Return value

value indicating if the random horizontal flip for grass polygons is set
## void setThinning ( bool thinning )

Sets a new flag indicating if the grass is thinned out with a distance (random grass polygons are not rendered across the grass fade distance).
### Arguments

- *bool* **thinning** - flag indicating if the grass is thinned out with a distance

## bool getThinning () const

Returns the current flag indicating if the grass is thinned out with a distance (random grass polygons are not rendered across the grass fade distance).
### Return value

flag indicating if the grass is thinned out with a distance
## void setFieldMask ( int mask )

Sets a new mask specifying the area of the field node to be applied to the grass. The integer is treated as a bit mask, where each bit is a separate mask.
### Arguments

- *int* **mask** - The mask specifying the area of the field node to be applied to the grass

## int getFieldMask () const

Returns the current mask specifying the area of the field node to be applied to the grass. The integer is treated as a bit mask, where each bit is a separate mask.
### Return value

Current mask specifying the area of the field node to be applied to the grass
## void setTerrainMasks ( const Math:: ivec4 & masks )

Sets a new set of [Landscape Terrain masks](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md#getDetailMask_int_TerrainDetailMask) used for grass placement (a four-component vector combining mask indices, each component in the [0; 19] range, to be used for the corresponding diffuse texture column).
### Arguments

- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md)&* **masks** - The set of Landscape Terrain masks used for grass placement

## Math:: ivec4 getTerrainMasks () const

Returns the current set of [Landscape Terrain masks](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md#getDetailMask_int_TerrainDetailMask) used for grass placement (a four-component vector combining mask indices, each component in the [0; 19] range, to be used for the corresponding diffuse texture column).
### Return value

Current set of Landscape Terrain masks used for grass placement
---

## static ObjectGrassPtr create ( )

Constructor. Creates a new grass object.
## void setAspect ( const Math:: vec4 & mean , const Math:: vec4 & spread )

Sets the aspect of the grass polygons (width to height ratio).
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **mean** - Mean value of grass aspect.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **spread** - Spread value of grass aspect.

## Math:: vec4 getAspectMean ( ) const

Returns the current mean value of the grass aspect (width to height ratio), defined for four diffuse texture columns.
### Return value

Mean value of grass aspect.
## Math:: vec4 getAspectSpread ( ) const

Returns the current spread value of the grass aspect (width to height ratio), defined for four diffuse texture columns.
### Return value

Spread value of grass aspect.
## int setMaskImage ( const Ptr < Image > & image , int invalidate = 1 )

Sets an image that defines the areas of growing grass. Possible mask formats are *R8*, *RG8*, *RGB8* and *RGBA8*.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Pointer to the image.
- *int* **invalidate** - Invalidate flag. Set **1** to invalidate all grass cells; otherwise, set **0**. All invalidated cells will be regenerated.

### Return value

**1** if the mask image is successfully set; otherwise, **0**.
## int getMaskImage ( const Ptr < Image > & image ) const

Writes the image that is currently used to define the areas of grass growing into the given buffer. Possible mask formats are *R8*, *RG8*, *RGB8* and *RGBA8*.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image buffer to store a mask into.

### Return value

**1** if the mask image is successfully written into the buffer; otherwise, **0**.
## void setMaskImageName ( const char * image_name , int invalidate = 1 )

Sets the name of a mask image that defines the areas of growing grass. Possible mask formats are *R8*, *RG8*, *RGB8* and *RGBA8*.
### Arguments

- *const char ** **image_name** - Name (path) of the mask image.
- *int* **invalidate** - Invalidate flag. Set **1** to invalidate all grass cells; otherwise, set **0**. All invalidated cells will be regenerated.

## const char * getMaskImageName ( ) const

Returns a name of the current mask image that defines the areas of grass growing. Possible mask formats are *R8*, *RG8*, *RGB8* and *RGBA8*.
### Return value

Name (path) of the mask image.
## int setMaskMesh ( const Ptr < Mesh > & mesh , int invalidate = 1 )

Sets a mesh to be used as a mask on-the-fly. Limitations:
- Before the method is called, another mesh must be set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void) first.
- If the world is reloaded, the mesh set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void) will be loaded.
- If the memory limit is exceeded, the new mesh might be replaced with the mesh set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void).


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - Pointer to the mesh.
- *int* **invalidate** - Invalidate flag. Set **1** to invalidate all grass cells; otherwise, set **0**. All invalidated cells will be regenerated.

### Return value

**1** if the mesh is set successfully; otherwise - **0**.
## int getMaskMesh ( const Ptr < Mesh > & mesh ) const

Copies the current mask mesh (if it exists) to the specified target mesh.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - Pointer to the mesh to copy the current mask mesh to.

### Return value

**1** if mesh mask exists; otherwise - **0**.
## void setMaskMeshName ( const char * mesh_name , int invalidate = 1 )

Sets a mesh to be used as a mask for the grass. This mesh should be plane.
### Arguments

- *const char ** **mesh_name** - Path to the **.mesh* file.
- *int* **invalidate** - Invalidate flag. Set **1** to invalidate all grass cells; otherwise, set **0**. All invalidated cells will be regenerated.

## const char * getMaskMeshName ( ) const

Returns the name (path) of the current mesh used as a mask for the grass. This mesh should be plane.
### Return value

Path to the **.mesh* file.
## void setMaxBend ( const Math:: vec4 & mean , const Math:: vec4 & spread )

Sets the maximum grass bending parameters (rendered in areas with the highest density according to the mask). Bend angles (mean and spread) are defined for four diffuse texture columns. The resulting value is determined as follows: `Result = Mean + Random * Spread`, where `Random` is a random value in range from -1 to 1.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **mean** - Vector of mean values of grass bending angles to be set for four diffuse texture columns.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **spread** - Vector of spread values of grass bending angles to be set for four diffuse texture columns.

## Math:: vec4 getMaxBendMean ( ) const

Returns the mean value for the maximum grass bending (rendered in areas with the highest density according to the mask). Bend angles are defined for four diffuse texture columns.
### Return value

Vector of mean values of grass bending angles for four diffuse texture columns.
## Math:: vec4 getMaxBendSpread ( ) const

Returns the spread value for the maximum grass bending (rendered in areas with the highest density according to the mask). Bend angles are defined for four diffuse texture columns.
### Return value

Vector of spread values of grass bending angles for four diffuse texture columns.
## void setMinBend ( const Math:: vec4 & mean , const Math:: vec4 & spread )

Sets the minimum grass bending parameters (rendered in areas with the lowest density according to the mask). Bend angles (mean and spread) are defined for four diffuse texture columns. The resulting value is determined as follows: `Result = Mean + Random * Spread`, where `Random` is a random value in range from -1 to 1.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **mean** - Vector of mean values of grass bending angles to be set for four diffuse texture columns.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **spread** - Vector of spread values of grass bending angles to be set for four diffuse texture columns.

## Math:: vec4 getMinBendMean ( ) const

Returns the mean value for the minimum grass bending (rendered in areas with the lowest density according to the mask). Bend angles are defined for four diffuse texture columns.
### Return value

Vector of mean values of grass bending angles for four diffuse texture columns.
## Math:: vec4 getMinBendSpread ( ) const

Returns the spread value for the minimum grass bending (rendered in areas with the lowest density according to the mask). Bend angles are defined for four diffuse texture columns.
### Return value

Vector of spread values of grass bending angles for four diffuse texture columns.
## void setMaxHeight ( const Math:: vec4 & mean , const Math:: vec4 & spread )

Sets the maximum grass height (rendered in areas with the highest density according to the mask). The height is defined for four diffuse texture columns, as mean and spread values ( `Result = Mean + Random * Spread`, where `Random` is a random value in range from -1 to 1).
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **mean** - Mean value for the maximum grass height in units. If a negative value is provided, EPSILON will be used instead.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **spread** - Spread value for the maximum grass height in units.

## Math:: vec4 getMaxHeightMean ( ) const

Returns the mean value for the maximum grass height (rendered in areas with the highest density according to the mask). The height is defined for four diffuse texture columns.
### Return value

Mean value for the maximum grass height in units.
## Math:: vec4 getMaxHeightSpread ( ) const

Returns the spread value for the maximum grass height (rendered in areas with the highest density according to the mask). The height is defined for four diffuse texture columns.
### Return value

Spread value for the maximum grass height in units.
## void setMinHeight ( const Math:: vec4 & mean , const Math:: vec4 & spread )

Sets the minimum grass height (rendered in areas with the lowest density according to the mask). The height is defined for four diffuse texture columns, as mean and spread values ( `Result = Mean + Random * Spread`, where `Random` is a random value in range from -1 to 1).
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **mean** - Mean value for the minimum grass height in units. If a negative value is provided, EPSILON will be used instead.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **spread** - Spread value for the minimum grass height in units.

## Math:: vec4 getMinHeightMean ( ) const

Returns the mean value for the minimum grass height (rendered in areas with the lowest density according to the mask). The height is defined for four diffuse texture columns.
### Return value

Mean value for the minimum grass height in units.
## Math:: vec4 getMinHeightSpread ( ) const

Returns the spread value for the minimum grass height (rendered in areas with the lowest density according to the mask). The height is defined for four diffuse texture columns.
### Return value

Spread value for the minimum grass height in units.
## void setOffset ( const Math:: vec4 & mean , const Math:: vec4 & spread )

Sets the grass offset from the surface along the surface normal, defined for four diffuse texture columns. If a negative mean value is provided, **vec4_eps** will be used instead.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **mean** - Mean value of grass polygons offset in units.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **spread** - Spread value of grass polygons offset in units.

## Math:: vec4 getOffsetMean ( ) const

Returns the current mean value of the grass offset from the surface along the surface normal, defined for four diffuse texture columns.
### Return value

Mean value of grass polygons offset in units.
## Math:: vec4 getOffsetSpread ( ) const

Returns the current spread value for the grass offset from the surface along the surface normal, defined for four diffuse texture columns.
### Return value

Spread value for grass polygons offset in units.
## void setRotation ( const Math:: vec4 & mean , const Math:: vec4 & spread )

Sets the grass rotation. Rotation is defined for four diffuse texture columns, as mean and spread values ( `Result = Mean + Random * Spread`, where `Random` is a random value in range from -1 to 1).
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **mean** - Mean value of grass polygons rotation, in degrees.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **spread** - Spread value of grass polygons rotation, in degrees.

## Math:: vec4 getRotationMean ( ) const

Returns the current mean value for the grass rotation, defined for four diffuse texture columns.
### Return value

Mean value of grass polygons rotation, in degrees.
## Math:: vec4 getRotationSpread ( ) const

Returns the current spread value for the grass rotation, defined for four diffuse texture columns.
### Return value

Spread value of grass polygons rotation, in degrees.
## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cpp.md) type identifier.
## void invalidate ( )

Invalidates all grass cells. All invalidated cells will be regenerated.
## void invalidate ( const Math:: WorldBoundBox & bounds )

Invalidates all grass cells within the area specified by the given bounding box. All invalidated cells will be regenerated.
### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bounds** - Bounding box, defining the area, where grass cells will be regenerated.
