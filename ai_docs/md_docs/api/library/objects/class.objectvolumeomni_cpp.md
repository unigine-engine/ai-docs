# ObjectVolumeOmni Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


This class is used to create a [volume omni](../../../objects/effects/volumetrics/volume_omni.md) object. It simulates a visible volume of light emitted from a flat light source.


The volume omni object is rendered as a flat rectangle and billboards around its edges. The rectangle simulates a light emitting surface and billboards create a light volume around it.


## ObjectVolumeOmni Class

### Members

## void setAttenuation ( float attenuation )

Sets a new Attenuation that modulates smooth fading of the volume omni object when the camera looks at it from a side. If a too small value is provided, 1E-6 will be used instead.
### Arguments

- *float* **attenuation** - The Attenuation that modulates smooth fading of the volume omni object when the camera looks at it from a side

## float getAttenuation () const

Returns the current Attenuation that modulates smooth fading of the volume omni object when the camera looks at it from a side. If a too small value is provided, 1E-6 will be used instead.
### Return value

Current Attenuation that modulates smooth fading of the volume omni object when the camera looks at it from a side
## void setRadius ( float radius )

Sets a new size of billboards.
### Arguments

- *float* **radius** - The size of billboards

## float getRadius () const

Returns the current size of billboards.
### Return value

Current size of billboards
## float getHeight () const

Returns the current height of the central flat rectangle in units.
### Return value

Current height of the central flat rectangle in units
## float getWidth () const

Returns the current width of the central flat rectangle.
### Return value

Current width of the central flat rectangle
---

## static ObjectVolumeOmniPtr create ( float width , float height , float radius )

Constructor. Creates a new volume omni object with given properties.
### Arguments

- *float* **width** - Width of the central rectangle in units.
- *float* **height** - Height of the central rectangle in units.
- *float* **radius** - Size of billboards in units.

## void setSize ( float width , float height )

Sets new dimensions of the volume omni object.
### Arguments

- *float* **width** - A new width of the central flat rectangle in units. If a negative value is provided, 0 will be used instead.
- *float* **height** - A new height of the central flat rectangle in units. If a negative value is provided, 0 will be used instead.

## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cpp.md) type identifier.
