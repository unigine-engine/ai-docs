# Unigine.PlayerPersecutor Class (CS)

**Inherits from:** Player


This class is used to create a free flying camera without a physical body that follows the [target node](#setTarget_Node_void) at the specified [distance](#setDistance_float_void). The exact point of the target it follows is called an [anchor](#setAnchor_vec3_void). The persecutor can either turn around its target or its viewing direction can be [fixed](#setFixed_int_void). Just like [PlayerSpectator](../../../api/library/players/class.playerspectator_cs.md) it is approximated with a sphere, which allows it to [collide](#setCollision_int_void) with objects (but cannot, for example, push or interact with them).


### See Also


UnigineScript samples:


-
-


## PlayerPersecutor Class

### Properties

## 🔒︎ int NumContacts

The number of contacts, in which the player's capsule participates.
## float ThetaAngle

The theta angle (zenith angle, also known as pitch angle). this angle determines the vertical viewing direction, i.e. upwards or downwards. if a positive value is returned, the player looks upwards; if a negative value is returned, the player looks downwards. the value is clamped between the minimum and the maximum theta angle.
## float PhiAngle

The phi angle (azimuth angle, also known as yaw angle). this angle determines the horizontal viewing direction, i.e. left or right. positive values rotate the player right; negative values rotate the player left.
## float Distance

The current distance between the target and the persecutor. the value is clamped between the minimum and the maximum distance values.
## float Turning

The A velocity of player turning.
## float MaxThetaAngle

The maximum theta angle (zenith angle, also known as pitch angle) that determines how far downward the player can look. the higher the value, the further down the player can look.
## float MinThetaAngle

The minimum theta angle (zenith angle, also known as pitch angle) that determines how far upward the player can look. the lower the value, the further up the player can look.
## float MaxDistance

The maximum possible distance between the persecutor and the target.
## float MinDistance

The minimum possible distance between the persecutor and the target.
## vec3 Anchor

The Coordinates of an anchor point (in the target node local coordinates), to which the persecutor is bound.
## Node Target

The object currently followed by the persecutor.
## float CollisionRadius

The Radius of the persecutor's collision sphere.
## int CollisionMask

The A collision mask of the persecutor's collision sphere. two objects collide, if they both have matching masks.
## int Collision

The A value indicating if collisions with persecutor's sphere should be taken into account.
## bool Fixed

The A value indicating if the persecutor can freely rotate around its target or it is oriented strictly in one direction. the fixed viewing direction is the same direction the persecutor was looking in when the *setFixed()* function is called, though it can be reset to another one afterwards.
### Members

---

## PlayerPersecutor ( )

Constructor. Creates a new persecutor with default properties.
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

Normal of the contact point..
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

PlayerPersecutor [type identifier](../../../api/library/nodes/class.node_cs.md#PLAYER_PERSECUTOR).
