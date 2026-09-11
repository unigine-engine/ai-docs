# ObjectVolumeSphere Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


This class is used to create a [volume sphere](../../../objects/effects/volumetrics/volume_sphere.md). Depending on the assigned material, it can be used to render [fog](../../../content/materials/library/volume_fog_base/index.md) or a visible volume of [light](../../../content/materials/library/volume_light_base/index.md) around a light source. A volume sphere can also be of an ellipsoid shape.


## ObjectVolumeSphere Class

### Members

## void setRadius ( const Math:: vec3 & radius )

Sets a new volume sphere radius values.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **radius** - The volume sphere radius values

## Math:: vec3 getRadius () const

Returns the current volume sphere radius values.
### Return value

Current volume sphere radius values
---

## static ObjectVolumeSpherePtr create ( const Math:: vec3 & radius )

Constructor. Creates a new volume sphere object with given radius values.
> **Notice:** If a [volume light](../../../content/materials/library/volume_light_base/index.md) material is assigned to an object, it is rendered based only on the X-axis radius value. If its radius values along Y or Z axes are smaller, then the object is cut along them.


### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **radius** - Radius values of the new volume sphere object in units. If a negative value is provided, **0** will be used instead.

## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cpp.md) type identifier.
