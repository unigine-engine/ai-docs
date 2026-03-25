# Unigine.PhysicalWater Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Physical


A *PhysicalWater* class is used to simulate water interaction effects.


> **Notice:** The water will affect only objects, to which a [*cloth body*](../../../api/library/physics/class.bodycloth_usc.md) or a [*rigid body*](../../../api/library/physics/class.bodyrigid_usc.md) are assigned. If the rigid body is used, a [shape](../../../api/library/physics/shapes_usc.md) should be also assigned.


### See Also


- Article on *[Physical Water](../../../objects/effects/physicals/physical_water/index.md)*
- UnigineScript samples:

  -
  -


## PhysicalWater Class

### Members

---

## static PhysicalWater ( vec3 size )

Constructor. Creates a physical water node of the specified size.
### Arguments

- *vec3* **size** - Water box size in units.

## void setAngularDamping ( float damping )

Sets a value indicating how much the angular velocity of the objects decreases when they get into the physical water. The higher the value is, the lower the angular velocity will be.
### Arguments

- *float* **damping** - Angular damping value. If a negative value is provided, **0** will be used instead.

## float getAngularDamping ( )

Returns the current value indicating how much the angular velocity of the objects decreases when they get into the physical water.
### Return value

Angular damping value.
## Body getContactBody ( int num )

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
## vec3 getContactForce ( int num )

Returns the force in the point of a given contact.
### Arguments

- *int* **num** - Contact number.

### Return value

Force value.
## Vec3 getContactPoint ( int num )

Returns the coordinates of the contact point.
### Arguments

- *int* **num** - Contact number.

### Return value

Contact point coordinates.
## vec3 getContactVelocity ( int num )

Returns the relative velocity between the object and the physical water.
### Arguments

- *int* **num** - Contact number.

### Return value

Relative velocity in units per second.
## void setDensity ( float density )

Sets the density of the water that determines buoyancy of objects that float in the physical water. The higher the value is, the higher buoyancy of the object.
### Arguments

- *float* **density** - Density value. If a negative value is provided, **0** will be used instead.

## float getDensity ( )

Returns the current density of the physical water that determines buoyancy of objects that float in the physical water.
### Return value

Density value.
## void setLinearDamping ( float damping )

Sets a value indicating how much the linear velocity of the objects decreases when they get into the physical water. The higher the value is, the lower the linear velocity will be.
### Arguments

- *float* **damping** - Linear damping value. If a negative value is provided, **0** will be used instead.

## float getLinearDamping ( )

Returns the current value indicating how much the linear velocity of the objects decreases when they get into the physical water.
### Return value

Linear damping value.
## int getNumContacts ( )

Returns the number of contacts between the physical water and the objects.
### Return value

Number of contacts.
## void setSize ( vec3 size )

Sets the size of the physical water node.
### Arguments

- *vec3* **size** - Water box size in units.

## vec3 getSize ( )

Returns the current size of the physical water node.
### Return value

Water box size.
## void setVelocity ( vec3 velocity )

Sets velocity of the flow in physical water.
### Arguments

- *vec3* **velocity** - Velocity in units per second.

## vec3 getVelocity ( )

Returns the current velocity of the flow in physical water.
### Return value

Velocity in units per second.
## static int type ( )

Returns the type of the node.
### Return value

[Physical](../../../api/library/physics/class.physical_usc.md) type identifier.
