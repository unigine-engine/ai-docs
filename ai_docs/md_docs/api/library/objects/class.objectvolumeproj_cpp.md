# ObjectVolumeProj Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


This class is used to create a [volume projected](../../../objects/effects/volumetrics/volume_proj.md) object that simulates a light beam from a directional light source. It can be animated to create a flow of particles moving to the end of the beam and rotating, if necessary.


Projected volume object is rendered as a number of billboards, where each following billboard is bigger than the previous one.


## ObjectVolumeProj Class

### Members

---

## static ObjectVolumeProjPtr create ( float width , float height , float fov )

Constructor. Creates a new volume projected object with the given properties.
### Arguments

- *float* **width** - Size of the smallest billboard in units.
- *float* **height** - Length of the light beam along the Z axis in units.
- *float* **fov** - Angle of the beam cone in degrees. It controls the width of the light beam.

## void setFov ( float fov )

Sets the width of the light beam, which is specified as an angle of the beam cone.
### Arguments

- *float* **fov** - Angle in degrees. The provided value will be saturated in the range [10;90].

## float getFov ( ) const

Returns the width of the light beam, which is specified as the angle of the beam cone.
### Return value

Angle in degrees.
## void setRadius ( float radius )

Sets a length of the light beam.
### Arguments

- *float* **radius** - Length in units. If a negative value is provided, 0 will be used instead.

## float getRadius ( ) const

Returns the length of the light beam along the Z axis in units.
### Return value

The current length in units.
## void setSize ( float size )

Sets a size of the smallest billboard at the beginning of the light beam.
### Arguments

- *float* **size** - Size of the smallest billboard in units. If a too small value is provided, 0.001 will be used instead.

## float getSize ( ) const

Returns the size of the smallest billboard at the beginning of the light beam.
### Return value

Size of the smallest billboard in units.
## void setStep ( float step )

Sets a step between neighboring billboards. The step controls how many billboards are used to render the volume projected object. The bigger the step, the less billboards are used to render the object.
### Arguments

- *float* **step** - Step between billboards. The provided value will be saturated in the range [0.1; 1]. By the value of 1, the beam is rendered discrete.

## float getStep ( ) const

Returns the distance between neighboring billboards. The step controls how many billboards are used to render the volume projected object. The bigger the step, the less billboards are used to render the object.
### Return value

The step between billboards.
## void setVelocity ( float velocity )

Sets a velocity with which billboards move to the end of the light beam.
### Arguments

- *float* **velocity** - A velocity of billboards.

## float getVelocity ( ) const

Returns the velocity with which billboards move to the end of the light beam.
### Return value

The velocity of billboards.
## void setVolumeRotation ( float rotation )

Sets an angle of billboards rotation. This angle is set for the billboard at the end of the light beam.
### Arguments

- *float* **rotation** - A rotation angle. If a positive value is set, the billboards will be rotated clockwise; if a negative value is set, the billboards will be rotated counterclockwise.

## float getVolumeRotation ( ) const

Returns the angle of billboards rotation. This angle is set for the billboard at the end of the beam. If a positive value is set, the billboards will be rotated clockwise; if a negative value is set, the billboards will be rotated counterclockwise.
### Return value

The rotation angle.
## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cpp.md) type identifier.
