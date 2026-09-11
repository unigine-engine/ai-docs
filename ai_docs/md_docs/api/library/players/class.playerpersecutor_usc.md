# Unigine.PlayerPersecutor Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Player


This class is used to create a free flying camera without a physical body that follows the [target node](#setTarget_Node_void) at the specified [distance](#setDistance_float_void). The exact point of the target it follows is called an [anchor](#setAnchor_vec3_void). The persecutor can either turn around its target or its viewing direction can be [fixed](#setFixed_int_void). Just like [PlayerSpectator](../../../api/library/players/class.playerspectator_usc.md) it is approximated with a sphere, which allows it to [collide](#setCollision_int_void) with objects (but cannot, for example, push or interact with them).


### See Also


UnigineScript samples:


-
-


## PlayerPersecutor Class

### Members

---

## static PlayerPersecutor ( )

Constructor. Creates a new persecutor with default properties.
## void setAnchor ( vec3 anchor )

Sets coordinates of an anchor point (in the target node local coordinates), to which the persecutor is bound.
### Arguments

- *vec3* **anchor** - Anchor coordinates.

## vec3 getAnchor ( )

Returns coordinates of an anchor point (in the target node local coordinates), to which the persecutor is bound.
### Return value

Anchor coordinates.
## void setCollision ( int collision )

Sets a value indicating if collisions with persecutor's sphere should be taken into account.
### Arguments

- *int* **collision** - Positive number to allow collisions, **0** to let the persecutor fly through objects.

## int getCollision ( )

Returns a value indicating if collisions with persecutor's sphere should be taken into account.
### Return value

Positive number if collisions are taken into account; otherwise, **0**.
## void setCollisionMask ( int mask )

Sets a collision mask for the persecutor's collision sphere. Two objects collide, if they both have matching masks.
### Arguments

- *int* **mask** - An integer value, each bit of which is used to set a bit mask.

## int getCollisionMask ( )

Returns a collision mask of the persecutor's collision sphere. Two objects collide, if they both have matching masks.
### Return value

An integer value, each bit of which is used to set a bit mask.
## void setCollisionRadius ( float radius )

Sets the radius of the persecutor's collision sphere.
### Arguments

- *float* **radius** - New radius of the collision sphere.

## float getCollisionRadius ( )

Returns radius of the persecutor's collision sphere.
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

Normal of the contact point..
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
## void setDistance ( float distance )

Sets a distance between the target node and the persecutor. The value will be clamped between the minimum and the maximum distance values.
### Arguments

- *float* **distance** - New distance in units.

## float getDistance ( )

Returns the current distance between the target and the persecutor. The value is clamped between the minimum and the maximum distance values.
### Return value

Distance in units.
## void setFixed ( int fixed )

Sets a value indicating if the persecutor can freely rotate around its target or it is oriented strictly in one direction. The fixed viewing direction is the same direction the persecutor was looking in when this function is called, though it can be reset to another one afterwards.
### Arguments

- *int* **fixed** - **1** to orient the player strictly in one direction, **0** to let it rotate freely.

## int isFixed ( )

Returns a value indicating if the persecutor can freely rotate around its target or it is oriented strictly in one direction. The fixed viewing direction is the same direction the persecutor was looking in when [setFixed()](#setFixed_int_void) function is called, though it can be reset to another one afterwards.
### Return value

**1** if the persecutor is oriented strictly in one direction; otherwise, **0**.
## void setMaxDistance ( float distance )

Sets the maximum possible distance between the persecutor and the target.
### Arguments

- *float* **distance** - New distance in units.

## float getMaxDistance ( )

Returns the maximum possible distance between the persecutor and the target.
### Return value

Distance in units.
## void setMaxThetaAngle ( float angle )

Sets the maximum theta angle (zenith angle, also known as pitch angle) that determines how far downward the player can look.
### Arguments

- *float* **angle** - New angle in degrees in range [0;90]. The higher the value, the further down the player can look.

## float getMaxThetaAngle ( )

Returns the maximum theta angle (zenith angle, also known as pitch angle) that determines how far downward the player can look. The higher the value, the further down the player can look.
### Return value

Angle in degrees.
## void setMinDistance ( float distance )

Sets the minimum possible distance between the persecutor and the target.
### Arguments

- *float* **distance** - New distance in units.

## float getMinDistance ( )

Returns the minimum possible distance between the persecutor and the target.
### Return value

Distance in units.
## void setMinThetaAngle ( float angle )

Sets the minimum theta angle (zenith angle, also known as pitch angle) that determines how far upward the player can look.
### Arguments

- *float* **angle** - New angle in degrees in range [-90;0]. The lower the value, the further up the player can look.

## float getMinThetaAngle ( )

Returns the minimum theta angle (zenith angle, also known as pitch angle) that determines how far upward the player can look. The lower the value, the further up the player can look.
### Return value

Angle in degrees.
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
## void setTarget ( Node target )

Sets an object, which will be followed by the persecutor.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **target** - New target node.

## Node getTarget ( )

Returns the object currently followed by the persecutor.
### Return value

Target node.
## void setThetaAngle ( float angle )

Sets the theta angle of the player (zenith angle, also known as pitch angle). This angle determines the vertical viewing direction, i.e. upwards or downwards. The value will be clamped between the minimum and the maximum theta angle.
### Arguments

- *float* **angle** - New angle in degrees in range [-90;90]. If a positive value is specified, the player will look upwards; if a negative value is specified, the player will look downwards.

## float getThetaAngle ( )

Returns the theta angle (zenith angle, also known as pitch angle). This angle determines the vertical viewing direction, i.e. upwards or downwards. If a positive value is returned, the player looks upwards; if a negative value is returned, the player looks downwards. The value is clamped between the [minimum](#setMinThetaAngle_float_void) and the [maximum](#setMaxThetaAngle_float_void) theta angle.
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
## static int type ( )

Returns the type of the player.
### Return value

PlayerPersecutor [type identifier](../../../api/library/nodes/class.node_usc.md#PLAYER_PERSECUTOR).
