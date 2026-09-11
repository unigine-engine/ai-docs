# ObjectVolumeSphere Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


This class is used to create a [volume sphere](../../../objects/effects/volumetrics/volume_sphere.md). Depending on the assigned material, it can be used to render [fog](../../../content/materials/library/volume_fog_base/index.md) or a visible volume of [light](../../../content/materials/library/volume_light_base/index.md) around a light source. A volume sphere can also be of an ellipsoid shape.


## ObjectVolumeSphere Class

### Members

## void setRadius ( vec3 radius )

Sets a new volume sphere radius values.
### Arguments

- *vec3* **radius** - The volume sphere radius values

## vec3 getRadius () const

Returns the current volume sphere radius values.
### Return value

Current volume sphere radius values
---

## static ObjectVolumeSphere ( vec3 radius )

Constructor. Creates a new volume sphere object with given radius values.
> **Notice:** If a [volume light](../../../content/materials/library/volume_light_base/index.md) material is assigned to an object, it is rendered based only on the X-axis radius value. If its radius values along Y or Z axes are smaller, then the object is cut along them.


### Arguments

- *vec3* **radius** - Radius values of the new volume sphere object in units. If a negative value is provided, **0** will be used instead.

## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_usc.md) type identifier.
