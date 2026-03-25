# Unigine.PlayerSpectator Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Player


This class is used to create a free flying camera without a physical body. It is approximated with a sphere, which allows it to [collide](#setCollision_int_void) with objects (but it cannot, for example, push or interact with them). It can also [accelerate](#setAcceleration_float_void) and [damp](#setDamping_float_void) its velocity.


### See Also


- C++ sample
- C# component sample
- UnigineScript sample


## PlayerSpectator Class

### Members

---

## static PlayerSpectator ( )

Constructor. Creates a new spectator with default properties.
## void setAcceleration ( float acceleration )

Sets an acceleration of the spectator.
### Arguments

- *float* **acceleration** - New acceleration in units per second squared. If a negative value is provided, 0 will be used instead.

## float getAcceleration ( )

Returns the current acceleration of the spectator.
### Return value

Acceleration, in units per second squared.
## void setCollision ( int collision )

Updates a value indicating if collisions with spectator's sphere should be taken into account.
### Arguments

- *int* **collision** - 1 to enable collisions, 0 to let the spectator fly through objects.

## int getCollision ( )

Returns a value indicating if collisions with spectator's sphere should be taken into account.
### Return value

1 if collisions are taken into account; otherwise, 0.
## void setCollisionMask ( int mask )

Sets a collision mask for the spectators's collision sphere. Two objects collide, if they both have matching masks.
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getCollisionMask ( )

Returns a collision mask of the spectators's collision sphere. Two objects collide, if they both have matching masks.
### Return value

Integer, each bit of which is a mask.
## void setCollisionRadius ( float radius )

Updates radius of the spectators's collision sphere.
### Arguments

- *float* **radius** - New radius of the collision sphere.

## float getCollisionRadius ( )

Returns radius of the spectators's collision sphere.
### Return value

Radius of the collision sphere in units.
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

Returns a shape that collided with the player.
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

Sets spectator's damping.
### Arguments

- *float* **damping** - New damping.

## float getDamping ( )

Returns spectator's damping.
### Return value

Damping.
## void setMaxThetaAngle ( float angle )

Sets the maximum theta angle (zenith angle, also known as pitch angle) that determines how far downward the player can look.
### Arguments

- *float* **angle** - New angle in degrees in range [0;90]. The higher the value, the further down the player can look.

## float getMaxThetaAngle ( )

Returns the maximum theta angle (zenith angle, also known as pitch angle) that determines how far downward the player can look. The higher the value, the further down the player can look.
### Return value

The current maximum theta angle in degrees.
## void setMaxVelocity ( float velocity )

Sets the velocity of the spectator, which is used while the spectator runs (while [CONTROLS_STATE_RUN](../../../api/library/controls/class.controls_usc.md#STATE_RUN) is "pressed").
### Arguments

- *float* **velocity** - New velocity in units per second. If a negative value is provided, 0 will be used instead.

## float getMaxVelocity ( )

Returns the velocity of the spectator, which is used while the spectator runs (while [CONTROLS_STATE_RUN](../../../api/library/controls/class.controls_usc.md#STATE_RUN) is "pressed").
### Return value

Velocity in units per second.
## void setMinThetaAngle ( float angle )

Sets the minimum theta angle (zenith angle, also known as pitch angle) that determines how far upward the player can look.
### Arguments

- *float* **angle** - New angle in degrees in range [-90;0]. The lower the value, the further up the player can look.

## float getMinThetaAngle ( )

Returns the minimum theta angle (zenith angle, also known as pitch angle) that determines how far upward the player can look. The lower the value, the further up the player can look.
### Return value

The current minimum Theta angle in degrees.
## void setMinVelocity ( float velocity )

Sets the default velocity of the spectator.
### Arguments

- *float* **velocity** - New velocity in units per second. If a negative value is provided, 0 will be used instead.

## float getMinVelocity ( )

Returns the default velocity of the spectator.
### Return value

Velocity in units per second.
## int getNumContacts ( )

Returns the number of contacts, in which the spectator's sphere participates.
### Return value

Number of contacts.
## void setPhiAngle ( float angle )

Sets the phi angle (azimuth angle, also known as yaw angle). This angle determines the horizontal viewing direction, i.e. left or right.
### Arguments

- *float* **angle** - New angle in degrees. Positive values rotate the player right; negative values rotate it left.

## float getPhiAngle ( )

Returns the phi angle (azimuth angle, also known as yaw angle). This angle determines the horizontal viewing direction, i.e. left or right. Positive values rotate the player to the right; negative values rotate it to the left.
### Return value

Phi angle value.
## void setThetaAngle ( float angle )

Sets the theta angle of the player (zenith angle, also known as pitch angle). This angle determines the vertical viewing direction, i.e. upwards or downwards. The value will be clamped between the minimum and the maximum theta angle.
### Arguments

- *float* **angle** - New angle in degrees in range [-90;90]. If a positive value is specified, the player will look upwards; if a negative value is specified, the player will look downwards.

## float getThetaAngle ( )

Returns the theta angle (zenith angle, also known as pitch angle). This angle determines the vertical viewing direction, i.e. upwards or downwards. If a positive value is returned, the player looks upwards; if a negative value is returned, the player looks downwards. The value is clamped between the [minimum](#setMinThetaAngle_float_void) and the [maximum](#setMaxThetaAngle_float_void) theta angle.
### Return value

Theta angle value.
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

PlayerSpectator [type identifier](../../../api/library/nodes/class.node_usc.md#PLAYER_SPECTATOR).
