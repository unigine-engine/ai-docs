# Unigine.PhysicalWater Class (CS)

**Inherits from:** Physical


A *PhysicalWater* class is used to simulate water interaction effects.


> **Notice:** The water will affect only objects, to which a [*cloth body*](../../../api/library/physics/class.bodycloth_cs.md) or a [*rigid body*](../../../api/library/physics/class.bodyrigid_cs.md) are assigned. If the rigid body is used, a [shape](../../../api/library/physics/shapes_cs.md) should be also assigned.


### See Also


- Article on *[Physical Water](../../../objects/effects/physicals/physical_water/index.md)*
- UnigineScript samples:

  -
  -


## PhysicalWater Class

### Properties

## vec3 Velocity

The velocity of the flow in physical water.
## vec3 Size

The size of the physical water node.
## 🔒︎ int NumContacts

The number of contacts between the physical water and the objects.
## float LinearDamping

The value indicating how much the linear velocity of the objects decreases when they get into the physical water.
## float Density

The density of the physical water that determines objects buoyancy.
## float AngularDamping

The value indicating how much the angular velocity of the objects decreases when they get into the physical water.
### Members

---

## PhysicalWater ( vec3 size )

Constructor. Creates a physical water node of the specified size.
### Arguments

- *vec3* **size** - Water box size in units.

## Body GetContactBody ( int num )

Returns the body of the object by the given contact with physical water.
### Arguments

- *int* **num** - Contact number.

### Return value

Body of the object.
## float GetContactDepth ( int num )

Returns the depth of the object submergence by the given contact.
### Arguments

- *int* **num** - Contact number.

### Return value

Depth of object submergence in units.
## vec3 GetContactForce ( int num )

Returns the force in the point of a given contact.
### Arguments

- *int* **num** - Contact number.

### Return value

Force value.
## vec3 GetContactPoint ( int num )

Returns the coordinates of the contact point.
### Arguments

- *int* **num** - Contact number.

### Return value

Contact point coordinates.
## vec3 GetContactVelocity ( int num )

Returns the relative velocity between the object and the physical water.
### Arguments

- *int* **num** - Contact number.

### Return value

Relative velocity in units per second.
## static int type ( )

Returns the type of the node.
### Return value

[Physical](../../../api/library/physics/class.physical_cs.md) type identifier.
