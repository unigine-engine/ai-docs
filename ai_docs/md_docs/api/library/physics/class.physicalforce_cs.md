# Unigine.PhysicalForce Class (CS)

**Inherits from:** Physical


This class is used to simulate a point force that pulls physical bodies [up to or away from](#setAttractor_float_void) the point.  It can also [rotate](#setRotator_float_void) them around the force center.


> **Notice:** The physical force can affect only a [*cloth*](../../../api/library/physics/class.bodycloth_cs.md), a [*rope*](../../../api/library/physics/class.bodyrope_cs.md) or a [*rigid*](../../../api/library/physics/class.bodyrigid_cs.md) body. If the rigid body is used, a [shape](../../../api/library/physics/shapes_cs.md) should be also assigned.


### See also


- Article on *[Physical Force](../../../objects/effects/physicals/physical_force/index.md)*
- UnigineScript samples:

  -
  -


## PhysicalForce Class

### Properties

## float Rotator

The rotation force that will be applied to objects in the physical force radius.
## float Radius

The radius set for applying the physical force.
## float Attractor

The attraction force applied to objects in the physical force radius. positive values pull objects away from the force point, negative values pull them up to it.
## float Attenuation

The attenuation factor for the physical force.
### Members

---

## PhysicalForce ( float radius )

Constructor. Creates a physical force node with the specified radius in units.
### Arguments

- *float* **radius** - The radius of the physical force node in units.

## static int type ( )

Returns the type of the node.
### Return value

[Physical](../../../api/library/physics/class.physical_cs.md) type identifier.
