# Unigine.PhysicalWind Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Physical


A *PhysicalWind* class is used to simulate a box-shaped area inside of which the wind is [blowing](#setVelocity_vec3_void). The wind [gradually decreases](#setThreshold_vec3_void) up to the box boundaries.


> **Notice:** A physical wind will affect only an object that meets the following requirements:
> - The object's bounds must be inside the physical wind box.
> - A [*cloth body*](../../../api/library/physics/class.bodycloth_usc.md) or a [*rigid body*](../../../api/library/physics/class.bodyrigid_usc.md) must be assigned to the object. If the rigid body is used, a [shape](../../../api/library/physics/shapes_usc.md) should be also assigned.


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

## void setVelocity ( vec3 velocity )

Sets a new velocity of the physical wind flow along the axes.
### Arguments

- *vec3* **velocity** - The velocity of the physical wind flow

## vec3 getVelocity () const

Returns the current velocity of the physical wind flow along the axes.
### Return value

Current velocity of the physical wind flow
## void setThreshold ( vec3 threshold )

Sets a new threshold distance values along the coordinates axes relative to the wind node size (that is, inside of it). It determines the area of gradual change from zero to full wind velocity. See also [setThreshold()](#setThreshold_vec3_void).
### Arguments

- *vec3* **threshold** - The threshold distance values relative to the wind node size

## vec3 getThreshold () const

Returns the current threshold distance values along the coordinates axes relative to the wind node size (that is, inside of it). It determines the area of gradual change from zero to full wind velocity. See also [setThreshold()](#setThreshold_vec3_void).
### Return value

Current threshold distance values relative to the wind node size
## void setSize ( vec3 size )

Sets a new size of the physical wind node.
### Arguments

- *vec3* **size** - The size of the physical wind node

## vec3 getSize () const

Returns the current size of the physical wind node.
### Return value

Current size of the physical wind node
## void setLinearDamping ( float damping )

Sets a new value indicating how much the linear velocity of the objects decreases when they get inside the wind node.
### Arguments

- *float* **damping** - The damping of the objects linear velocity in the wind

## float getLinearDamping () const

Returns the current value indicating how much the linear velocity of the objects decreases when they get inside the wind node.
### Return value

Current damping of the objects linear velocity in the wind
## void setAngularDamping ( float damping )

Sets a new value indicating how much the angular velocity of the objects decreases when they get inside the physical wind node.
### Arguments

- *float* **damping** - The damping of the objects angular velocity in the wind

## float getAngularDamping () const

Returns the current value indicating how much the angular velocity of the objects decreases when they get inside the physical wind node.
### Return value

Current damping of the objects angular velocity in the wind
---

## static PhysicalWind ( vec3 size )

Constructor. Creates a physical wind node of the specified size.
### Arguments

- *vec3* **size** - Wind box size in units.

## static int type ( )

Returns the type of the node.
### Return value

[Physical](../../../api/library/physics/class.physical_usc.md) type identifier.
