# ObjectVolumeOmni Class (CS)

**Inherits from:** Object


This class is used to create a [volume omni](../../../objects/effects/volumetrics/volume_omni.md) object. It simulates a visible volume of light emitted from a flat light source.


The volume omni object is rendered as a flat rectangle and billboards around its edges. The rectangle simulates a light emitting surface and billboards create a light volume around it.


## ObjectVolumeOmni Class

### Properties

## float Attenuation

The Attenuation that modulates smooth fading of the volume omni object when the camera looks at it from a side. If a too small value is provided, 1E-6 will be used instead.
## float Radius

The size of billboards.
## 🔒︎ float Height

The height of the central flat rectangle in units.
## 🔒︎ float Width

The width of the central flat rectangle.
### Members

---

## ObjectVolumeOmni ( float width , float height , float radius )

Constructor. Creates a new volume omni object with given properties.
### Arguments

- *float* **width** - Width of the central rectangle in units.
- *float* **height** - Height of the central rectangle in units.
- *float* **radius** - Size of billboards in units.

## void SetSize ( float width , float height )

Sets new dimensions of the volume omni object.
### Arguments

- *float* **width** - New width of the central rectangle in units. If a negative value is provided, **0** will be used instead.
- *float* **height** - New height of the central rectangle in units. If a negative value is provided, **0** will be used instead.

## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cs.md) type identifier.
