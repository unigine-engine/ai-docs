# Unigine.WorldClutter Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


[WorldClutter](../../../objects/worlds/world_clutter/index.md) class allows to randomly position [reference nodes](../../../api/library/nodes/class.nodereference_usc.md) according to the [mask](#setMaskImageName_cstr_int_void) and using the specified [seed](#setSeed_int_void). For each node a [probability of appearing](#setReferenceProbability_int_float_void) is set. All nodes in the *World Clutter* are rendered visible only within a specified [distance](#setVisibleDistance_float_void) and then [fade out](#setFadeDistance_float_void). Just like the [ObjectGrass](../../../api/library/objects/class.objectgrass_usc.md), *World Clutter* is rendered in cells.


There are two benefits of using WorldClutter:


- Instances of nodes that are currently outside the view frustum are not stored in the memory, which provides much more efficient memory usage.
- Less cluttered spatial tree, which allows, for example, faster collision detection.


You can use [a mask](#setCutoutIntersectionMask_int_void) to cut out clutter objects in the areas of intersection with other objects and decals (e.g. to remove vegetation under houses or from the surface of roads projected using decals).


### See Also


UnigineScript sample


## WorldClutter Class

### Members

## void setCutoutInverse ( int inverse )

Sets a new value indicating if the clutter objects is rendered inside or outside the areas determined by the [*Cutout Intersection* mask](#setCutoutIntersectionMask_int_void).
### Arguments

- *int* **inverse** - The flag: **0** for rendering clutter objects outside the areas determined by the *Cutout Intersection* mask; **1** for rendering the clutter objects inside these areas.

## int getCutoutInverse () const

Returns the current value indicating if the clutter objects is rendered inside or outside the areas determined by the [*Cutout Intersection* mask](#setCutoutIntersectionMask_int_void).
### Return value

Current flag: **0** for rendering clutter objects outside the areas determined by the *Cutout Intersection* mask; **1** for rendering the clutter objects inside these areas.
## void setCutoutIntersectionMask ( int mask )

Sets a new *Cutout Intersection* mask. This mask allows you to cut out clutter objects in the areas of intersection with other Objects and Decals (e.g. can be used to remove vegetation under houses or from the surface of roads projected using Decals).
Clutter objects will be cut out by objects and decals that have their *Intersection* mask matching this one (one bit at least).


> **Notice:** To set intersection masks the following methods can be used:
>
>
> - **for decals** use *[getIntersectionMask()](../../../api/library/decals/class.decal_usc.md#getIntersectionMask_int)*
> - **for objects** use *[getIntersectionMask()](../../../api/library/objects/class.object_usc.md#getIntersectionMask_int_int)*


### Arguments

- *int* **mask** - The mask - an integer, each bit of which is a mask.

## int getCutoutIntersectionMask () const

Returns the current *Cutout Intersection* mask. This mask allows you to cut out clutter objects in the areas of intersection with other Objects and Decals (e.g. can be used to remove vegetation under houses or from the surface of roads projected using Decals).
Clutter objects will be cut out by objects and decals that have their *Intersection* mask matching this one (one bit at least).


> **Notice:** To set intersection masks the following methods can be used:
>
>
> - **for decals** use *[getIntersectionMask()](../../../api/library/decals/class.decal_usc.md#getIntersectionMask_int)*
> - **for objects** use *[getIntersectionMask()](../../../api/library/objects/class.object_usc.md#getIntersectionMask_int_int)*


### Return value

Current mask - an integer, each bit of which is a mask.
## void setMaskInverse ( int inverse )

Sets a new flag indicating if reference nodes are rendered inside or outside the mask mesh contour.
### Arguments

- *int* **inverse** - The flag: **0** for rendering reference nodes inside the mesh contour; **1** for rendering them outside.

## int getMaskInverse () const

Returns the current flag indicating if reference nodes are rendered inside or outside the mask mesh contour.
### Return value

Current flag: **0** for rendering reference nodes inside the mesh contour; **1** for rendering them outside.
## void setMaskMaxValue ( int value )

Sets a new maximum mask value for the WorldClutter object.
### Arguments

- *int* **value** - The maximum mask value.

## int getMaskMaxValue () const

Returns the current maximum mask value for the WorldClutter object.
### Return value

Current maximum mask value.
## void setMaskMinValue ( int value )

Sets a new minimum mask value for the WorldClutter object.
### Arguments

- *int* **value** - The minimum mask value.

## int getMaskMinValue () const

Returns the current minimum mask value for the WorldClutter object.
### Return value

Current minimum mask value.
## void setMaskFlipY ( int y )

Sets a new flag indicating if a mask is flipped by Y axis.
### Arguments

- *int* **y** - The positive value for flipping the mask; otherwise, **0**.

## int getMaskFlipY () const

Returns the current flag indicating if a mask is flipped by Y axis.
### Return value

Current positive value for flipping the mask; otherwise, **0**.
## void setMaskFlipX ( int x )

Sets a new flag indicating if a mask is flipped by X axis.
### Arguments

- *int* **x** - The positive value for flipping the mask; otherwise, **0**.

## int getMaskFlipX () const

Returns the current flag indicating if a mask is flipped by X axis.
### Return value

Current positive value for flipping the mask; otherwise, **0**.
## void setAngle ( float angle )

Sets a new angle cosine that defines the slope steepness appropriate for positioning nodes.
### Arguments

- *float* **angle** - The slope angle cosine. The provided value is saturated in range [0;1].

## float getAngle () const

Returns the current angle cosine that defines the slope steepness appropriate for positioning nodes.
### Return value

Current slope angle cosine. The provided value is saturated in range [0;1].
## void setThreshold ( float threshold )

Sets a new density threshold (for a mask) starting from which reference nodes are rendered if placed dense enough.
### Arguments

- *float* **threshold** - The density threshold. The provided value is saturated in range [0;1].

## float getThreshold () const

Returns the current density threshold (for a mask) starting from which reference nodes are rendered if placed dense enough.
### Return value

Current density threshold. The provided value is saturated in range [0;1].
## void setDensity ( float density )

Sets a new density factor that defines the number of reference nodes per square unit.
### Arguments

- *float* **density** - The density factor. If a negative value is provided, **0** will be used instead.

## float getDensity () const

Returns the current density factor that defines the number of reference nodes per square unit.
### Return value

Current density factor. If a negative value is provided, **0** will be used instead.
## void setStep ( float step )

Sets a new step for cells used to render node references contained in the *World Clutter*.
### Arguments

- *float* **step** - The step for clutter cells, in units.

## float getStep () const

Returns the current step for cells used to render node references contained in the *World Clutter*.
### Return value

Current step for clutter cells, in units.
## void setSizeY ( float y )

Sets a new length of the *World Clutter* along the Y-coordinate.
### Arguments

- *float* **y** - The Y-coordinate width in units. If a negative value is provided, **0** is used instead.

## float getSizeY () const

Returns the current length of the *World Clutter* along the Y-coordinate.
### Return value

Current Y-coordinate width in units. If a negative value is provided, **0** is used instead.
## void setSizeX ( float x )

Sets a new width of the *World Clutter* along the X-coordinate.
### Arguments

- *float* **x** - The X-coordinate width in units. If a negative value is provided, **0** is used instead.

## float getSizeX () const

Returns the current width of the *World Clutter* along the X-coordinate.
### Return value

Current X-coordinate width in units. If a negative value is provided, **0** is used instead.
## void setSeed ( int seed )

Sets a new seed used for pseudo-random positioning of reference nodes.
### Arguments

- *int* **seed** - The number used to initialize a pseudo-random sequence.

## int getSeed () const

Returns the current seed used for pseudo-random positioning of reference nodes.
### Return value

Current number used to initialize a pseudo-random sequence.
## void setSpawnRate ( int rate )

Sets a new number of cells updated each frame. High number of updated cells may lead to a performance spike.
### Arguments

- *int* **rate** - The number of cells to be updated. If a non-positive value is provided, **1** is used instead.

## int getSpawnRate () const

Returns the current number of cells updated each frame. High number of updated cells may lead to a performance spike.
### Return value

Current number of cells to be updated. If a non-positive value is provided, **1** is used instead.
## void setFadeDistance ( float distance )

Sets a new distance up to which reference nodes are fading out (that is, fewer nodes will be rendered instead of all).
The distance is measured starting from the [visibility distance](#setVisibleDistance_float_void).


> **Notice:** In order for a fade distance to be applied, [visibility distance](#getVisibleDistance_float) should not be infinite.


### Arguments

- *float* **distance** - The distance in units. If a negative value is provided, **0** is used instead.

## float getFadeDistance () const

Returns the current distance up to which reference nodes are fading out (that is, fewer nodes will be rendered instead of all).
The distance is measured starting from the [visibility distance](#setVisibleDistance_float_void).


> **Notice:** In order for a fade distance to be applied, [visibility distance](#getVisibleDistance_float) should not be infinite.


### Return value

Current distance in units. If a negative value is provided, **0** is used instead.
## void setVisibleDistance ( float distance )

Sets a new distance up to which all the reference nodes are rendered. The distance is measured from the camera.
### Arguments

- *float* **distance** - The distance in units. If a negative value is provided, **0** is used instead.

## float getVisibleDistance () const

Returns the current distance up to which all the reference nodes are rendered. The distance is measured from the camera.
### Return value

Current distance in units. If a negative value is provided, **0** is used instead.
## void setIntersection ( int intersection )

Sets a new value indicating whether reference nodes are scattered upon the ground (along its relief): either the terrain or a mesh set as a parent node.
### Arguments

- *int* **intersection** - The flag: positive number - intersection enabled; **0** - disabled.

## int getIntersection () const

Returns the current value indicating whether reference nodes are scattered upon the ground (along its relief): either the terrain or a mesh set as a parent node.
### Return value

Current flag: positive number - intersection enabled; **0** - disabled.
## void setOrientation ( int orientation )

Sets a new value indicating whether reference nodes are oriented along the normals of the ground (either the terrain or a mesh set as a parent node).
### Arguments

- *int* **orientation** - The flag: positive number - orientation enabled; **0** - disabled.

## int getOrientation () const

Returns the current value indicating whether reference nodes are oriented along the normals of the ground (either the terrain or a mesh set as a parent node).
### Return value

Current flag: positive number - orientation enabled; **0** - disabled.
## int getNumReferences () const

Returns the current total number of reference nodes contained in the *World Clutter*.
### Return value

Current number of reference nodes.
## void setIntersectionMask ( int mask )

Sets a new *Intersection* mask for the *World Clutter*.
This mask can be used to cut out areas intersected by the *World Clutter* from *[Grass](../../../api/library/objects/class.objectgrass_usc.md#setCutoutIntersectionMask_int_void), [Mesh Clutter](../../../api/library/objects/class.objectmeshclutter_usc.md#setCutoutIntersectionMask_int_void)* and another *[World Clutter](#setCutoutIntersectionMask_int_void)* (e.g. to remove grass or forest from the surface of roads projected using decals).


> **Notice:** The areas will be cut out only if *Intersection* masks of grass and clutter objects matches this mask (one bit at least).


### Arguments

- *int* **mask** - The *Intersection* mask - an integer, each bit of which is a mask.

## int getIntersectionMask () const

Returns the current *Intersection* mask for the *World Clutter*.
This mask can be used to cut out areas intersected by the *World Clutter* from *[Grass](../../../api/library/objects/class.objectgrass_usc.md#setCutoutIntersectionMask_int_void), [Mesh Clutter](../../../api/library/objects/class.objectmeshclutter_usc.md#setCutoutIntersectionMask_int_void)* and another *[World Clutter](#setCutoutIntersectionMask_int_void)* (e.g. to remove grass or forest from the surface of roads projected using decals).


> **Notice:** The areas will be cut out only if *Intersection* masks of grass and clutter objects matches this mask (one bit at least).


### Return value

Current *Intersection* mask - an integer, each bit of which is a mask.
---

## static WorldClutter ( )

Constructor. Creates a *World Clutter* with default properties.
## void invalidate ( )

Invalidates all cells of the *World Clutter*. All invalidated cells will be regenerated.
## void invalidate ( WorldBoundBox bounds )

Invalidates all cells of the *World Clutter* within the area specified by the given bounding box. All invalidated cells will be regenerated.
### Arguments

- *WorldBoundBox* **bounds** - Bounding box, defining the area, where *World Clutter* cells will be regenerated.

## int setMaskImage ( Image image , int invalidate = 1 )

Sets an image (in *R8* format) that defines the placement of meshes.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Pointer to the image.
- *int* **invalidate** - Invalidate flag. Set **1** to invalidate all *World Clutter* cells; otherwise, set **0**. All invalidated cells will be regenerated.

### Return value

**1** if the mask image is successfully set; otherwise, **0**.
## int getMaskImage ( Image image )

Writes the image that is currently used as a mask for the placement of meshes into the given buffer.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image buffer to store a mask into.

### Return value

**1** if the mask image is successfully written into the buffer; otherwise, **0**.
## void setMaskImageName ( string image_name , int invalidate = 1 )

Sets the name of a new mask image (in *R8* format) that defines the placement of meshes.
### Arguments

- *string* **image_name** - Name (path) of the mask image.
- *int* **invalidate** - Invalidate flag. Set **1** to invalidate all cells of the *World Clutter*; otherwise, set **0**. All invalidated cells will be regenerated.

## string getMaskImageName ( )

Returns the name of a mask image (in *R8* format) that defines the placement of reference nodes.
### Return value

Name (path) of the mask image.
## int setMaskMesh ( Mesh mesh , int invalidate = 1 )


Sets a mesh to be used as a mask on-the-fly. Limitations:


- Before the method is called, another mesh must be set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void) first.
- If the world is reloaded, the mesh set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void) will be loaded.
- If the memory limit is exceeded, the new mesh might be replaced with the mesh set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void).


### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **mesh** - Mesh instance.
- *int* **invalidate** - Invalidate flag. Set **1** to invalidate all cells of the *World Clutter*; otherwise, set **0**. All invalidated cells will be regenerated.

### Return value

**1** if the mesh is set successfully; otherwise - **0**.
## int getMaskMesh ( Mesh mesh )

Copies the current mask mesh (if it exists) to the specified target mesh.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **mesh** - Mesh instance to copy the current mask mesh to.

### Return value

**1** if mesh mask exists; otherwise - **0**.
## void setMaskMeshName ( string mesh_name , int invalidate = 1 )

Sets a mesh to be used as a mask for the *World Clutter*. This mesh should be plane.
### Arguments

- *string* **mesh_name** - Path to the **.mesh* file.
- *int* **invalidate** - Invalidate flag. Set **1** to invalidate all cells of the *World Clutter*; otherwise, set **0**. All invalidated cells will be regenerated.

## string getMaskMeshName ( )

Returns the name (path) of the current mesh used as a mask for the *World Clutter*. This mesh should be plane.
### Return value

Path to the **.mesh* file.
## void setMaxScale ( float mean , float spread )

Sets the scale for meshes in the areas with high density (according to the mask). With the minimum scale it is possible to automatically render, for example, big trees in the center of the forest. A spread value enables to control the range of scales relative to the mean value.
### Arguments

- *float* **mean** - Scale mean value.
- *float* **spread** - Maximum spread value to randomly upscale or downscale objects.

## float getMaxScaleMean ( )

Returns the scale mean value for meshes in the areas with high density (according to the mask).
### Return value

Scale mean value.
## float getMaxScaleSpread ( )

Returns the scale spread value that controls the range of mesh scales in the areas with high density (according to the mask).
### Return value

Scale spread value.
## void setMinScale ( float mean , float spread )

Sets the scale for meshes in the areas with low density (according to the mask). With the minimum scale it is possible to automatically render, for example, small trees at the forest border. A spread value allows to control the range of scales relative to the mean value.
### Arguments

- *float* **mean** - Scale mean value.
- *float* **spread** - Maximum spread value to randomly upscale or downscale objects.

## float getMinScaleMean ( )

Returns the scale mean value for meshes in the areas with low density (according to the mask).
### Return value

Scale mean value.
## float getMinScaleSpread ( )

Returns the scale spread value that controls the range of mesh scales in the areas with low density (according to the mask).
### Return value

Scale spread value.
## void setNodesRotation ( vec3 mean , vec3 spread )

Sets the rotation of reference nodes along X, Y and Z axes.
### Arguments

- *vec3* **mean** - Mean values of rotation angles in degrees.
- *vec3* **spread** - Spread values of rotation angles in degrees.

## vec3 getNodesRotationMean ( )

Returns the mean value of reference nodes rotation along X, Y and Z axes.
### Return value

Mean values of rotation angles in degrees.
## vec3 getNodesRotationSpread ( )

Returns the spread value of reference nodes rotation along X, Y and Z axes.
### Return value

Spread values of rotation angles in degrees.
## void setOffset ( float mean , float spread )

Sets the vertical offset that determines the placement of reference nodes above or below the surface.
### Arguments

- *float* **mean** - Mean value of the offset in units.
- *float* **spread** - Spread value of the offset in units.

## float getOffsetMean ( )

Returns the current mean value of the vertical offset that determines the placement of reference nodes above or below the surface.
### Return value

Mean value of the offset in units.
## float getOffsetSpread ( )

Returns the current spread value of the vertical offset that determines the placement of reference nodes above or below the surface.
### Return value

Spread value of the offset in units.
## void setReferenceName ( int num , string name )

Sets the name of the specified reference node contained in the *World Clutter*.
### Arguments

- *int* **num** - The number of the reference node.
- *string* **name** - Name to be updated.

## string getReferenceName ( int num )

Returns the name of the reference node contained in the *World Clutter*.
### Arguments

- *int* **num** - The number of the reference node among contained in the *World Clutter*.

### Return value

Name of the reference node.
## void setReferenceProbability ( int num , float probability )

Sets the probability of the occurrence of the specified node reference.
### Arguments

- *int* **num** - The number of the reference node.
- *float* **probability** - Probability factor. The provided value is saturated in range [0.0f, 1.0f].

## float getReferenceProbability ( int num )

Returns the probability of the occurrence of the specified node reference.
### Arguments

- *int* **num** - The number of the reference node.

### Return value

Probability factor.
## int addReference ( string name )

Adds a new reference node to the *World Clutter*.
### Arguments

- *string* **name** - Name of the reference node.

### Return value

The number of added reference node.
## void removeReference ( int num )

Removes the specified reference node from the *World Clutter*.
### Arguments

- *int* **num** - The number of the reference node.

## static int type ( )

Returns the type of the node.
### Return value

[World](../../../api/library/engine/class.world_usc.md) type identifier.
## void clearReferences ( )

Deletes all reference nodes from the *World Clutter*.
## int saveStateReferences ( Stream stream )

Saves the state of all reference nodes from the *World Clutter* to the specified stream.


**Example** using *saveStateReferences()* and *[restoreStateReferences()](#restoreStateReferences_Stream_int)* methods:


```cpp
// initialize a node and set its state
WorldClutter worldClutter = new WorldClutter();
worldClutter.setSizeX(500.0f);
worldClutter.setSizeY(500.0f);

// save state
Blob blob_state = new Blob();
worldClutter.saveStateReferences(blob_state);

// change state
worldClutter.setSizeY(700.0f);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
worldClutter.restoreStateReferences(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream instance.

### Return value

**1** if the states of all reference nodes from the *World Clutter* were successfully saved to the specified stream; otherwise, **0**.
## int restoreStateReferences ( Stream stream )


Restores the state of all reference nodes from the *World Clutter* from the specified stream.


**Example** using *[saveStateReferences()](#saveStateReferences_Stream_int)* and *restoreStateReferences()* methods:


```cpp
// initialize a node and set its state
WorldClutter worldClutter = new WorldClutter();
worldClutter.setSizeX(500.0f);
worldClutter.setSizeY(500.0f);

// save state
Blob blob_state = new Blob();
worldClutter.saveStateReferences(blob_state);

// change state
worldClutter.setSizeY(700.0f);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
worldClutter.restoreStateReferences(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream instance.

### Return value

**1** if the states of all reference nodes from the *World Clutter* were successfully restored from the specified stream; otherwise, **0**.
