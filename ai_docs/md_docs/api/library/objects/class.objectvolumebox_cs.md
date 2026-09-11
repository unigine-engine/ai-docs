# ObjectVolumeBox Class (CS)

**Inherits from:** Object


This class is used to create a [volume box](../../../objects/effects/volumetrics/volume_box.md). Depending on the assigned material, it can be used to render [fog](../../../content/materials/library/volume_fog_base/index.md), [light shafts](../../../content/materials/library/volume_shaft_base/index.md) from a world light source or [clouds](../../../content/materials/library/volume_cloud_base/index.md).


## ObjectVolumeBox Class

### Properties

## vec3 Size

The dimensions of the volume box, in units. If a negative value is provided, 0 will be used instead.
### Members

---

## ObjectVolumeBox ( vec3 size )

Constructor. Creates a new volume box object with given dimensions.
### Arguments

- *vec3* **size** - Dimensions of the new volume box object in units.

## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cs.md) type identifier.
