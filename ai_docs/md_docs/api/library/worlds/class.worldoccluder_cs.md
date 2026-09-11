# Unigine.WorldOccluder Class (CS)

**Inherits from:** Node


This class is used to create a box-shaped occluder that culls surfaces, bounds of which are currently hidden behind it. If any part of the bound of the object's surface is visible behind the occluder, the surface will not be culled. The objects' surfaces behind the occluder are not sent to the GPU, thereby saving performance.


The occluder itself is rendered by the CPU and stored in a separate buffer.


> **Notice:** The front or back faces of the occluder are used to cull surfaces. See details [here](../../../objects/worlds/world_occluders/occluder_object/index.md).


#### Usage


In order to enhance performance, occluders should be used wisely. The following notes will help you to decide whether to use the occluder or not:


- Occluders can be highly effective in case of complex environments where there are many objects that occlude each other and are costly to render (they have a lot of polygons and/or heavy shaders).
- Effective culling is possible if objects are not too large, since if any part of their surface is seen, it cannot be culled. In case objects are big and have a few surfaces, it is likely that an additional performance load of an occluder will not pay off.
- In case the scene is filled with flat objects or a camera looks down on the scene from above (for example, in flight simulators), it is better not to use occluders at all or disable them.


#### See Also


- Article on [Occluders](../../../objects/worlds/world_occluders/index.md) for general information
- Article on the *[Occluder](../../../objects/worlds/world_occluders/occluder_object/index.md)* node
- UnigineScript samples:

  -
  -


## WorldOccluder Class

### Properties

## float Distance

The distance between the camera and the bounding box of the occluder, at which the occluder becomes disabled (it isn't processed by the CPU, hence it isn't rendered). By default, the inf value is used.
## vec3 Size

The dimensions of the world occluder box.
## bool BackFace

The value indicating whether the back faces of the occluder box are used instead of front faces to occlude objects' surfaces. by default, the front faces are used.
### Members

---

## WorldOccluder ( vec3 size )

Constructor. Creates a new world occluder with given dimensions.
### Arguments

- *vec3* **size** - Size of the new occluder.

## static int type ( )

Returns the type of the node.
### Return value

[World](../../../api/library/engine/class.world_cs.md) type identifier.
