# ObjectVolumeProj Class (CS)

**Inherits from:** Object


This class is used to create a [volume projected](../../../objects/effects/volumetrics/volume_proj.md) object that simulates a light beam from a directional light source. It can be animated to create a flow of particles moving to the end of the beam and rotating, if necessary.


Projected volume object is rendered as a number of billboards, where each following billboard is bigger than the previous one.


## ObjectVolumeProj Class

### Properties

## float VolumeRotation

The angle of billboards rotation. this angle is set for the billboard at the end of the beam. if a positive value is set, the billboards will be rotated clockwise; if a negative value is set, the billboards will be rotated counterclockwise.
## float Velocity

The velocity with which billboards move to the end of the light beam.
## float Step

The distance between neighboring billboards. the step controls how many billboards are used to render the volume projected object. the bigger the step, the less billboards are used to render the object. The provided value will be saturated in the range [0.1; 1]. By the value of 1, the beam is rendered discrete.
## float Fov

The width of the light beam, which is specified as the angle of the beam cone, in degrees. The provided value will be saturated in the range [10;90].
## float Radius

The length of the light beam along the z axis in units.
## float Size

The size of the smallest billboard at the beginning of the light beam, in units. If a too small value is provided, 0.001 will be used instead.
### Members

---

## ObjectVolumeProj ( float width , float height , float fov )

Constructor. Creates a new volume projected object with the given properties.
### Arguments

- *float* **width** - Size of the smallest billboard in units.
- *float* **height** - Length of the light beam along the Z axis in units.
- *float* **fov** - Angle of the beam cone in degrees. It controls the width of the light beam.

## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cs.md) type identifier.
