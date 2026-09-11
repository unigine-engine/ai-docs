# Unigine.PlayerActor Class (CS)

**Inherits from:** Player


Interface for player actor handling.


To use this class, include the `UniginePlayerActor.h` file.


### See Also


UnigineScript samples:


-
-


## PlayerActor Class

### Properties

## 🔒︎ int NumContacts

The number of contacts, in which the player's capsule participates.
## 🔒︎ ShapeCapsule Shape

The A shape, which approximates the actor in physical interactions.
## 🔒︎ Body Body

The A [rigid body](../../../api/library/physics/class.bodyrigid_cs.md), if the body is [simulated physically](#isPhysical_int) (*isPhysical(1)*); otherwise a *[Dummy Body](../../../api/library/physics/class.bodydummy_cs.md)* will be returned (*isPhysical(0)*).
## int Ceiling

The A value indicating if the actor touches the ceiling surface with its head.
## int Ground

The A flag indicating if the actor currently stands on the ground surface. this flag is used to determine the actor state, i.e. play the corresponding skinned animation of standing/walking instead of being in the air.
## vec3 ViewDirection

The current player's view direction vector.
## float ThetaAngle

The theta angle (zenith angle, also known as pitch angle). this angle determines the vertical viewing direction, i.e. upwards or downwards. if a positive value is returned, the player looks upwards; if a negative value is returned, the player looks downwards. the value is clamped between the minimum and the maximum theta angle.
## float PhiAngle

The phi angle (azimuth angle, also known as yaw angle). this angle determines the horizontal viewing direction, i.e. left or right. positive values rotate the player right; negative values rotate the player left.
## float MaxStepHeight

The maximum height of a surface to which the player can make a step.
## float Jumping

The current jumping coefficient.
## float Turning

The A velocity of player turning.
## float Damping

The Actor's velocity damping with the time.
## float Acceleration

The current acceleration of the actor.
## float MaxThetaAngle

The maximum theta angle (zenith angle, also known as pitch angle) that determines how far downward the player can look. the higher the value, the further down the player can look.
## float MinThetaAngle

The minimum theta angle (zenith angle, also known as pitch angle) that determines how far upward the player can look. the lower the value, the further up the player can look.
## float MaxVelocity

The velocity of the actor, which is used while the actor runs.
## float MinVelocity

The default velocity of the actor.
## float MaxFriction

The friction value set for the actor that is used when the actor doesn't move, i.e. stands still on the ground. see also *getMinFriction()*.
## float MinFriction

The friction value set for the actor that is used when the actor walks upon the ground. see also *getMaxFriction()*.
## float CollisionHeight

The height of actor's capsule.
## float CollisionRadius

The radius of actor's capsule.
## int CollisionMask

The collision mask of the actor. two objects collide, if they both have matching masks (i.e. at least one bit matches).
## int Collision

The A value indicating if collisions with a player's capsule should be taken into account. this method is valid only in case *setPhysical()* is set to 0 and does not handle collisions automatically.
## int PhysicsIntersectionMask

The A [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for a player.
## int PhysicalMask

The bit mask for interaction with physicals. two objects interact, if they both have matching masks (i.e. at least one bit matches).
## float PhysicalMass

The current mass of the actor. if g (Earth's gravity) equals to 9.8 m/s^2, and 1 unit equals to 1 meter, the mass is measured in kilograms.
## bool Physical

The A value indicating whether the actor interacts with the environment as a physical object or not.
### Members

---

## PlayerActor ( )

Constructor. Creates a new actor with default properties.
## float GetContactDepth ( int contact )

Returns penetration depth by the given contact.
### Arguments

- *int* **contact** - Contact number.

### Return value

Penetration depth.
## vec3 GetContactNormal ( int contact )

Returns a normal of the contact point, in world coordinates.
### Arguments

- *int* **contact** - Contact number.

### Return value

Normal of the contact point.
## Object GetContactObject ( int contact )

Returns an object participating in the contact with the player (used for collisions with physical object).
### Arguments

- *int* **contact** - Contact number.

### Return value

Object in contact.
## vec3 GetContactPoint ( int contact )

Returns world coordinates of the contact point.
### Arguments

- *int* **contact** - Contact number.

### Return value

Contact point.
## Shape GetContactShape ( int num )

Returns a shape that collided with the player's capsule.
### Arguments

- *int* **num** - Contact number.

### Return value

Shape in contact.
## int GetContactSurface ( int contact )

Returns the surface of the current object, which is in contact (used for collisions with non-physical object).
### Arguments

- *int* **contact** - Contact number.

### Return value

Surface number.
## int GetState ( int arg1 )

Returns a value indicating if the actor is in a given state.
### Arguments

- *int* **arg1** - One of the *PLAYER_ACTOR_STATE_** pre-defined variables.

### Return value

1 if the actor is in the given state; otherwise, 0.
## float GetStateTime ( int arg1 )

Returns time spent by the actor in a given state.
### Arguments

- *int* **arg1** - One of the *PLAYER_ACTOR_STATE_** pre-defined variables.

### Return value

Time in seconds spent by the actor in a given state.
## static int type ( )

Returns the type of the player.
### Return value

PlayerActor [type identifier](../../../api/library/nodes/class.node_cs.md#PLAYER_ACTOR).
