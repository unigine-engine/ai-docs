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

---

## static PhysicalWaterPtr create ( const Math:: vec3 & size )

Constructor. Creates a physical water node of the specified size.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Water box size in units.

## void setAngularDamping ( float damping )

Sets a value indicating how much the angular velocity of the objects decreases when they get into the physical water.
### Arguments

- *float* **damping** - An angular damping value. If a negative value is provided, 0 will be used instead.

## float getAngularDamping ( )

Returns the current value indicating how much the angular velocity of the objects decreases when they get into the physical water.
### Return value

The angular damping value.
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
## void setDensity ( float density )

Sets a density of the water that determines objects buoyancy.
### Arguments

- *float* **density** - A density value. If a negative value is provided, 0 will be used instead.

## float getDensity ( )

Returns the current density of the physical water that determines objects buoyancy.
### Return value

The density value.
## void setLinearDamping ( float damping )

Sets a value indicating how much the linear velocity of the objects decreases when they get into the physical water.
### Arguments

- *float* **damping** - A linear damping value. If a negative value is provided, 0 will be used instead.

## float getLinearDamping ( )

Returns the current value indicating how much the linear velocity of the objects decreases when they get into the physical water.
### Return value

The linear damping value.
## int getNumContacts ( )

Returns the number of contacts between the physical water and the objects.
### Return value

Number of contacts.
## void setSize ( const Math:: vec3 & size )

Sets a size of the physical water node.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - A size of the water box in units. If a negative value is provided, 0 will be used instead.

## Math:: vec3 getSize ( )

Returns the current size of the physical water node.
### Return value

The size of the water box in units.
## void setVelocity ( const Math:: vec3 & velocity )

Sets a velocity of the flow in physical water.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **velocity** - A velocity in units per second.

## Math:: vec3 getVelocity ( )

Returns the current velocity of the flow in physical water.
### Return value

The velocity in units per second.
## static int type ( )

Returns the type of the node.
### Return value

[Physical](../../../api/library/physics/class.physical_cpp.md) type identifier.
