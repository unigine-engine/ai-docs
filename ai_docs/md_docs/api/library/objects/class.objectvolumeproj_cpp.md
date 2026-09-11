# ObjectVolumeProj Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


This class is used to create a [volume projected](../../../objects/effects/volumetrics/volume_proj.md) object that simulates a light beam from a directional light source. It can be animated to create a flow of particles moving to the end of the beam and rotating, if necessary.


Projected volume object is rendered as a number of billboards, where each following billboard is bigger than the previous one.


## ObjectVolumeProj Class

### Members

## void setVolumeRotation ( float rotation )

Sets a new angle of billboards rotation. this angle is set for the billboard at the end of the beam. if a positive value is set, the billboards will be rotated clockwise; if a negative value is set, the billboards will be rotated counterclockwise.
### Arguments

- *float* **rotation** - The angle of billboards rotation

## float getVolumeRotation () const

Returns the current angle of billboards rotation. this angle is set for the billboard at the end of the beam. if a positive value is set, the billboards will be rotated clockwise; if a negative value is set, the billboards will be rotated counterclockwise.
### Return value

Current angle of billboards rotation
## void setVelocity ( float velocity )

Sets a new velocity with which billboards move to the end of the light beam.
### Arguments

- *float* **velocity** - The velocity with which billboards move to the end of the light beam

## float getVelocity () const

Returns the current velocity with which billboards move to the end of the light beam.
### Return value

Current velocity with which billboards move to the end of the light beam
## void setStep ( float step )

Sets a new distance between neighboring billboards. the step controls how many billboards are used to render the volume projected object. the bigger the step, the less billboards are used to render the object. The provided value will be saturated in the range [0.1; 1]. By the value of 1, the beam is rendered discrete.
### Arguments

- *float* **step** - The distance between neighboring billboards

## float getStep () const

Returns the current distance between neighboring billboards. the step controls how many billboards are used to render the volume projected object. the bigger the step, the less billboards are used to render the object. The provided value will be saturated in the range [0.1; 1]. By the value of 1, the beam is rendered discrete.
### Return value

Current distance between neighboring billboards
## void setFov ( float fov )

Sets a new width of the light beam, which is specified as the angle of the beam cone, in degrees. The provided value will be saturated in the range [10;90].
### Arguments

- *float* **fov** - The width of the light beam, which is specified as the angle of the beam cone

## float getFov () const

Returns the current width of the light beam, which is specified as the angle of the beam cone, in degrees. The provided value will be saturated in the range [10;90].
### Return value

Current width of the light beam, which is specified as the angle of the beam cone
## void setRadius ( float radius )

Sets a new length of the light beam along the z axis in units.
### Arguments

- *float* **radius** - The length of the light beam along the z axis in units

## float getRadius () const

Returns the current length of the light beam along the z axis in units.
### Return value

Current length of the light beam along the z axis in units
## void setSize ( float size )

Sets a new size of the smallest billboard at the beginning of the light beam, in units. If a too small value is provided, 0.001 will be used instead.
### Arguments

- *float* **size** - The size of the smallest billboard at the beginning of the light beam

## float getSize () const

Returns the current size of the smallest billboard at the beginning of the light beam, in units. If a too small value is provided, 0.001 will be used instead.
### Return value

Current size of the smallest billboard at the beginning of the light beam
---

## static ObjectVolumeProjPtr create ( float width , float height , float fov )

Constructor. Creates a new volume projected object with the given properties.
### Arguments

- *float* **width** - Size of the smallest billboard in units.
- *float* **height** - Length of the light beam along the Z axis in units.
- *float* **fov** - Angle of the beam cone in degrees. It controls the width of the light beam.

## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cpp.md) type identifier.
