# CigiRateControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiRateControl Class

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
## int getToPart ( ) const

Returns the value of the **Aply to Articulated Part** parameter specified in the packet.
### Return value

**Aply to Articulated Part** parameter value: 1 - the rate specified in the packet shall be applied to the articulated part; 0 - the rate specified in the packet shall be applied to the entity.
## int getLocal ( ) const

Returns the value of the **Coordinate System** parameter specified in the packet.
### Return value

**Coordinate System** parameter value: 1 - Local; 0 - World/Parent.
## Math:: vec3 getLinear ( ) const

Returns the linear velocity vector specified in the packet.
### Return value

Linear velocity vector.
## Math:: vec3 getAngular ( ) const

Returns the angular velocity vector specified in the packet.
### Return value

Angular velocity vector.
