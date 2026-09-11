# ObjectVolumeBox Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


This class is used to create a [volume box](../../../objects/effects/volumetrics/volume_box.md). Depending on the assigned material, it can be used to render [fog](../../../content/materials/library/volume_fog_base/index.md), [light shafts](../../../content/materials/library/volume_shaft_base/index.md) from a world light source or [clouds](../../../content/materials/library/volume_cloud_base/index.md).


## ObjectVolumeBox Class

### Members

## void setSize ( const Math:: vec3 & size )

Sets a new dimensions of the volume box, in units. If a negative value is provided, 0 will be used instead.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The dimensions of the volume box

## Math:: vec3 getSize () const

Returns the current dimensions of the volume box, in units. If a negative value is provided, 0 will be used instead.
### Return value

Current dimensions of the volume box
---

## static ObjectVolumeBoxPtr create ( const Math:: vec3 & size )

Constructor. Creates a new volume box object with given dimensions.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Dimensions of the new volume box object in units.

## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cpp.md) type identifier.
