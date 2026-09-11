# Unigine.WorldClutter Class (CS)

**Inherits from:** Node


[WorldClutter](../../../objects/worlds/world_clutter/index.md) class allows to randomly position [reference nodes](../../../api/library/nodes/class.nodereference_cs.md) according to the [mask](#setMaskImageName_cstr_int_void) and using the specified [seed](#setSeed_int_void). For each node a [probability of appearing](#setReferenceProbability_int_float_void) is set. All nodes in the *World Clutter* are rendered visible only within a specified [distance](#setVisibleDistance_float_void) and then [fade out](#setFadeDistance_float_void). Just like the [ObjectGrass](../../../api/library/objects/class.objectgrass_cs.md), *World Clutter* is rendered in cells.


There are two benefits of using WorldClutter:


- Instances of nodes that are currently outside the view frustum are not stored in the memory, which provides much more efficient memory usage.
- Less cluttered spatial tree, which allows, for example, faster collision detection.


You can use [a mask](#setCutoutIntersectionMask_int_void) to cut out clutter objects in the areas of intersection with other objects and decals (e.g. to remove vegetation under houses or from the surface of roads projected using decals).


### See Also


UnigineScript sample


## WorldClutter Class

### Properties

## int CutoutInverse

The value indicating if the clutter objects is rendered inside or outside the areas determined by the [*Cutout Intersection* mask](#setCutoutIntersectionMask_int_void).
## int CutoutIntersectionMask

The *Cutout Intersection* mask. This mask allows you to cut out clutter objects in the areas of intersection with other Objects and Decals (e.g. can be used to remove vegetation under houses or from the surface of roads projected using Decals).
Clutter objects will be cut out by objects and decals that have their *Intersection* mask matching this one (one bit at least).


> **Notice:** To set intersection masks the following methods can be used:
>
>
> - **for decals** use *[getIntersectionMask()](../../../api/library/decals/class.decal_cs.md#getIntersectionMask_int)*
> - **for objects** use *[getIntersectionMask()](../../../api/library/objects/class.object_cs.md#getIntersectionMask_int_int)*


## int MaskInverse

The flag indicating if reference nodes are rendered inside or outside the mask mesh contour.
## int MaskMaxValue

The maximum mask value for the WorldClutter object.
## int MaskMinValue

The minimum mask value for the WorldClutter object.
## int MaskFlipY

The flag indicating if a mask is flipped by Y axis.
## int MaskFlipX

The flag indicating if a mask is flipped by X axis.
## float Angle

The angle cosine that defines the slope steepness appropriate for positioning nodes.
## float Threshold

The density threshold (for a mask) starting from which reference nodes are rendered if placed dense enough.
## float Density

The density factor that defines the number of reference nodes per square unit.
## float Step

The step for cells used to render node references contained in the *World Clutter*.
## float SizeY

The length of the *World Clutter* along the Y-coordinate.
## float SizeX

The width of the *World Clutter* along the X-coordinate.
## int Seed

The seed used for pseudo-random positioning of reference nodes.
## int SpawnRate

The number of cells updated each frame. High number of updated cells may lead to a performance spike.
## float FadeDistance

The distance up to which reference nodes are fading out (that is, fewer nodes will be rendered instead of all).
The distance is measured starting from the [visibility distance](#setVisibleDistance_float_void).


> **Notice:** In order for a fade distance to be applied, [visibility distance](#getVisibleDistance_float) should not be infinite.


## float VisibleDistance

The distance up to which all the reference nodes are rendered. The distance is measured from the camera.
## int Intersection

The value indicating whether reference nodes are scattered upon the ground (along its relief): either the terrain or a mesh set as a parent node.
## int Orientation

The value indicating whether reference nodes are oriented along the normals of the ground (either the terrain or a mesh set as a parent node).
## 🔒︎ int NumReferences

The total number of reference nodes contained in the *World Clutter*.
## int IntersectionMask

The *Intersection* mask for the *World Clutter*.
This mask can be used to cut out areas intersected by the *World Clutter* from *[Grass](../../../api/library/objects/class.objectgrass_cs.md#setCutoutIntersectionMask_int_void), [Mesh Clutter](../../../api/library/objects/class.objectmeshclutter_cs.md#setCutoutIntersectionMask_int_void)* and another *[World Clutter](#setCutoutIntersectionMask_int_void)* (e.g. to remove grass or forest from the surface of roads projected using decals).


> **Notice:** The areas will be cut out only if *Intersection* masks of grass and clutter objects matches this mask (one bit at least).


### Members

---

## WorldClutter ( )

Constructor. Creates a *World Clutter* with default properties.
## void Invalidate ( )

Invalidates all cells of the *World Clutter*. All invalidated cells will be regenerated.
## void Invalidate ( WorldBoundBox bounds )

Invalidates all cells of the *World Clutter* within the area specified by the given bounding box. All invalidated cells will be regenerated.
### Arguments

- *[WorldBoundBox](../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bounds** - Bounding box, defining the area, where *World Clutter* cells will be regenerated.

## int SetMaskImage ( Image image , bool invalidate = 1 )

Sets an image (in *R8* format) that defines the placement of meshes.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Pointer to the image.
- *bool* **invalidate** - Invalidate flag. Set true to invalidate all *World Clutter* cells; otherwise, set false. All invalidated cells will be regenerated.

### Return value

**1** if the mask image is successfully set; otherwise, **0**.
## int GetMaskImage ( Image image )

Writes the image that is currently used as a mask for the placement of meshes into the given buffer.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image buffer to store a mask into.

### Return value

**1** if the mask image is successfully written into the buffer; otherwise, **0**.
## void SetMaskImageName ( string image_name , bool invalidate = 1 )

Sets the name of a new mask image (in *R8* format) that defines the placement of meshes.
### Arguments

- *string* **image_name** - Name (path) of the mask image.
- *bool* **invalidate** - Invalidate flag. Set true to invalidate all cells of the *World Clutter*; otherwise, set false. All invalidated cells will be regenerated.

## string GetMaskImageName ( )

Returns the name of a mask image (in *R8* format) that defines the placement of reference nodes.
### Return value

Name (path) of the mask image.
## int SetMaskMesh ( Mesh mesh , bool invalidate = 1 )


Sets a mesh to be used as a mask on-the-fly. Limitations:


- Before the method is called, another mesh must be set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void) first.
- If the world is reloaded, the mesh set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void) will be loaded.
- If the memory limit is exceeded, the new mesh might be replaced with the mesh set via [setMaskMeshName()](#setMaskMeshName_cstr_int_void).


### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Mesh instance.
- *bool* **invalidate** - Invalidate flag. Set true to invalidate all cells of the *World Clutter*; otherwise, set false. All invalidated cells will be regenerated.

### Return value

**1** if the mesh is set successfully; otherwise - **0**.
## int GetMaskMesh ( Mesh mesh )

Copies the current mask mesh (if it exists) to the specified target mesh.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Mesh instance to copy the current mask mesh to.

### Return value

**1** if mesh mask exists; otherwise - **0**.
## void SetMaskMeshName ( string mesh_name , bool invalidate = 1 )

Sets a mesh to be used as a mask for the *World Clutter*. This mesh should be plane.
### Arguments

- *string* **mesh_name** - Path to the **.mesh* file.
- *bool* **invalidate** - Invalidate flag. Set true to invalidate all cells of the *World Clutter*; otherwise, set false. All invalidated cells will be regenerated.

## string GetMaskMeshName ( )

Returns the name (path) of the current mesh used as a mask for the *World Clutter*. This mesh should be plane.
### Return value

Path to the **.mesh* file.
## void SetMaxScale ( float mean , float spread )

Sets the scale for meshes in the areas with high density (according to the mask). With the minimum scale it is possible to automatically render, for example, big trees in the center of the forest. A spread value enables to control the range of scales relative to the mean value.
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
## void SetMinScale ( float mean , float spread )

Sets the scale for meshes in the areas with low density (according to the mask). With the minimum scale it is possible to automatically render, for example, small trees at the forest border. A spread value allows to control the range of scales relative to the mean value.
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
## void SetNodesRotation ( vec3 mean , vec3 spread )

Sets the rotation of reference nodes along X, Y and Z axes.
### Arguments

- *vec3* **mean** - Mean values of rotation angles in degrees.
- *vec3* **spread** - Spread values of rotation angles in degrees.

## vec3 GetNodesRotationMean ( )

Returns the mean value of reference nodes rotation along X, Y and Z axes.
### Return value

Mean values of rotation angles in degrees.
## vec3 GetNodesRotationSpread ( )

Returns the spread value of reference nodes rotation along X, Y and Z axes.
### Return value

Spread values of rotation angles in degrees.
## void SetOffset ( float mean , float spread )

Sets the vertical offset that determines the placement of reference nodes above or below the surface.
### Arguments

- *float* **mean** - Mean value of the offset in units.
- *float* **spread** - Spread value of the offset in units.

## float GetOffsetMean ( )

Returns the current mean value of the vertical offset that determines the placement of reference nodes above or below the surface.
### Return value

Mean value of the offset in units.
## float GetOffsetSpread ( )

Returns the current spread value of the vertical offset that determines the placement of reference nodes above or below the surface.
### Return value

Spread value of the offset in units.
## void SetReferenceName ( int num , string name )

Sets the name of the specified reference node contained in the *World Clutter*.
### Arguments

- *int* **num** - The number of the reference node.
- *string* **name** - Name to be updated.

## string GetReferenceName ( int num )

Returns the name of the reference node contained in the *World Clutter*.
### Arguments

- *int* **num** - The number of the reference node among contained in the *World Clutter*.

### Return value

Name of the reference node.
## void SetReferenceProbability ( int num , float probability )

Sets the probability of the occurrence of the specified node reference.
### Arguments

- *int* **num** - The number of the reference node.
- *float* **probability** - Probability factor. The provided value is saturated in range [0.0f, 1.0f].

## float GetReferenceProbability ( int num )

Returns the probability of the occurrence of the specified node reference.
### Arguments

- *int* **num** - The number of the reference node.

### Return value

Probability factor.
## int AddReference ( string name )

Adds a new reference node to the *World Clutter*.
### Arguments

- *string* **name** - Name of the reference node.

### Return value

The number of added reference node.
## void RemoveReference ( int num )

Removes the specified reference node from the *World Clutter*.
### Arguments

- *int* **num** - The number of the reference node.

## static int type ( )

Returns the type of the node.
### Return value

[World](../../../api/library/engine/class.world_cs.md) type identifier.
## void ClearReferences ( )

Deletes all reference nodes from the *World Clutter*.
## bool SaveStateReferences ( Stream stream )

Saves the state of all reference nodes from the *World Clutter* to the specified stream.


**Example** using *saveStateReferences()* and *[restoreStateReferences()](#restoreStateReferences_Stream_int)* methods:


```csharp
// initialize a node and set its state
WorldClutter worldClutter = new WorldClutter();
worldClutter.SizeX = 500.0f;
worldClutter.SizeY = 500.0f;

// save state
Blob blob_state = new Blob();
worldClutter.SaveStateReferences(blob_state);

// change the node state
worldClutter.SizeY = 700.0f;

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
worldClutter.RestoreStateReferences(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream instance.

### Return value

true if the states of all reference nodes from the *World Clutter* were successfully saved to the specified stream; otherwise, false.
## bool RestoreStateReferences ( Stream stream )


Restores the state of all reference nodes from the *World Clutter* from the specified stream.


**Example** using *[saveStateReferences()](#saveStateReferences_Stream_int)* and *restoreStateReferences()* methods:


```csharp
// initialize a node and set its state
WorldClutter worldClutter = new WorldClutter();
worldClutter.SizeX = 500.0f;
worldClutter.SizeY = 500.0f;

// save state
Blob blob_state = new Blob();
worldClutter.SaveStateReferences(blob_state);

// change the node state
worldClutter.SizeY = 700.0f;

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
worldClutter.RestoreStateReferences(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream instance.

### Return value

true if the states of all reference nodes from the *World Clutter* were successfully restored from the specified stream; otherwise, false.
