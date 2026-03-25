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

---

## static PhysicalForce ( float radius )

Constructor. Creates a physical force node with the specified radius in units.
### Arguments

- *float* **radius** - The radius of the physical force node in units.

## void setAttenuation ( float attenuation )

Updates the attenuation factor for the physical force.
### Arguments

- *float* **attenuation** - Attenuation factor.

## float getAttenuation ( )

Returns the current attenuation factor for the physical force.
### Return value

Attenuation factor.
## void setAttractor ( float attractor )

Updates attraction force that will be applied to objects in the physical force radius.
### Arguments

- *float* **attractor** - Attraction force value. If a positive value is specified, objects will be pulled away from the force point. If a negative value is specified, objects will be pulled up to the force center.

## float getAttractor ( )

 Returns the current attraction force applied to objects in the physical force radius.  Positive values pull objects away from the force point, negative values pull them up to it.
### Return value

Attraction force value.
## void setRadius ( float radius )

Updates the radius for applying the physical force.
### Arguments

- *float* **radius** - Radius in units. If a negative value is provided, **0** will be used instead.

## float getRadius ( )

Returns the current radius set for applying the physical force.
### Return value

Radius in units.
## void setRotator ( float rotator )

Updates rotation force that will be applied to objects in the physical force radius.
### Arguments

- *float* **rotator** - Rotation force value. If a positive value is specified, object will be rotated *clockwise*. If a negative value is specified, objects will be rotated *counterclockwise*.

## float getRotator ( )

Returns the current rotation force that will be applied to objects in the physical force radius.  Positive values rotate objects *clockwise*, negative values rotate them *counterclockwise*.
### Return value

Rotation force value.
## static int type ( )

Returns the type of the node.
### Return value

[Physical](../../../api/library/physics/class.physical_usc.md) type identifier.
