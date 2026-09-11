# ObjectVolumeBox Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


This class is used to create a [volume box](../../../objects/effects/volumetrics/volume_box.md). Depending on the assigned material, it can be used to render [fog](../../../content/materials/library/volume_fog_base/index.md), [light shafts](../../../content/materials/library/volume_shaft_base/index.md) from a world light source or [clouds](../../../content/materials/library/volume_cloud_base/index.md).


## ObjectVolumeBox Class

### Members

## void setSize ( vec3 size )

Sets a new dimensions of the volume box, in units. If a negative value is provided, 0 will be used instead.
### Arguments

- *vec3* **size** - The dimensions of the volume box

## vec3 getSize () const

Returns the current dimensions of the volume box, in units. If a negative value is provided, 0 will be used instead.
### Return value

Current dimensions of the volume box
---

## static ObjectVolumeBox ( vec3 size )

Constructor. Creates a new volume box object with given dimensions.
### Arguments

- *vec3* **size** - Dimensions of the new volume box object in units.

## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_usc.md) type identifier.
