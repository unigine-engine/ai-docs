# Unigine.PhysicalWind Class (CS)

**Inherits from:** Physical


A *PhysicalWind* class is used to simulate a box-shaped area inside of which the wind is [blowing](#setVelocity_vec3_void). The wind [gradually decreases](#setThreshold_vec3_void) up to the box boundaries.


> **Notice:** A physical wind will affect only an object that meets the following requirements:
> - The object's bounds must be inside the physical wind box.
> - A [*cloth body*](../../../api/library/physics/class.bodycloth_cs.md) or a [*rigid body*](../../../api/library/physics/class.bodyrigid_cs.md) must be assigned to the object. If the rigid body is used, a [shape](../../../api/library/physics/shapes_cs.md) should be also assigned.


### See Also


- Article on *[Physical Wind](../../../objects/effects/physicals/physical_wind/index.md)*
- UnigineScript samples:

  -
  -
  -
  -
  -
  -


## PhysicalWind Class

### Properties

## vec3 Velocity

The velocity of the physical wind flow along the axes.
## vec3 Threshold

The threshold distance values along the coordinates axes relative to the wind node size (that is, inside of it). It determines the area of gradual change from zero to full wind velocity. See also [setThreshold()](#setThreshold_vec3_void).
## vec3 Size

The size of the physical wind node.
## float LinearDamping

The value indicating how much the linear velocity of the objects decreases when they get inside the wind node.
## float AngularDamping

The value indicating how much the angular velocity of the objects decreases when they get inside the physical wind node.
### Members

---

## PhysicalWind ( vec3 size )

Constructor. Creates a physical wind node of the specified size.
### Arguments

- *vec3* **size** - Wind box size in units.

## static int type ( )

Returns the type of the node.
### Return value

[Physical](../../../api/library/physics/class.physical_cs.md) type identifier.
