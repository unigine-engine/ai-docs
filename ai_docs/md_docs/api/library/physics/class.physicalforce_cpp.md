# Unigine.PhysicalForce Class (CPP)

**Header:** #include <UniginePhysicals.h>

**Inherits from:** Physical


This class is used to simulate a point force that pulls physical bodies [up to or away from](#setAttractor_float_void) the point.  It can also [rotate](#setRotator_float_void) them around the force center.


> **Notice:** The physical force can affect only a [*cloth*](../../../api/library/physics/class.bodycloth_cpp.md), a [*rope*](../../../api/library/physics/class.bodyrope_cpp.md) or a [*rigid*](../../../api/library/physics/class.bodyrigid_cpp.md) body. If the rigid body is used, a [shape](../../../api/library/physics/shapes_cpp.md) should be also assigned.


### See also


- Article on *[Physical Force](../../../objects/effects/physicals/physical_force/index.md)*
- UnigineScript samples:

  -
  -


## PhysicalForce Class

### Members

---

## static PhysicalForcePtr create ( float radius )

Constructor. Creates a physical force node with the specified radius in units.
### Arguments

- *float* **radius** - The radius of the physical force node in units.

## void setAttenuation ( float attenuation )

Updates the attenuation factor for the physical force.
### Arguments

- *float* **attenuation** - A new attenuation factor.

## float getAttenuation ( )

Returns the current attenuation factor for the physical force.
### Return value

The attenuation factor.
## void setAttractor ( float attractor )

Updates the attraction force that will be applied to objects in the physical force radius.
### Arguments

- *float* **attractor** - A new attraction force value. Positive values pull objects away from the force point, negative values pull them up to it.

## float getAttractor ( )

Returns the current attraction force applied to objects in the physical force radius. Positive values pull objects away from the force point, negative values pull them up to it.
### Return value

The attraction force value.
## void setRadius ( float radius )

Updates the radius for applying the physical force.
### Arguments

- *float* **radius** - A new radius in units. If a negative value is provided, 0 will be used instead.

## float getRadius ( )

Returns the current radius set for applying the physical force.
### Return value

The radius in units.
## void setRotator ( float rotator )

Updates the rotation force that will be applied to objects in the physical force radius.
### Arguments

- *float* **rotator** - A new rotation force value. Set a positive value for clockwise rotation or a negative value for counterclockwise one.

## float getRotator ( )

Returns the current rotation force that will be applied to objects in the physical force radius.
### Return value

The rotation force value.
## static int type ( )

Returns the type of the node.
### Return value

[Physical](../../../api/library/physics/class.physical_cpp.md) type identifier.
