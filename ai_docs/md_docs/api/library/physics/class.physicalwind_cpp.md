# Unigine.PhysicalWind Class (CPP)

**Header:** #include <UniginePhysicals.h>

**Inherits from:** Physical


A *PhysicalWind* class is used to simulate a box-shaped area inside of which the wind is [blowing](#setVelocity_vec3_void). The wind [gradually decreases](#setThreshold_vec3_void) up to the box boundaries.


> **Notice:** A physical wind will affect only an object that meets the following requirements:
> - The object's bounds must be inside the physical wind box.
> - A [*cloth body*](../../../api/library/physics/class.bodycloth_cpp.md) or a [*rigid body*](../../../api/library/physics/class.bodyrigid_cpp.md) must be assigned to the object. If the rigid body is used, a [shape](../../../api/library/physics/shapes_cpp.md) should be also assigned.


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

### Members

---

## static PhysicalWindPtr create ( const Math:: vec3 & size )

Constructor. Creates a physical wind node of the specified size.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Wind box size in units.

## void setAngularDamping ( float damping )

Sets a value indicating how much the angular velocity of the objects decreases when they get inside the wind node.
### Arguments

- *float* **damping** - Angular damping value. If a negative value is provided, **0** will be used instead.

## float getAngularDamping ( )

Returns the current value indicating how much the angular velocity of the objects decreases when they get inside the physical wind node.
### Return value

Angular damping value.
## void setLinearDamping ( float damping )

Sets a value indicating how much the linear velocity of the objects decreases when they get inside the wind node.
### Arguments

- *float* **damping** - Linear damping value. If a negative value is provided, 0 will be used instead.

## float getLinearDamping ( )

Returns the current value indicating how much the linear velocity of the objects decreases when they get inside the wind node.
### Return value

Linear damping value.
## void setSize ( const Math:: vec3 & size )

Sets the size of the physical wind node.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Wind box size in units.

## Math:: vec3 getSize ( )

Returns the current size of the physical wind node.
### Return value

Wind box size in units.
## void setThreshold ( const Math:: vec3 & threshold )

Sets the threshold distance values along the coordinates axes relative to the wind node [size](#setSize_vec3_void) (that is, inside of it). It determines the area of gradual change from zero to full wind [velocity](#setVelocity_vec3_void).
The threshold distance values form an invisible box, inside which the wind blows with full velocity:


![](../../../objects/effects/physicals/threshold.png)


### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **threshold** - Threshold distance in units.

## Math:: vec3 getThreshold ( )

Returns the current threshold distance values along the coordinates axes relative to the wind node [size](#setSize_vec3_void) (that is, inside of it). It determines the area of gradual change from zero to full wind [velocity](#setVelocity_vec3_void). See also [*setThreshold()*](#setThreshold_vec3_void).
### Return value

Threshold distance in units.
## void setVelocity ( const Math:: vec3 & velocity )

Sets the velocity of the physical wind flow along the axes.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **velocity** - Velocity in units per second.

## Math:: vec3 getVelocity ( )

Returns the current velocity of the physical wind flow along the axes.
### Return value

Velocity in units per second.
## static int type ( )

Returns the type of the node.
### Return value

[Physical](../../../api/library/physics/class.physical_cpp.md) type identifier.
