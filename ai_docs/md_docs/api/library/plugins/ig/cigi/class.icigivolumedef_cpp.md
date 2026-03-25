# CigiVolumeDef Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiVolumeDef Class

### Members

---

## int getEntityID ( ) const

Returns the entity ID specified in the packet.
### Return value

Entity ID.
## int getVolumeID ( ) const

Returns the volume ID specified in the packet.
### Return value

Volume ID.
## int getVolumeEnabled ( ) const

Returns the value of the **Volume Enable** parameter specified in the packet.
### Return value

**Volume Enable** parameter value: 1 - the volume will be considered during collision testing; otherwise, 0.
## int getVolumeType ( ) const

Returns the value of the **Volume Type** parameter specified in the packet.
### Return value

**Volume Type** parameter value. The following values are supported:
- 0 - Sphere
- 1 - Cuboid


## Math:: vec3 getCenter ( ) const

Returns the coordinates of the offset of the center of the collision volume specified in the packet.
### Return value

Offset of the center of the collision volume.
> **Notice:** Measured with respect to the coordinate system of the entity specified by the [Entity ID](#getEntityID_int) parameter


## Math:: vec3 getSize ( ) const

Returns the size of the collision volume specified in the packet.
### Return value

Sizes of the collision volume: (height, width, depth).
> **Notice:** For spherical volumes only the first component of the vector is considered - it is interpreted as radius.


## Math:: vec3 getRotation ( ) const

Returns the rotation euler angles of the collision volume specified in the packet.
### Return value

Collision volume rotation euler angles (roll, pitch, yaw).
## float getRadius ( ) const

Returns the radius of the spherical collision volume specified in the packet.
### Return value

Collision volume radius.
