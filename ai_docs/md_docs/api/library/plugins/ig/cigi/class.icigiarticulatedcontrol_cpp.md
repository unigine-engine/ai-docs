# CigiArticulatedControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiArticulatedControl Class

### Members

---

## int getEntityID ( ) const

Returns the entity ID specified in the packet.
### Return value

Entity ID.
## int getPartID ( ) const

Returns the articulated part ID specified in the packet.
### Return value

Articulated part ID.
## int getPartEnabled ( ) const

Returns the value of the **Articulated Part Enable** parameter specified in the packet.
### Return value

**Articulated Part Enable** parameter value: 1 if the articulated part is enabled; otherwise, 0.
## Math:: ivec3 getOffsetEnabled ( ) const

Returns a three-component vector combining **Offset Enable** values specified in the packet. Each value determines whether the offset for the corresponding axis(X - back, Y - left, Z - down) is enabled.
### Return value

Vector of three integer values. Each value determines whether the offset for the corresponding axis(X - back, Y - left, Z - down) is enabled: 1 - enabled; 0 - disabled.
## Math:: ivec3 getRotationEnabled ( ) const

Returns a three-component vector combining **Roll/Pitch/Yaw Enable** values specified in the packet. Each value determines whether the rotation around the corresponding axis(roll, pitch, yaw) is enabled.
### Return value

Vector of three integer values. Each value determines whether the rotation for the corresponding axis(X - back, Y - left, Z - down) is enabled: 1 - enabled; 0 - disabled.
## Math:: vec3 getOffset ( ) const

Returns the offset of the articulated part in the submodel coordinate system (SCS) specified in the packet.
### Return value

Articulated part offset coordinates (X - back, Y - left, Z - down).
## Math:: vec3 getRotation ( ) const

Returns the rotation of the articulated part in the submodel coordinate system (SCS) specified in the packet.
### Return value

Articulated part rotation euler angles.
