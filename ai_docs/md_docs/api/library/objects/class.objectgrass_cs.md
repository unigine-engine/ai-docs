# ObjectGrass Class (CS)

**Inherits from:** Object


This class is used to create [grass](../../../objects/objects/grass/index.md). The grass object is rendered in grid [cells](../../../objects/objects/grass/index.md#step).


You can use [a mask](#setCutoutIntersectionMask_int_void) to cut out grass in the areas of intersection with other objects and decals (e.g. to remove vegetation under houses or from the surface of roads projected using decals).


## ObjectGrass Class

### Properties

## bool CutoutInverse

The value indicating if the grass is rendered inside or outside the areas determined by the [cutout intersection mask](#setCutoutIntersectionMask_int_void).
## int CutoutIntersectionMask

The cutout intersection mask. this mask allows you to cut out the grass in the areas of intersection with objects and decals (e.g. can be used to remove grass under houses or from the surface of roads projected using decals). the grass will be cut out by objects and decals that have their intersection mask matching this one (one bit at least).
> **Notice:** To set intersection masks the following methods can be used:
> - **for decals** use *[getIntersectionMask()](../../../api/library/decals/class.decal_cs.md#getIntersectionMask_int)*
> - **for objects** use *[getIntersectionMask()](../../../api/library/objects/class.object_cs.md#getIntersectionMask_int_int)*

## bool MaskInverse

The flag indicating if the grass is rendered inside or outside the mask mesh contour.
## int MaskMaxValue

The maximum value of the mask application range (a color range from **0** to **255**, indicating that only that part of mask, which contains this color range, will be applied to the image).
## int MaskMinValue

The minimum value of the mask application range.
## int MaskFlipY

The flag indicating if a mask is flipped by y axis.
## int MaskFlipX

The flag indicating if a mask is flipped by x axis.
## vec4 Probability

The grass rendering probability per column (in the diffuse texture). the higher the value for some column, the more frequently it will be rendered. Any values can be set, since they are normalized.
## float Angle

The angle cosine defining the slope steepness appropriate for grass growing, in range from **0** to **1**.
## float Threshold

The threshold for density, starting from which the grass is rendered.
## float Density

The density factor for the grass per square unit.
## int Subdivision

The divisor used to subdivide grass rendering cells into smaller sub-cells. The value is clamped to a range **[1;32]**. subdividing is used if a grass node is used as a distant lod for [WorldClutter](../../../api/library/worlds/class.worldclutter_cs.md) or [ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_cs.md) with smaller cells. This way, positions of randomly scattered objects will coincide with those of grass-based impostors.
## float Step

The step for cells used to render grass.
## float SizeY

The length of the grass object along the y-coordinate, in units. If a negative value is provided, **0** will be used instead.
## float SizeX

The width of the grass object along the x-coordinate, in units. If a negative value is provided, **0** will be used instead.
## int Seed

The seed used for pseudo-random positioning of grass. If a negative value is provided, **0** will be used instead.
## int NumTextures

The number of rows contained in the [grass diffuse texture](../../../content/materials/library/grass_base/index.md#texture_diffuse), in the **[1; 4]** range.
## bool Intersection

The value indicating whether grass grow upon the ground: either the terrain or a mesh set as a parent node.
## int IntersectionMask

The intersection mask for the object.
## bool Orientation

The flag indicating if grass polygons are oriented along the normal of its parent (for example, a terrain).
## bool Variation

The value indicating if the random horizontal flip for grass polygons is set.
## bool Thinning

The flag indicating if the grass is thinned out with a distance (random grass polygons are not rendered across the grass fade distance).
## int FieldMask

The mask specifying the area of the field node to be applied to the grass. The integer is treated as a bit mask, where each bit is a separate mask.
## ivec4 TerrainMasks

The set of [Landscape Terrain masks](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cs.md#getDetailMask_int_TerrainDetailMask) used for grass placement (a four-component vector combining mask indices, each component in the [0; 19] range, to be used for the corresponding diffuse texture column).
### Members

---

## ObjectGrass ( )

Constructor. Creates a new grass object.
## void SetAspect ( vec4 mean , vec4 spread )

Sets the aspect of the grass polygons (width to height ratio).
### Arguments

- *vec4* **mean** - Mean value of grass aspect.
- *vec4* **spread** - Spread value of grass aspect.

## vec4 GetAspectMean ( )

Returns the current mean value of the grass aspect (width to height ratio), defined for four diffuse texture columns.
### Return value

Mean value of grass aspect.
## vec4 GetAspectSpread ( )

Returns the current spread value of the grass aspect (width to height ratio), defined for four diffuse texture columns.
### Return value

Spread value of grass aspect.
## int SetMaskImage ( Image image , int invalidate = 1 )

Sets an image that defines the areas of growing grass. Possible mask formats are *R8*, *RG8*, *RGB8* and *RGBA8*.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Pointer to the image.
- *int* **invalidate** - Invalidate flag. Set **1** to invalidate all grass cells; otherwise, set **0**. All invalidated cells will be regenerated.

### Return value

**1** if the mask image is successfully set; otherwise, **0**.
## int GetMaskImage ( Image image )

Writes the image that is currently used to define the areas of grass growing into the given buffer. Possible mask formats are *R8*, *RG8*, *RGB8* and *RGBA8*.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image buffer to store a mask into.

### Return value

**1** if the mask image is successfully written into the buffer; otherwise, **0**.
## void SetMaskImageName ( string image_name , int invalidate = 1 )

Sets the name of a mask image that defines the areas of growing grass. Possible mask formats are *R8*, *RG8*, *RGB8* and *RGBA8*.
### Arguments

- *string* **image_name** - Name (path) of the mask image.
- *int* **invalidate** - Invalidate flag. Set **1** to invalidate all grass cells; otherwise, set **0**. All invalidated cells will be regenerated.

## string GetMaskImageName ( )

Returns a name of the current mask image that defines the areas of grass growing. Possible mask formats are *R8*, *RG8*, *RGB8* and *RGBA8*.
### Return value

Name (path) of the mask image.
## int SetMaskMesh ( Mesh mesh , int invalidate = 1 )

Sets a mesh to be used as a mask on-the-fly. Limitations:
- Before the method is called, another mesh must be set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void) first.
- If the world is reloaded, the mesh set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void) will be loaded.
- If the memory limit is exceeded, the new mesh might be replaced with the mesh set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void).


### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Mesh instance.
- *int* **invalidate** - Invalidate flag. Set **1** to invalidate all grass cells; otherwise, set **0**. All invalidated cells will be regenerated.

### Return value

**1** if the mesh is set successfully; otherwise - **0**.
## int GetMaskMesh ( Mesh mesh )

Copies the current mask mesh (if it exists) to the specified target mesh.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Mesh instance to copy the current mask mesh to.

### Return value

**1** if mesh mask exists; otherwise - **0**.
## void SetMaskMeshName ( string mesh_name , int invalidate = 1 )

Sets a mesh to be used as a mask for the grass. This mesh should be plane.
### Arguments

- *string* **mesh_name** - Path to the **.mesh* file.
- *int* **invalidate** - Invalidate flag. Set **1** to invalidate all grass cells; otherwise, set **0**. All invalidated cells will be regenerated.

## string GetMaskMeshName ( )

Returns the name (path) of the current mesh used as a mask for the grass. This mesh should be plane.
### Return value

Path to the **.mesh* file.
## void SetMaxBend ( vec4 mean , vec4 spread )

Sets the maximum grass bending parameters (rendered in areas with the highest density according to the mask). Bend angles (mean and spread) are defined for four diffuse texture columns. The resulting value is determined as follows: `Result = Mean + Random * Spread`, where `Random` is a random value in range from -1 to 1.
### Arguments

- *vec4* **mean** - Vector of mean values of grass bending angles to be set for four diffuse texture columns.
- *vec4* **spread** - Vector of spread values of grass bending angles to be set for four diffuse texture columns.

## vec4 GetMaxBendMean ( )

Returns the mean value for the maximum grass bending (rendered in areas with the highest density according to the mask). Bend angles are defined for four diffuse texture columns.
### Return value

Vector of mean values of grass bending angles for four diffuse texture columns.
## vec4 GetMaxBendSpread ( )

Returns the spread value for the maximum grass bending (rendered in areas with the highest density according to the mask). Bend angles are defined for four diffuse texture columns.
### Return value

Vector of spread values of grass bending angles for four diffuse texture columns.
## void SetMinBend ( vec4 mean , vec4 spread )

Sets the minimum grass bending parameters (rendered in areas with the lowest density according to the mask). Bend angles (mean and spread) are defined for four diffuse texture columns. The resulting value is determined as follows: `Result = Mean + Random * Spread`, where `Random` is a random value in range from -1 to 1.
### Arguments

- *vec4* **mean** - Vector of mean values of grass bending angles to be set for four diffuse texture columns.
- *vec4* **spread** - Vector of spread values of grass bending angles to be set for four diffuse texture columns.

## vec4 GetMinBendMean ( )

Returns the mean value for the minimum grass bending (rendered in areas with the lowest density according to the mask). Bend angles are defined for four diffuse texture columns.
### Return value

Vector of mean values of grass bending angles for four diffuse texture columns.
## vec4 GetMinBendSpread ( )

Returns the spread value for the minimum grass bending (rendered in areas with the lowest density according to the mask). Bend angles are defined for four diffuse texture columns.
### Return value

Vector of spread values of grass bending angles for four diffuse texture columns.
## void SetMaxHeight ( vec4 mean , vec4 spread )

Sets the maximum grass height (rendered in areas with the highest density according to the mask). The height is defined for four diffuse texture columns, as mean and spread values ( `Result = Mean + Random * Spread`, where `Random` is a random value in range from -1 to 1).
### Arguments

- *vec4* **mean** - Mean value for the maximum grass height in units. If a negative value is provided, EPSILON will be used instead.
- *vec4* **spread** - Spread value for the maximum grass height in units.

## vec4 GetMaxHeightMean ( )

Returns the mean value for the maximum grass height (rendered in areas with the highest density according to the mask). The height is defined for four diffuse texture columns.
### Return value

Mean value for the maximum grass height in units.
## vec4 GetMaxHeightSpread ( )

Returns the spread value for the maximum grass height (rendered in areas with the highest density according to the mask). The height is defined for four diffuse texture columns.
### Return value

Spread value for the maximum grass height in units.
## void SetMinHeight ( vec4 mean , vec4 spread )

Sets the minimum grass height (rendered in areas with the lowest density according to the mask). The height is defined for four diffuse texture columns, as mean and spread values ( `Result = Mean + Random * Spread`, where `Random` is a random value in range from -1 to 1).
### Arguments

- *vec4* **mean** - Mean value for the minimum grass height in units. If a negative value is provided, EPSILON will be used instead.
- *vec4* **spread** - Spread value for the minimum grass height in units.

## vec4 GetMinHeightMean ( )

Returns the mean value for the minimum grass height (rendered in areas with the lowest density according to the mask). The height is defined for four diffuse texture columns.
### Return value

Mean value for the minimum grass height in units.
## vec4 GetMinHeightSpread ( )

Returns the spread value for the minimum grass height (rendered in areas with the lowest density according to the mask). The height is defined for four diffuse texture columns.
### Return value

Spread value for the minimum grass height in units.
## void SetOffset ( vec4 mean , vec4 spread )

Sets the grass offset from the surface along the surface normal, defined for four diffuse texture columns. If a negative mean value is provided, **vec4_eps** will be used instead.
### Arguments

- *vec4* **mean** - Mean value of grass polygons offset in units.
- *vec4* **spread** - Spread value of grass polygons offset in units.

## vec4 GetOffsetMean ( )

Returns the current mean value of the grass offset from the surface along the surface normal, defined for four diffuse texture columns.
### Return value

Mean value of grass polygons offset in units.
## vec4 GetOffsetSpread ( )

Returns the current spread value for the grass offset from the surface along the surface normal, defined for four diffuse texture columns.
### Return value

Spread value for grass polygons offset in units.
## void SetRotation ( vec4 mean , vec4 spread )

Sets the grass rotation. Rotation is defined for four diffuse texture columns, as mean and spread values ( `Result = Mean + Random * Spread`, where `Random` is a random value in range from -1 to 1).
### Arguments

- *vec4* **mean** - Mean value of grass polygons rotation, in degrees.
- *vec4* **spread** - Spread value of grass polygons rotation, in degrees.

## vec4 GetRotationMean ( )

Returns the current mean value for the grass rotation, defined for four diffuse texture columns.
### Return value

Mean value of grass polygons rotation, in degrees.
## vec4 GetRotationSpread ( )

Returns the current spread value for the grass rotation, defined for four diffuse texture columns.
### Return value

Spread value of grass polygons rotation, in degrees.
## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cs.md) type identifier.
## void Invalidate ( )

Invalidates all grass cells. All invalidated cells will be regenerated.
## void Invalidate ( WorldBoundBox bounds )

Invalidates all grass cells within the area specified by the given bounding box. All invalidated cells will be regenerated.
### Arguments

- *[WorldBoundBox](../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bounds** - Bounding box, defining the area, where grass cells will be regenerated.
