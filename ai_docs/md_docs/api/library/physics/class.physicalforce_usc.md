# Unigine.PhysicalForce Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Physical


This class is used to simulate a point force that pulls physical bodies [up to or away from](#setAttractor_float_void) the point.  It can also [rotate](#setRotator_float_void) them around the force center.


> **Notice:** The physical force can affect only a [*cloth*](../../../api/library/physics/class.bodycloth_usc.md), a [*rope*](../../../api/library/physics/class.bodyrope_usc.md) or a [*rigid*](../../../api/library/physics/class.bodyrigid_usc.md) body. If the rigid body is used, a [shape](../../../api/library/physics/shapes_usc.md) should be also assigned.


### See also


- Article on *[Physical Force](../../../objects/effects/physicals/physical_force/index.md)*
- UnigineScript samples:

  -
  -


## PhysicalForce Class

### Members

## void setRotator ( float rotator )

Sets a new rotation force that will be applied to objects in the physical force radius.
### Arguments

- *float* **rotator** - The rotation force applied to objects in the radius

## float getRotator () const

Returns the current rotation force that will be applied to objects in the physical force radius.
### Return value

Current rotation force applied to objects in the radius
## void setRadius ( float radius )

Sets a new radius set for applying the physical force.
### Arguments

- *float* **radius** - The radius for applying the physical force

## float getRadius () const

Returns the current radius set for applying the physical force.
### Return value

Current radius for applying the physical force
## void setAttractor ( float attractor )

Sets a new attraction force applied to objects in the physical force radius. positive values pull objects away from the force point, negative values pull them up to it.
### Arguments

- *float* **attractor** - The attraction force applied to objects in the radius

## float getAttractor () const

Returns the current attraction force applied to objects in the physical force radius. positive values pull objects away from the force point, negative values pull them up to it.
### Return value

Current attraction force applied to objects in the radius
## void setAttenuation ( float attenuation )

Sets a new attenuation factor for the physical force.
### Arguments

- *float* **attenuation** - The attenuation factor for the physical force

## float getAttenuation () const

Returns the current attenuation factor for the physical force.
### Return value

Current attenuation factor for the physical force
---

## static PhysicalForce ( float radius )

Constructor. Creates a physical force node with the specified radius in units.
### Arguments

- *float* **radius** - The radius of the physical force node in units.

## static int type ( )

Returns the type of the node.
### Return value

[Physical](../../../api/library/physics/class.physical_usc.md) type identifier.
