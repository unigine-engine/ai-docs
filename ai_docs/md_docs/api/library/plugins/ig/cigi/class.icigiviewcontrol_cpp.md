# CigiViewControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiViewControl Class

### Members

---

## int getViewID ( ) const

Returns the view ID specified in the packet.
### Return value

View ID.
## int getGroupID ( ) const

Returns the view group ID specified in the packet.
### Return value

View group ID. 0 - means the view is not a member of any group.
## int getEntityID ( ) const

Returns the entity ID specified in the packet.


> **Notice:** This value shall be ignored if the view is in a group.


### Return value

Entity ID.
## Math:: ivec3 getOffsetEnabled ( ) const

Returns a three-component vector combining **Offset Enable** values specified in the packet. Each value determines whether the offset for the corresponding axis(X - back, Y - left, Z - down) is enabled.
### Return value

Vector of three integer values. Each value determines whether the offset for the corresponding axis(X - back, Y - left, Z - down) is enabled: 1 - enabled; 0 - disabled.
## Math:: ivec3 getRotationEnabled ( ) const

Returns a three-component vector combining **Roll/Pitch/Yaw Enable** values specified in the packet. Each value determines whether the rotation around the corresponding axis(roll, pitch, yaw) is enabled.
### Return value

Vector of three integer values. Each value determines whether the rotation around the corresponding axis(Roll, Pitch, Yaw) is enabled: 1 - enabled; 0 - disabled.
## Math:: vec3 getOffset ( ) const

Returns the offset of the view specified in the packet.
### Return value

View offset coordinates (X - back, Y - left, Z - down).
## Math:: vec3 getRotation ( ) const

Returns the rotation of the view specified in the packet.
### Return value

View rotation euler angles.
