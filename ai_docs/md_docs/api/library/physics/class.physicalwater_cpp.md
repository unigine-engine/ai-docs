# Unigine.PhysicalWater Class (CPP)

**Header:** #include <UniginePhysicals.h>

**Inherits from:** Physical


A *PhysicalWater* class is used to simulate water interaction effects.


> **Notice:** The water will affect only objects, to which a [*cloth body*](../../../api/library/physics/class.bodycloth_cpp.md) or a [*rigid body*](../../../api/library/physics/class.bodyrigid_cpp.md) are assigned. If the rigid body is used, a [shape](../../../api/library/physics/shapes_cpp.md) should be also assigned.


### See Also


- Article on *[Physical Water](../../../objects/effects/physicals/physical_water/index.md)*
- UnigineScript samples:

  -
  -


## PhysicalWater Class

### Members

## void setVelocity ( const Math:: vec3 & velocity )

Sets a new velocity of the flow in physical water.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **velocity** - The velocity of the flow in physical water

## Math:: vec3 getVelocity () const

Returns the current velocity of the flow in physical water.
### Return value

Current velocity of the flow in physical water
## void setSize ( const Math:: vec3 & size )

Sets a new size of the physical water node.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The size of the physical water node

## Math:: vec3 getSize () const

Returns the current size of the physical water node.
### Return value

Current size of the physical water node
## int getNumContacts () const

Returns the current number of contacts between the physical water and the objects.
### Return value

Current number of contacts with objects
## void setLinearDamping ( float damping )

Sets a new value indicating how much the linear velocity of the objects decreases when they get into the physical water.
### Arguments

- *float* **damping** - The damping of the objects linear velocity in the water

## float getLinearDamping () const

Returns the current value indicating how much the linear velocity of the objects decreases when they get into the physical water.
### Return value

Current damping of the objects linear velocity in the water
## void setDensity ( float density )

Sets a new density of the physical water that determines objects buoyancy.
### Arguments

- *float* **density** - The density of the physical water

## float getDensity () const

Returns the current density of the physical water that determines objects buoyancy.
### Return value

Current density of the physical water
## void setAngularDamping ( float damping )

Sets a new value indicating how much the angular velocity of the objects decreases when they get into the physical water.
### Arguments

- *float* **damping** - The damping of the objects angular velocity in the water

## float getAngularDamping () const

Returns the current value indicating how much the angular velocity of the objects decreases when they get into the physical water.
### Return value

Current damping of the objects angular velocity in the water
---

## static PhysicalWaterPtr create ( const Math:: vec3 & size )

Constructor. Creates a physical water node of the specified size.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Water box size in units.

## Ptr < Body > getContactBody ( int num )

Returns the body of the object by the given contact with physical water.
### Arguments

- *int* **num** - Contact number.

### Return value

Body of the object.
## float getContactDepth ( int num )

Returns the depth of the object submergence by the given contact.
### Arguments

- *int* **num** - Contact number.

### Return value

Depth of object submergence in units.
## Math:: vec3 getContactForce ( int num )

Returns the force in the point of a given contact.
### Arguments

- *int* **num** - Contact number.

### Return value

Force value.
## Math:: Vec3 getContactPoint ( int num )

Returns the coordinates of the contact point.
### Arguments

- *int* **num** - Contact number.

### Return value

Contact point coordinates.
## Math:: vec3 getContactVelocity ( int num )

Returns the relative velocity between the object and the physical water.
### Arguments

- *int* **num** - Contact number.

### Return value

Relative velocity in units per second.
## static int type ( )

Returns the type of the node.
### Return value

[Physical](../../../api/library/physics/class.physical_cpp.md) type identifier.
