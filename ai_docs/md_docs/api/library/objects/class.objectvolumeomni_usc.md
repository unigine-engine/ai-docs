# ObjectVolumeOmni Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


This class is used to create a [volume omni](../../../objects/effects/volumetrics/volume_omni.md) object. It simulates a visible volume of light emitted from a flat light source.


The volume omni object is rendered as a flat rectangle and billboards around its edges. The rectangle simulates a light emitting surface and billboards create a light volume around it.


## ObjectVolumeOmni Class

### Members

---

## static ObjectVolumeOmni ( float width , float height , float radius )

Constructor. Creates a new volume omni object with given properties.
### Arguments

- *float* **width** - Width of the central rectangle in units.
- *float* **height** - Height of the central rectangle in units.
- *float* **radius** - Size of billboards in units.

## void setAttenuation ( float attenuation )

Sets attenuation that controls how fast the volume omni object fades out when a camera looks at it from a side.
### Arguments

- *float* **attenuation** - An attenuation factor. If a too small value is provided, 1E-6 will be used instead.

## float getAttenuation ( )

Returns attenuation that modulates smooth fading of the volume omni object when the camera looks at it from a side.
### Return value

Attenuation factor.
## float getHeight ( )

Returns the height of the central rectangle in units.
### Return value

Height of the central rectangle in units.
## void setRadius ( float radius )

Sets the width of billboards at the edges.
### Arguments

- *float* **radius** - A new width in units. If a negative value is provided, 0 will be used instead.

## float getRadius ( )

Returns the size of billboards.
### Return value

Radius in units. If a negative value is provided, **0** will be used instead.
## void setSize ( float width , float height )

Sets new dimensions of the volume omni object.
### Arguments

- *float* **width** - New width of the central rectangle in units. If a negative value is provided, **0** will be used instead.
- *float* **height** - New height of the central rectangle in units. If a negative value is provided, **0** will be used instead.

## float getWidth ( )

Returns the width of the central rectangle.
### Return value

Width of the central rectangle in units.
## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_usc.md) type identifier.
