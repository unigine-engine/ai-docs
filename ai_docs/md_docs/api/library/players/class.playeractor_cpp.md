# Unigine.PlayerActor Class (CPP)

**Header:** #include <UniginePlayers.h>

**Inherits from:** Player


Interface for player actor handling.


To use this class, include the `UniginePlayerActor.h` file.


### See Also


UnigineScript samples:


-
-


## PlayerActor Class

### Members

---

## static PlayerActorPtr create ( )

Constructor. Creates a new actor with default properties.
## void setAcceleration ( float acceleration )

Sets an acceleration of the actor.
### Arguments

- *float* **acceleration** - New acceleration in units per second squared. If a negative value is provided, 0 will be used instead.

## float getAcceleration ( ) const

Returns the current acceleration of the actor.
### Return value

Acceleration in units per second squared.
## Ptr < Body > getBody ( ) const

Returns a [rigid body](../../../api/library/physics/class.bodyrigid_cpp.md), if the body is [simulated physically](#isPhysical_int) (*isPhysical(1)*); otherwise a [dummy body](../../../api/library/physics/class.bodydummy_cpp.md) will be returned (*isPhysical(0)*).
### Return value

Actor body.
## void setCeiling ( int ceiling )

Sets a value indicating if the actor touches the ceiling surface with its head.
### Arguments

- *int* **ceiling** - 1 to indicate that an actor touches the ceiling; otherwise, 0.

## int getCeiling ( ) const

Returns a value indicating if the actor touches the ceiling surface with its head.
### Return value

1 if the actor touches the ceiling; otherwise, 0.
## void setCollision ( int collision )

Sets a value indicating if collisions with a player's capsule should be taken into account. This method is valid only in case *setPhysical()* is set to 0 and does not handle collisions automatically.
### Arguments

- *int* **collision** - 1 to enable collisions, 0 not to handle collisions with the actor.

## int getCollision ( ) const

Returns a value indicating if collisions with a player's capsule should be taken into account. This method is valid only in case *setPhysical()* is set to 0 and does not handle collisions automatically.
### Return value

1 if collisions are taken into account; otherwise, 0.
## void setCollisionHeight ( float height )

Sets a height of actor's capsule.
### Arguments

- *float* **height** - New height in units. If a negative value is provided, 0 will be used instead.

## float getCollisionHeight ( ) const

Returns the height of actor's capsule.
### Return value

Height in units.
## void setCollisionMask ( int mask )

Sets a collision mask for the actor. Two objects collide, if they both have matching masks (i.e. at least one bit matches).
### Arguments

- *int* **mask** - Integer value, each bit of which is used to set a bit mask.

## int getCollisionMask ( ) const

Returns the collision mask of the actor. Two objects collide, if they both have matching masks (i.e. at least one bit matches).
### Return value

integer value, each bit of which is used to set a bit mask.
## void setCollisionRadius ( float radius )

Sets a radius of actor's capsule.
### Arguments

- *float* **radius** - New radius in units. If a negative value is provided, 0 will be used instead.

## float getCollisionRadius ( ) const

Returns the radius of actor's capsule.
### Return value

Radius in units.
## float getContactDepth ( int contact ) const

Returns penetration depth by the given contact.
### Arguments

- *int* **contact** - Contact number.

### Return value

Penetration depth.
## Math:: vec3 getContactNormal ( int contact ) const

Returns a normal of the contact point, in world coordinates.
### Arguments

- *int* **contact** - Contact number.

### Return value

Normal of the contact point.
## Ptr < Object > getContactObject ( int contact ) const

Returns an object participating in the contact with the player (used for collisions with physical object).
### Arguments

- *int* **contact** - Contact number.

### Return value

Object in contact.
## Math:: Vec3 getContactPoint ( int contact ) const

Returns world coordinates of the contact point.
### Arguments

- *int* **contact** - Contact number.

### Return value

Contact point.
## Ptr < Shape > getContactShape ( int num ) const

Returns a shape that collided with the player's capsule.
### Arguments

- *int* **num** - Contact number.

### Return value

Shape in contact.
## int getContactSurface ( int contact ) const

Returns the surface of the current object, which is in contact (used for collisions with non-physical object).
### Arguments

- *int* **contact** - Contact number.

### Return value

Surface number.
## void setDamping ( float damping )

Sets actor's velocity damping with the time.
### Arguments

- *float* **damping** - New velocity damping. If a negative value is provided, 0 will be used instead.

## float getDamping ( ) const

Returns actor's velocity damping with the time.
### Return value

Velocity damping.
## void setGround ( int ground )

Sets a flag indicating that the actor currently stands on the ground surface. This flag is used to set actor state, i.e. play the corresponding skinned animation of standing/walking instead of being in the air.
### Arguments

- *int* **ground** - 1 to indicate that the actor is on the ground; otherwise, 0.

## int getGround ( ) const

Returns a flag indicating if the actor currently stands on the ground surface. This flag is used to determine the actor state, i.e. play the corresponding skinned animation of standing/walking instead of being in the air.
### Return value

1 if the actor is on the ground; otherwise, 0.
## void setPhysicsIntersectionMask ( int mask )

Sets a [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for a player (masks are considered matching if at least one bit matches).
### Arguments

- *int* **mask** - An integer value, each bit of which is used to set a bit mask.

## int getPhysicsIntersectionMask ( ) const

Returns the current [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for a player (masks are considered matching if at least one bit matches).
### Return value

An integer value, each bit of which is used to set a bit mask.
## void setJumping ( float jumping )

Sets a jumping coefficient. The greater the value, the higher the actor jumps.
### Arguments

- *float* **jumping** - Jumping coefficient. If a negative value is provided, 0 will be used instead.

## float getJumping ( ) const

Returns the current jumping coefficient.
### Return value

Jumping coefficient.
## void setMaxFriction ( float friction )

Sets a friction value for the actor that is used when the actor doesn't move, i.e. stands still on the ground. See also *setMinFriction()*.
### Arguments

- *float* **friction** - Friction value. If a negative value is provided, 0 will be used instead.

## float getMaxFriction ( ) const

Returns the friction value set for the actor that is used when the actor doesn't move, i.e. stands still on the ground. See also *getMinFriction()*.
### Return value

Friction value.
## void setMaxThetaAngle ( float angle )

Sets the maximum theta angle (zenith angle, also known as pitch angle) that determines how far downward the player can look.
### Arguments

- *float* **angle** - New maximum angle in degrees in range [0;90]. The higher the value, the further down the player can look.

## float getMaxThetaAngle ( ) const

Returns the maximum theta angle (zenith angle, also known as pitch angle) that determines how far downward the player can look. The higher the value, the further down the player can look.
### Return value

Angle in degrees.
## void setMaxVelocity ( float velocity )

Sets the velocity of the actor, which is used while the actor runs.
### Arguments

- *float* **velocity** - New velocity in units per second. If a negative value is provided, 0 will be used instead.

## float getMaxVelocity ( ) const

Returns the velocity of the actor, which is used while the actor runs.
### Return value

Velocity in units per second.
## void setMinFriction ( float friction )

Sets a friction value for the actor that is used when the actor walks upon the ground. See also *setMaxFriction()*.
### Arguments

- *float* **friction** - Friction value. If a negative value is provided, 0 will be used instead.

## float getMinFriction ( ) const

Returns the friction value set for the actor that is used when the actor walks upon the ground. See also *getMaxFriction()*.
### Return value

Friction value.
## void setMinThetaAngle ( float angle )

Sets the minimum theta angle (zenith angle, also known as pitch angle) that determines how far upward the player can look.
### Arguments

- *float* **angle** - New minimum angle in degrees in range [-90;0]. The lower the value, the further up the player can look.

## float getMinThetaAngle ( ) const

Returns the minimum theta angle (zenith angle, also known as pitch angle) that determines how far upward the player can look. The lower the value, the further up the player can look.
### Return value

Angle in degrees.
## void setMinVelocity ( float velocity )

Sets the default velocity of the actor.
### Arguments

- *float* **velocity** - New velocity in units per second. If a negative value is provided, 0 will be used instead.

## float getMinVelocity ( ) const

Returns the default velocity of the actor.
### Return value

Velocity in units per second.
## int getNumContacts ( ) const

Returns the number of contacts, in which the player's capsule participates.
### Return value

Number of contacts.
## void setPhiAngle ( float angle )

Sets the phi angle (azimuth angle, also known as yaw angle). This angle determines the horizontal viewing direction, i.e. left or right.
### Arguments

- *float* **angle** - New angle in degrees. Positive values rotate the player to the right; negative values rotate it to the left.

## float getPhiAngle ( ) const

Returns the phi angle (azimuth angle, also known as yaw angle). This angle determines the horizontal viewing direction, i.e. left or right. Positive values rotate the player to the right; negative values rotate it to the left.
### Return value

Angle in degrees.
## void setPhysical ( bool physical )

Sets a value indicating whether the actor should interact with the environment as a physical object or not (enables or disables its [rigid body](../../../api/library/physics/class.bodyrigid_cpp.md)). If disabled, collisions can be handled using [setCollision()](#setCollision_int_void) method.
### Arguments

- *bool* **physical** - Physical flag: **true** to enable rigid body model, **false** to disable it.

## bool isPhysical ( ) const

Returns a value indicating whether the actor interacts with the environment as a physical object or not.
### Return value

Physical flag: true if rigid body model is enabled; otherwise, false.
## void setPhysicalMask ( int mask )

Sets the bit mask for interaction with physicals. Two objects interact, if they both have matching masks (i.e. at least one bit matches).
### Arguments

- *int* **mask** - An integer value, each bit of which is used to set a bit mask.

## int getPhysicalMask ( ) const

Returns the bit mask for interaction with physicals. Two objects interact, if they both have matching masks (i.e. at least one bit matches).
### Return value

An integer value, each bit of which is used to set a bit mask.
## void setPhysicalMass ( float mass )

Sets a mass of the actor. If g (Earth's gravity) equals to 9.8 m/s2, and 1 unit equals to 1 meter, the mass is measured in kilograms.
### Arguments

- *float* **mass** - New mass value. If a negative value is provided, 0 will be used instead.

## float getPhysicalMass ( ) const

Returns the current mass of the actor. If g (Earth's gravity) equals to 9.8 m/s2, and 1 unit equals to 1 meter, the mass is measured in kilograms.
### Return value

Mass value.
## Ptr<ShapeCapsule> getShape ( ) const

Returns a shape, which approximates the actor in physical interactions.
### Return value

Actor shape.
## int getState ( int arg1 ) const

Returns a value indicating if the actor is in a given state.
### Arguments

- *int* **arg1** - One of the available states with the STATE_* prefix.

### Return value

1 if the actor is in the given state; otherwise, 0.
## float getStateTime ( int arg1 ) const

Returns time spent by the actor in a given state.
### Arguments

- *int* **arg1** - One of the available states with the STATE_* prefix.

### Return value

Time in seconds spent by the actor in a given state.
## void setThetaAngle ( float angle )

Sets the theta angle of the player (zenith angle, also known as pitch angle). This angle determines the vertical viewing direction, i.e. upward and downward. The value will be clamped between the minimum and the maximum theta angle.
### Arguments

- *float* **angle** - New angle in degrees in range [-90;90]. If a positive value is specified, the player will look upwards; if a negative value is specified, the player will look downwards.

## float getThetaAngle ( ) const

Returns the theta angle (zenith angle, also known as pitch angle). This angle determines the vertical viewing direction, i.e. upwards or downwards. If a positive value is returned, the player looks upwards; if a negative value is returned, the player looks downwards. The value is clamped between the minimum and the maximum theta angle.
### Return value

Angle in degrees.
## void setTurning ( float turning )

Sets a velocity of player turning.
### Arguments

- *float* **turning** - Turning velocity in degrees per second. If a negative value is provided, 0 will be used instead.

## float getTurning ( ) const

Returns a velocity of player turning.
### Return value

Turning velocity in degrees per second.
## void setViewDirection ( const Math:: vec3 & direction )

Sets a new Player's view direction vector.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **direction** - New view direction vector to be set.

## Math:: vec3 getViewDirection ( ) const

Returns the current Player's view direction vector.
### Return value

Current Player's view direction vector.
## static int type ( )

Returns the type of the player.
### Return value

PlayerActor [type identifier](../../../api/library/nodes/class.node_cpp.md#PLAYER_ACTOR).
## void setMaxStepHeight ( float height )

Sets the maximum step height. The value defines the maximum height of a surface to which the player can make a step; it can be used for walking up and down the stairs and over curbs.
### Arguments

- *float* **height** - Maximum step height. > **Notice:** Used only when the body is not [simulated physically](#isPhysical_int) (isPhysical(0)).

## float getMaxStepHeight ( ) const

Returns the maximum height of a surface to which the player can make a step.
### Return value

Maximum step height.
