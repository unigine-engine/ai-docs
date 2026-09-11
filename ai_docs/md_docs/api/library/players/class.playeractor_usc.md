# Unigine.PlayerActor Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Player


This class is used to create a player with a rigid [physical body](#isPhysical_int). It is approximated with a capsule (of a certain [radius](#setCollisionRadius_float_void) and [height](#setCollisionHeight_float_void)) and has such physical parameters as [mass](#setPhysical_int_void) and [friction](#setMaxFriction_float_void). It also [accelerate](#setAcceleration_float_void) and [damp](#setDamping_float_void) its velocity over time. Unlike all other players that can move in any direction, it can only walk on the ground.


Each player state (walking, running, etc.) can be accompanied with one of the four helper states:


- [PLAYER_ACTOR_STATE_BEGIN](#STATE_BEGIN)
- [PLAYER_ACTOR_STATE_ENABLED](#STATE_ENABLED)
- [PLAYER_ACTOR_STATE_END](#STATE_END)
- [PLAYER_ACTOR_STATE_DISABLED](#STATE_DISABLED)


They appear in the order they are listed above. These states allow you to bind parts of animation to them.


### See Also


UnigineScript samples:


-
-


## PlayerActor Class

### Members

---

## static PlayerActor ( )

Constructor. Creates a new actor with default properties.
## void setAcceleration ( float acceleration )

Sets an acceleration of the actor.
### Arguments

- *float* **acceleration** - New acceleration in units per second squared. If a negative value is provided, 0 will be used instead.

## float getAcceleration ( )

Returns the current acceleration of the actor.
### Return value

Acceleration in units per second squared.
## Body getBody ( )

Returns a [rigid body](../../../api/library/physics/class.bodyrigid_usc.md), if the body is [simulated physically](#isPhysical_int) (*isPhysical(1)*); otherwise a [dummy body](../../../api/library/physics/class.bodydummy_usc.md) will be returned (*isPhysical(0)*).
### Return value

Actor body.
## void setCeiling ( int ceiling )

Sets a value indicating if the actor touches the ceiling surface with its head.
### Arguments

- *int* **ceiling** - Positive value to indicate that an actor touches the ceiling; otherwise, **0**.

## int getCeiling ( )

Returns a value indicating if the actor touches the ceiling surface with its head.
### Return value

1 if the actor touches the ceiling; otherwise, 0.
## void setCollision ( int collision )

Sets a value indicating if collisions with a player's capsule should be taken into account. This method is valid only in case *setPhysical()* is set to 0 and does not handle collisions automatically.
### Arguments

- *int* **collision** - Positive number to allow collisions, **0** not to handle collisions with the actor.

## int getCollision ( )

Returns a value indicating if collisions with a player's capsule should be taken into account. This method is valid only in case *setPhysical()* is set to 0 and does not handle collisions automatically.
### Return value

Positive number if collisions are taken into account; otherwise, **0**.
## void setCollisionHeight ( float height )

Sets a height of actor's capsule.
### Arguments

- *float* **height** - New height in units. If a negative value is provided, 0 will be used instead.

## float getCollisionHeight ( )

Returns the height of actor's capsule.
### Return value

Height in units.
## void setCollisionMask ( int mask )

Sets a collision mask for the actor. Two objects collide, if they both have matching masks (i.e. at least one bit matches).
### Arguments

- *int* **mask** - Integer value, each bit of which is used to set a bit mask.

## int getCollisionMask ( )

Returns the collision mask of the actor. Two objects collide, if they both have matching masks (i.e. at least one bit matches).
### Return value

integer value, each bit of which is used to set a bit mask.
## void setCollisionRadius ( float radius )

Sets a radius of actor's capsule.
### Arguments

- *float* **radius** - New radius in units. If a negative value is provided, 0 will be used instead.

## float getCollisionRadius ( )

Returns the radius of actor's capsule.
### Return value

Radius in units.
## float getContactDepth ( int contact )

Returns penetration depth by the given contact.
### Arguments

- *int* **contact** - Contact number.

### Return value

Penetration depth.
## vec3 getContactNormal ( int contact )

Returns a normal of the contact point, in world coordinates.
### Arguments

- *int* **contact** - Contact number.

### Return value

Normal of the contact point.
## Object getContactObject ( int contact )

Returns an object participating in the contact with the player (used for collisions with physical object).
### Arguments

- *int* **contact** - Contact number.

### Return value

Object in contact.
## Vec3 getContactPoint ( int contact )

Returns world coordinates of the contact point.
### Arguments

- *int* **contact** - Contact number.

### Return value

Contact point.
## Shape getContactShape ( int num )

Returns a shape that collided with the player's capsule.
### Arguments

- *int* **num** - Contact number.

### Return value

Shape in contact.
## int getContactSurface ( int contact )

Returns the surface of the current object, which is in contact (used for collisions with non-physical object).
### Arguments

- *int* **contact** - Contact number.

### Return value

Surface number.
## void setDamping ( float damping )

Sets actor's velocity damping with the time.
### Arguments

- *float* **damping** - New velocity damping. If a negative value is provided, 0 will be used instead.

## float getDamping ( )

Returns actor's velocity damping with the time.
### Return value

Velocity damping.
## void setGround ( int ground )

Sets a flag indicating that the actor currently stands on the ground surface. This flag is used to set actor state, i.e. play the corresponding skinned animation of standing/walking instead of being in the air.
### Arguments

- *int* **ground** - Positive value to indicate that the actor is on the ground; otherwise, **0**.

## int getGround ( )

Returns a flag indicating if the actor currently stands on the ground surface. This flag is used to determine the actor state, i.e. play the corresponding skinned animation of standing/walking instead of being in the air.
### Return value

1 if the actor is on the ground; otherwise, 0.
## void setPhysicsIntersectionMask ( int mask )

Sets a [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for a player (masks are considered matching if at least one bit matches).
### Arguments

- *int* **mask** - An integer value, each bit of which is used to set a bit mask.

## int getPhysicsIntersectionMask ( )

Returns the current [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for a player (masks are considered matching if at least one bit matches).
### Return value

An integer value, each bit of which is used to set a bit mask.
## void setJumping ( float jumping )

Sets a jumping coefficient. The greater the value, the higher the actor jumps.
### Arguments

- *float* **jumping** - Jumping coefficient. If a negative value is provided, 0 will be used instead.

## float getJumping ( )

Returns a jumping coefficient.
### Return value

Jumping coefficient.
## void setMaxFriction ( float friction )

Sets a friction value for the actor that is used when the actor doesn't move, i.e. stands still on the ground. See also *setMinFriction()*.
### Arguments

- *float* **friction** - Friction value. If a negative value is provided, 0 will be used instead.

## float getMaxFriction ( )

Returns the friction value set for the actor that is used when the actor doesn't move, i.e. stands still on the ground. See also *getMinFriction()*.
### Return value

Friction value.
## void setMaxThetaAngle ( float angle )

Sets the maximum theta angle (zenith angle, also known as pitch angle) that determines how far downward the player can look.
### Arguments

- *float* **angle** - New maximum angle in degrees in range [0;90]. The higher the value, the further down the player can look.

## float getMaxThetaAngle ( )

Returns the maximum theta angle (zenith angle, also known as pitch angle) that determines how far downward the player can look. The higher the value, the further down the player can look.
### Return value

Angle in degrees.
## void setMaxVelocity ( float velocity )

Sets the velocity of the actor, which is used while the actor runs.
### Arguments

- *float* **velocity** - New velocity in units per second. If a negative value is provided, 0 will be used instead.

## float getMaxVelocity ( )

Returns the velocity of the actor, which is used while the actor runs.
### Return value

Velocity in units per second.
## void setMinFriction ( float friction )

Sets a friction value for the actor that is used when the actor walks upon the ground. See also *setMaxFriction()*.
### Arguments

- *float* **friction** - Friction value. If a negative value is provided, 0 will be used instead.

## float getMinFriction ( )

Returns the friction value set for the actor that is used when the actor walks upon the ground. See also *getMaxFriction()*.
### Return value

Friction value.
## void setMinThetaAngle ( float angle )

Sets the minimum theta angle (zenith angle, also known as pitch angle) that determines how far upward the player can look.
### Arguments

- *float* **angle** - New minimum angle in degrees in range [-90;0]. The lower the value, the further up the player can look.

## float getMinThetaAngle ( )

Returns the minimum theta angle (zenith angle, also known as pitch angle) that determines how far upward the player can look. The lower the value, the further up the player can look.
### Return value

Angle in degrees.
## void setMinVelocity ( float velocity )

Sets the default velocity of the actor.
### Arguments

- *float* **velocity** - New velocity in units per second. If a negative value is provided, 0 will be used instead.

## float getMinVelocity ( )

Returns the default velocity of the actor.
### Return value

Velocity in units per second.
## int getNumContacts ( )

Returns the number of contacts, in which the player's capsule participates.
### Return value

Number of contacts.
## void setPhiAngle ( float angle )

Sets the phi angle (azimuth angle, also known as yaw angle). This angle determines the horizontal viewing direction, i.e. left or right.
### Arguments

- *float* **angle** - New angle in degrees. Positive values rotate the player to the right; negative values rotate it to the left.

## float getPhiAngle ( )

Returns the phi angle (azimuth angle, also known as yaw angle). This angle determines the horizontal viewing direction, i.e. left or right. Positive values rotate the player to the right; negative values rotate it to the left.
### Return value

Angle in degrees.
## void setPhysical ( int physical )

Sets a value indicating whether the actor should interact with the environment as a physical object or not (enables or disables its [rigid body](../../../api/library/physics/class.bodyrigid_usc.md)). If disabled, collisions can be handled using [setCollision()](#setCollision_int_void) method.
### Arguments

- *int* **physical** - Physical flag: **1** to enable rigid body model, **0** to disable it.

## int isPhysical ( )

Returns a value indicating whether the actor interacts with the environment as a physical object or not.
### Return value

Physical flag: **1** if rigid body model is enabled; otherwise, **0**.
## void setPhysicalMask ( int mask )

Sets the bit mask for interaction with physicals. Two objects interact, if they both have matching masks (i.e. at least one bit matches).
### Arguments

- *int* **mask** - An integer value, each bit of which is used to set a bit mask.

## int getPhysicalMask ( )

Returns the bit mask for interaction with physicals. Two objects interact, if they both have matching masks (i.e. at least one bit matches).
### Return value

An integer value, each bit of which is used to set a bit mask.
## void setPhysicalMass ( float mass )

Sets a mass of the actor. If g (Earth's gravity) equals to 9.8 m/s2, and 1 unit equals to 1 meter, the mass is measured in kilograms.
### Arguments

- *float* **mass** - New mass value. If a negative value is provided, 0 will be used instead.

## float getPhysicalMass ( )

Returns the current mass of the actor. If g (Earth's gravity) equals to 9.8 m/s2, and 1 unit equals to 1 meter, the mass is measured in kilograms.
### Return value

Mass.
## ShapeCapsule getShape ( )

Returns a shape, which approximates the actor in physical interactions.
### Return value

Actor shape.
## int getState ( int arg1 )

Returns a value indicating if the actor is in a given state.
### Arguments

- *int* **arg1** - One of the *PLAYER_ACTOR_STATE_** pre-defined variables.

### Return value

1 if the actor is in the given state; otherwise, 0.
## float getStateTime ( int arg1 )

Returns time spent by the actor in a given state.
### Arguments

- *int* **arg1** - One of the *PLAYER_ACTOR_STATE_** pre-defined variables.

### Return value

Time in seconds spent by the actor in a given state.
## void setThetaAngle ( float angle )

Sets the theta angle of the player (zenith angle, also known as pitch angle). This angle determines the vertical viewing direction, i.e. upward and downward. The value will be clamped between the minimum and the maximum theta angle.
### Arguments

- *float* **angle** - New angle in degrees in range [-90;90]. If a positive value is specified, the player will look upwards; if a negative value is specified, the player will look downwards.

## float getThetaAngle ( )

Returns the theta angle (zenith angle, also known as pitch angle). This angle determines the vertical viewing direction, i.e. upwards or downwards. If a positive value is returned, the player looks upwards; if a negative value is returned, the player looks downwards. The value is clamped between the minimum and the maximum theta angle.
### Return value

Angle in degrees.
## void setTurning ( float turning )

Sets a velocity of player turning.
### Arguments

- *float* **turning** - Turning velocity in degrees per second. If a negative value is provided, 0 will be used instead.

## float getTurning ( )

Returns a velocity of player turning.
### Return value

Turning velocity in degrees per second.
## void setViewDirection ( vec3 direction )

Sets a new Player's view direction vector.
### Arguments

- *vec3* **direction** - New view direction vector to be set.

## vec3 getViewDirection ( )

Returns the current Player's view direction vector.
### Return value

Current Player's view direction vector.
## static int type ( )

Returns the type of the player.
### Return value

PlayerActor [type identifier](../../../api/library/nodes/class.node_usc.md#PLAYER_ACTOR).
## void setMaxStepHeight ( float height )

Sets the maximum step height. The value defines the maximum height of a surface to which the player can make a step; it can be used for walking up and down the stairs and over curbs.
### Arguments

- *float* **height** - Maximum step height. > **Notice:** Used only when the body is not [simulated physically](#isPhysical_int) (isPhysical(0)).

## float getMaxStepHeight ( )

Returns the maximum height of a surface to which the player can make a step.
### Return value

Maximum step height.
