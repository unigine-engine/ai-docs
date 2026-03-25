# Unigine.PlayerSpectator Class (CS)

**Inherits from:** Player


Interface for player spectator handling.


To use this class, include the `UniginePlayerSpectator.h` file.


### See Also


- C++ sample
- C# component sample
- UnigineScript sample


## PlayerSpectator Class

### Properties

## 🔒︎ int NumContacts

The number of contacts, in which the spectator's sphere participates.
## float ThetaAngle

The theta angle (zenith angle, also known as pitch angle). this angle determines the vertical viewing direction, i.e. upwards or downwards. if a positive value is returned, the player looks upwards; if a negative value is returned, the player looks downwards. the value is clamped between the minimum and the maximum theta angle.
## float PhiAngle

The phi angle (azimuth angle, also known as yaw angle). this angle determines the horizontal viewing direction, i.e. left or right. positive values rotate the player right; negative values rotate it to the left.
## float Turning

The A velocity of player turning.
## float Damping

The spectator's damping.
## float Acceleration

The current acceleration of the spectator.
## float MaxThetaAngle

The maximum theta angle (zenith angle, also known as pitch angle) that determines how far downward the player can look. the higher the value, the further down the player can look.
## float MinThetaAngle

The minimum theta angle (zenith angle, also known as pitch angle) that determines how far upward the player can look. the lower the value, the further up the player can look.
## float MaxVelocity

The velocity of the spectator, which is used while the spectator runs (the controls::state_run control state is "pressed").
## float MinVelocity

The default velocity of the spectator.
## float CollisionRadius

The Radius of the spectators's collision sphere.
## int CollisionMask

The A collision mask of the spectators's collision sphere. two objects collide, if they both have matching masks.
## int Collision

The A value indicating if collisions with spectator's sphere should be taken into account.
## vec3 ViewDirection

The current player's view direction vector.
### Members

---

## PlayerSpectator ( )

Constructor. Creates a new spectator with default properties.
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

Returns a shape that collided with the player.
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
## static int type ( )

Returns the type of the player.
### Return value

PlayerSpectator [type identifier](../../../api/library/nodes/class.node_cs.md#PLAYER_SPECTATOR).
